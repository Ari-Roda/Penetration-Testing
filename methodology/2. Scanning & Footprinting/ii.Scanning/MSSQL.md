```sudo nmap -sV -Pn -vv -p 1433 --script='(ms-sql*) and not (brute or broadcast or dos or external or fuzzer)' --script-args=unsafe=1 IP```
