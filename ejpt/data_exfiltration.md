Data exfiltration lab
_____________________________________________________________________________________________________________________________________________
Find useable outbound ports
_______________________________________________________________________________________________

Find out how to get data off the target machine. Data exfiltration can be straight forward in CTF's sometimes but can be made more difficult if outbound ports on machine are blocked and/or you dont want to be detected when exfilling data.
To find ports that may be possible to be used for exfil, we can:

1. Setup python http server on our machine using differen ports and try to connect to it. If can access shows outbound access to that port is available.

2. To just check if outbound dns is available, set dns server on victim machine to your machine and look at wireshark to see if you get dns packetrs from victim.

3. Can check firewall settings through GUI to see open and blocked ports.

4.egresscheck framework can be used to generate a oneliner or PE to run on victim that will test outbound access to a range of ports on your machine. Can then check wireshark to see if 
any got through. (Could do this with nc or nmap also if know how)

_______________________________________________________________________________________________
Stealth data exfil
_______________________________________________________________________________________________

if you want to exfil data stealth, you can use packetwhisper. It uses dns (port 53) and splits and cloaks destination filenames. You can then read data with wireshark and save pcap and decloak data also with packetwhisper. 
