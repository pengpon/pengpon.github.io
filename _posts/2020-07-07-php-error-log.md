---
layout: post
title: 	"[PHP]來寫Log吧"
date:   2020-07-06 12:00:00 +0800
author: Pon
categories: self 
tags: php
---

> 為Php又開了一個系列，繼三年前初學者般的體驗過後就好久不見了，Hello PHP!



# 起因

原本有一隻insert.php負責接前端表單Post來的資料，因為處理的事比較單純，當初沒特別記log

於是發生了，使用者在活動登錄頁上傳的圖片未成功轉成圖檔存在主機上

勢必要來加上log，之後如果還有發生才能稍微看出些什麼

<br>



# 架構概述

- 前端:活動頁驗證使用者填寫之資料&是否有上傳符合副檔名格式之圖片(含必填欄位&資料格式是否正確)
- 後端:再次確認部分重要欄位是否有值，先將base64轉成圖檔，計算取得不重複的圖檔名，check不重複欄位是否已存在，insert一筆新的資料至資料庫中



<br>

# Log進場

決定加進log紀錄每一步驟是否成功。

php有內建的error log function可以用，參考[Ultimate Guide to Logging](https://www.loggly.com/ultimate-guide/php-logging-basics/) ,或是有其他php跟log相關的library(ex:monolog)

不過這次選擇自己定義log function的方式，在主要程式中call function `wh_log`傳進要寫入的訊息!

<br>

完整範例:log.php&insert.php

```php
// log.php

<?php
date_default_timezone_set("Asia/Taipei");
 
function wh_log($log_msg)
{
    $log_time = date('Y-m-d H:i:s');
    $log_filename = "log";
    $log_msg='['.$log_time.'] '.$log_msg;

    if (!file_exists($log_filename)) 
    {
        // create directory/folder uploads.
        mkdir($log_filename, 0777, true); // mkdir(pathname[, mode[, recursive[, context]]])
    }
    $log_file_data = $log_filename.'/log_' . date('d-M-Y') . '.log';
    file_put_contents($log_file_data, $log_msg . "\n", FILE_APPEND);
}

set_error_handler(function($errno, $errstr, $errfile, $errline){
    if($errno === E_WARNING){
        wh_log("[".$_POST['ev_mp']."] Warning: ".$errstr);    
    } else {
        // fallback to default php error handler
    }
})

?>
```

```php
// insert.php
<?php
		
		header('Access-Control-Allow-Origin: *');
		require_once("config/db_config.php");
		require_once("log.php");

		if (empty($_POST['ev_na']) || empty($_POST['ev_in']) || empty($_POST['ev_mk']) || empty($_POST['ev_mp'])) {
			echo '{"code":error,"msg":"parameter is empty!" }';
			if (empty($_POST['ev_mp'])) {
				$mobile = 'None';
			} else {
				$mobile = $_POST['ev_mp'];
			}
			$log_msg = "[" . $mobile . "] Error: Parameter can not be empty!";
			wh_log($log_msg); 
			return;
		}

		if (!isset($_POST['p1_64']) || $_POST['p1_64'] == '' || !isset($_POST['p2_64']) || $_POST['p2_64'] == '') {
			echo '{"code":error,"msg":"image is empty!"}';
			$log_msg = "[" . $_POST['ev_mp'] . "] Error: Image can not be empty!";
			wh_log($log_msg);
			return;
		}

		$a0 = $_POST["ev_a0"]; 					// 郵遞區號 聯絡地址
		$r0 = $_POST["ev_r0"];					// 郵遞區號 收件地址
		$invoicedate = $_POST["ev_id"]; 		// 發票日期
		$buymodel = $_POST["ev_pd"]; 			// 型號
		$invoiceno = $_POST["ev_in"];			// 發票號碼
		$serialno = $_POST["ev_mk"];			// 保證書號碼
		$st_ty = $_POST["st_ty"];       		// 購買通路
		$st_sn = $_POST["st_sn"];      			// 購買店家名
		$name = $_POST["ev_na"];				// 姓名
		$gender = $_POST["ev_gd"];				// 性別
		$age = $_POST["ev_yr"];					// 年齡
		$mobile = $_POST["ev_mp"];				// mobile
		$a1 = $_POST["ev_a1"];					// 縣市
		$a2 = $_POST["ev_a2"];					// 區域
		$a3 = $_POST["ev_a3"];					// 地址
		$rname = $_POST["ev_rna"];				// 贈品收件姓名
		$rmobile = $_POST["ev_rmp"];			// 贈品收件電話
		$r1 = $_POST["ev_r1"];					// 贈品收件 縣市
		$r2 = $_POST["ev_r2"];					// 贈品收件 區域
		$r3 = $_POST["ev_r3"];					// 贈品收件 地址
		$ev_rule = $_POST["ev_rule"];			// 隱私權
		$ev_dm = $_POST["ev_dm"];				// 行銷
		$uid = $_POST["uid"];					// vpadn-src
		$gift = $_POST["ev_gift_color"];		// 贈品顏色
		$giftItem = $_POST["ev_gf"];			// 贈品品項

		// other store
		if ($st_sn === '其他') {
			$st_sn = $st_sn . '-' . $st_ty;
		}
		// gift
		if (empty($gift)) {
			$gift = '無';
		}
		$gift = $giftItem . '-' . $gift;
		// invoice.no 
		$invoiceno = strtoupper($invoiceno);

		// set default
		if (empty($ev_rule)) {
			$ev_rule = 0;
		}
		if (empty($ev_dm)) {
			$ev_dm = 0;
		}
		if (empty($uid)) {
			$uid = 'test';
		}

		$address = $a0 . $a1 . $a2 . $a3;
		$prizeaddress = $r0 . $r1 . $r2 . $r3;

		$pic1 =  $_POST["p1_64"];
		$pic2 =  $_POST["p2_64"];

		$invoicefilename = processData($pic1, 'images/invoice');
		$guaranteefilename = processData($pic2, 'images/guarantee');


		// start to connect to db
		$options = [
			PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
			PDO::ATTR_CASE => PDO::CASE_NATURAL,
			PDO::ATTR_ORACLE_NULLS => PDO::NULL_EMPTY_STRING
		];
		try {
			$dbh = new PDO('mysql:host=' . $_DB['host'] . ';dbname=' . $_DB['dbname'],  $_DB['username'], $_DB['password'], $options);
			$dbh->exec("set names utf8");

			// check if data exists or found
			$serial = $dbh->prepare('SELECT name FROM `xxx` WHERE serialno = :serialno');
			$serial->execute(array(':serialno' => $serialno));
			if ($serial->rowCount() > 0) {
				$log_msg = "[" . $mobile . "] Error: Serialno already exist " . $serialno;
				wh_log($log_msg);
				echo json_encode(array(
					'status' => false,
					'message' => 'serialno already exist'
				));
				return;
			}

			// insert data
			$sql = "INSERT INTO `xxx` (name, mobile,gender,age, address, contactname, contactmobile,prizeaddress,gift,buystore,buymodel,invoiceno,invoicedate,serialno,invoicefilename,guaranteefilename,check1,check2,uid) VALUES (:name, :mobile,:gender,:age,:address,:contactname, :contactmobile,:prizeaddress,:gift,:buystore,:buymodel,:invoiceno,:invoicedate,:serialno,:invoicefilename,:guaranteefilename,:check1,:check2,:uid)";
			

			$sth = $dbh->prepare($sql);
			
			$sth->execute(array(
				':name' => $name,
				':mobile' => $mobile,
				':gender' => $gender,
				':age' => $age,
				':address' => $address,
				':contactname' => $rname,
				':contactmobile' => $rmobile,
				':prizeaddress' => $prizeaddress,
				':gift' => $gift,
				':buystore' => $st_sn,
				':buymodel' => $buymodel,
				':invoiceno' => $invoiceno,
				':invoicedate' => $invoicedate,
				':serialno' => $serialno,
				':invoicefilename' => $invoicefilename,
				':guaranteefilename' => $guaranteefilename,
				':check1' => $ev_rule,
				':check2' => $ev_dm,
				':uid' => $uid,

			));

			echo json_encode(array(
				'status' => true,
				'message' => 'upload finish'
			));
			$log_msg = "[" . $mobile . "] Info: Upload to database successed";
			wh_log($log_msg);
			$dbh = NULL;
		} catch (PDOException $e) {
			die("Database connection failed: " . $e->getMessage());
			$log_msg ="[" . $mobile . "] Error: Database connection failed/ Can not Insert to Database";
			wh_log($log_msg);
		}


		function processData($data, $folder)
		{

			try {
				$fileName = getGUID();
				list($type, $data) = explode(';', $data);
				list(, $data)      = explode(',', $data);
				$data = base64_decode($data);

				imagejpeg(imagecreatefromstring($data), $folder . '/' . $fileName . '.jpg', 80); // source,filename, quality
				$log_msg = "[".$_POST['ev_mp']."] Info: Process image Data successed. Path " . $folder;
				wh_log($log_msg);
				return $fileName . ".jpg";
			} catch (Exception $e) {
				echo 'Process image Data falied:' . $e->getMessage();
				$log_msg = "[".$_POST['ev_mp']."] Error: Process image Data falied. Path " . $folder. $e->getMessage();
				wh_log($log_msg);
				return false;
			}
		}

		function getGUID()
		{
			mt_srand((float) microtime() * 10000); //optional for php 4.2.0 and up.
			$charid = strtoupper(md5(uniqid(rand(), true)));
			return $charid;
		}


		?>
```



<br>

自己的話是先決定

1. 那些時間點要加上`wh_log()`&訊息類型
2. log訊息的格式，要包含時間&辨識使用者的id/tel以及訊息重點

例如:

- 資料不齊-->Error: Parameter can not be empty
- 重複輸入-->Error: Serialno already exist
- 成功上傳-->Info: Upload to database successed
- 資料庫錯誤(連不上or其他無法成功insert的時候)-->Error:Database connection failed/ Can not Insert to Database
- 圖片轉檔成功-->Info: Process image Data successed
- 圖片轉檔失敗-->Error: Process image Data falied

<br>

# 插曲

後來發現function `processData`如果傳入的是不支援的格式資料時(ex:一般txt文字檔)，會出現warning , 不是exception, 也就不會進到catch block。

於是在log.php再加了`set_error_handler` function

定義warning出現時，要執行的Process

```php
set_error_handler(function($errno, $errstr, $errfile, $errline){
    if($errno === E_WARNING){
        wh_log("[".$_POST['ev_mp']."] Warning: ".$errstr);    
    } else {
        // fallback to default php error handler
    }
})
```

<br>

# Result

最後log的格式會像:

```
[2020-07-01 10:52:14] [0900000000] Warning: imagecreatefromstring(): Data is not in a recognized format
[2020-07-01 10:52:14] [0900000000] Warning: imagejpeg() expects parameter 1 to be resource, boolean given
```



<br>

# 其他

## php內建error_log

預設error會記錄到webserver中的error log中

Ex:`Apache: /var/log/apache2/error.log` ，`Nginx: /var/log/nginx/error.log`

範例:

```php
<?php
error_log('Your message here');
?>
```

log格式

```
// cat /var/log/apache2/error_log

[Mon Jul 06 15:39:01.046015 2020] [php7:notice] [pid 9793] [client ::1:60224] Your message here, referer: http://localhost/~pon.peng/
```

[Error_log語法,by官網](https://www.php.net/manual/en/function.error-log.php)

<br>

## libraries

- monolog

- Analog
- log4php

可參考[Ultimate Guide to Logging](https://www.loggly.com/ultimate-guide/php-logging-libraries/)



<br>



# 延伸閱讀&參考圖文

[精通 PHP 錯誤處理，讓除錯更自在](https://www.slideshare.net/asika32764/php-day-35-php)

[PHP Monolog Tutorial: A Step by Step Guide](https://stackify.com/php-monolog-tutorial/)

[PHP Try Catch: Basics & Advanced PHP Exception Handling Tutorial](https://stackify.com/php-try-catch-php-exception-tutorial/)

[Ultimate Guide to Logging](https://www.loggly.com/ultimate-guide/php-logging-libraries/)