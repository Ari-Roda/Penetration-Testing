nmap -sV -Pn -vv -p 25,110,143,587 --script='(smtp*) and not (brute or broadcast or dos or external or fuzzer)' --script-args=unsafe=1 IP
