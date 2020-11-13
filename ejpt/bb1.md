sudo nmap -sn <ip> -oN <outfile> : scan for live hosts

nmap -sV -n -v -Pn -p- -T4 -iL ips.txt -A --open

Use nmap with the following options:

-sV for version identification

-n for disabling reverse DNS lookup

-v for Verbose

-Pn to assume the host is alive

-p- to scan all the ports

-T4 to speed things up

-iL to use a list of IPs as input (ips.txt)

--open to see just open ports and not closed / filtered ones

-A for detailed information and running some scripts

#####################################################################################################################################
1.

multiple tomcat services. can find tomcat default directory using gobuster/dirb or can research to find default directory including admin panel.

try default creds to login to admin panel. read error pages properly since can contain important information.

admin panels often allow for file upload, if they filter by file type/extension can either try renaming file to get it uploaded, or trying alternative file extensions for a file type. eg php can also use phtml or php3.
upload a webshell in this way. have to take into account the language being used by the site and what can be uploaded. tomcat can upload .war files therefore see if .war webshell exists allowing for easy upload.

access the webshell either through url or admin panel.

from webshell use uname -m and others to determine which payload to use for reverse shell.

use webshell to get reverse shell, can use msfvenom, oneliner, downloading it with wget, netcat, socat etc

make listener. for the listener port can use a high port being used by the target to help with firewall bypass.c

if you download file with wget will need to remove extension if one was added make it executable chmod +x <file>. then run reverse shell script
  
