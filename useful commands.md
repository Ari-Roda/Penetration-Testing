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
