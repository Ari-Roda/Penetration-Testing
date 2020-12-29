```sudo nmap -sV -Pn -vv -p 3389 --script='(rdp*) and not (brute or broadcast or dos or external or fuzzer)' --script-args=unsafe=1 IP```
