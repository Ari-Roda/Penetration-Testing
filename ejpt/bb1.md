sudo nmap -sn <ip> -oN <outfile> : scan for live hosts

nmap -sV -n -v -Pn -p- -T4 -iL ips.txt -A --open

Use nmap with the following options:

-sV for version identification

-n for disabling reverse DNS lookup

-v for Verbose

-Pn to assume the host is alive

-p- to scan all the ports

-T4 to speed things up

-iL to use a list of IPs as input (ips.txt)

--open to see just open ports and not closed / filtered ones

-A for detailed information and running some scripts
