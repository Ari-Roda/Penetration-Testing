Commands/tools used frequently

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

# Web-Server

```Python -m SimpleHTTPServer 80``` : Spins up a webserver in the directory you are located on port 80.

```Python3 -m http.server 80``` : Spins up a python version 3.X web server in the directory you are located on port 80.

```Python -m pyftpdlib -p 21 -w``` : Spins up a FTP server in the directory you are located on port 21 and it allows anonymous login access.

```Python3 -m pyftpdlib -p 21 -w``` : Spins up a Python 3.X FTP server in the directory you are located on port 21 and it allows anonymous login access.

# Wfuzz
Web application bruteforcer it can be used for finding resources not linked directories, servlets, scripts, etc, bruteforce GET and POST parameters for checking different kind of injections

```wfuzz -c -z file,/usr/share/wordlists/dirb/big.txt --hc 404 http://192.168.1.1/FUZZ/ > output.txt``` -c Shows the output in color, -z Specifies what will replace FUZZ in the request. For example -z file,big.txt will read through all the lines of big.txt and replace FUZZ with, --hc Don't show certain http response codes

sudo apt-get install wfuzz

pip3 install wfuzz

