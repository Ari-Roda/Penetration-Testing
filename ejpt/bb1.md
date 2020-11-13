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

from webshell use uname -a and others to determine which payload to use for reverse shell.

use webshell to get reverse shell, can use msfvenom, oneliner, downloading it with wget, netcat, socat etc

make listener. for the listener port can use a high port being used by the target to help with firewall bypass.c

if you download file with wget will need to remove extension if one was added make it executable chmod +x <file>. then run reverse shell script
  
#####################################################################################################################################

2.

use gobuster to find available 

at logins and dashbaords try common credentials first (admin:admin, admin:password etc). then try credentials list with hydra etc dictionary attack.

if you want to continue enumerating a path that has authorization you can do it with dirb/gobuster but need to add the  credentials to the command. eg.
gobuster dir -u http://172.16.64.140/project/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -U admin -P admin

as you continue finding new paths you should continue enumerating to find new directories and files. if you find information such as file paths or credentials these can be used. if the file path is /var/www/html/... it can be accessed so try that.

#####################################################################################################################################

3.

you can find creds on other machine such as ssh



#####################################################################################################################################

4.

you can find creds on another machine which will give access to another machine or service on the machine. 

for mysql there are various ways to login to mysql services remotely. myssql_login metasplot module is one way but can be done manually, then mssql_enum and mssql_payload to get access. when setting ports for the payload consider what ports can have outbound access like dns and others and also the destination address of the listener.

