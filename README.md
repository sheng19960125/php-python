## 在php中調用python  
### 總共分為三種  
* exec  
原型：string exec ( string command [, array &output [, int &return_var]] )  
描述：返回值儲存最後的輸出結果，而所有輸出結果將會儲存到$output陣列，$return_var用來儲存命令執行的狀態碼（用來檢測成功或失敗）。  
例子：$ret = exec("python test.py", $output, $var);   
注意：輸出結果會逐行追加到$output中，因此在呼叫exec之前需要unset($output)，特別是迴圈呼叫的時候。  
* system
原型：string system ( string command [, int &return_var] )   
描述：執行給定的命令，返回最後的輸出結果；第二個引數是可選的，用來得到命令執行後的狀態碼。  
例子：$ret = system("ls -al", $var);  
* passthru  
原型：void passthru (string command [, int return_var])  
描述：執行給定的命令，但不返回任何輸出結果，而是直接輸出到顯示裝置上；第二個引數可選，用來得到命令執行後的狀態碼。  
例子：passthru("ls -al", $var);  
