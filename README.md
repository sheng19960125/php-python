## 在php中調用python  
### 目的
* 輸入一張含有民信片的圖->輸出只含民信片的圖。   
### 流程
1.利用html自帶form表單 input file上傳圖檔     
```
<form class="form-horizontal" method="POST" action="/index.php/python/image" enctype="multipart/form-data">
  <input type="file">      
<form>
```
2.在controller調用python函數，使圖片名稱傳值傳到python中。     
```
<?php
  $params = "value"; #傳遞給python指令碼的入口引數  
  $path="python test.py "; //需要注意的是：末尾要加一個空格
  print_r($path);
  passthru($path.$params);//等同於命令`python python.py 引數`，並接收列印出來的資訊 
?> 
```
3.python取到照片名稱，移至路徑下取得照片圖檔，進行解析。    
4.解析後圖片保存至相對路徑下，或是利用base64進行編碼，返回回傳值。   
5.取得回傳值，至路徑下取得返回值照片名稱，或是利用base64進行解碼，解出照片圖。   

### 總共分為三種  
* exec  
原型：
```
string exec ( string command [, array &output [, int &return_var]] )  
```
描述：返回值儲存最後的輸出結果，而所有輸出結果將會儲存到$output陣列，$return_var用來儲存命令執行的狀態碼（用來檢測成功或失敗）。  
例子：
```
$ret = exec("python test.py", $output, $var);   
```
注意：輸出結果會逐行追加到$output中，因此在呼叫exec之前需要unset($output)，特別是迴圈呼叫的時候。  
* system
原型：
```
string system ( string command [, int &return_var] )   
```
描述：執行給定的命令，返回最後的輸出結果；第二個引數是可選的，用來得到命令執行後的狀態碼。  
例子：
```
$ret = system("ls -al", $var);  
```
* passthru  
原型：
```
void passthru (string command [, int return_var])  
```
描述：執行給定的命令，但不返回任何輸出結果，而是直接輸出到顯示裝置上；第二個引數可選，用來得到命令執行後的狀態碼。  
例子：
```
passthru("ls -al", $var);  
```
