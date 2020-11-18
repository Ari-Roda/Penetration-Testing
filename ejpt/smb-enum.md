can use enum4linux from start or do manually by:

nmblookup -A <IP> : find out of file sharing service is running on target

smbclient -L //<IP> -N : find shares available

we can use enum4linux now to get more inforamtion on shares.

enum4linux -S <ip>

this can also be done with nmap

nmap -script=smb-enum-shares <IP>

can go deeper and run enum4linux -a IP or specific queries to get more information on users or password policies etc.
If looking for null session though can use the shares output to look for shares which arent denied

once found you can connect to the share with

smbclient -L //IP/sharename -N -U ""

nmap can enum users and also brute force shares with :

nmap -script=smb-enum-users <IP>

nmap -script=smb-brute <IP>
