1. Before Scanning check your connected to and have access to the networks you should have access to. This includes checking if you have an ip on the same network as your connected to. Check your routing table to identify you have access to the networks you should. someimtes you will know what networks you should be able to access other types you wont but its better to confirm you can access a network before beginning scanning since if your scanning multiple subnets and the results return nothing for particular subnet because you dont have access but there is actually important targets there this is a problem. AttackerKB site also has information about possible vulnerabilities.

```route```: check what routes you have before connecting to network

```ip a``` : to check you have interface connected to network

```route``` : to find what new network you are connected to and what network you should scan

```ip route ``` : check if you have a route to the networks you are connected to. if not add one.

```nmap -sn <ip subnet: eg: 192.168.0.1/24>``` : This finds the targets on your network — VERY fast but doesn’t scan any ports — just finds hosts on the network

```ip route add 192.168.222.0/24 via 10.175.34.1``` : If you need to reach a server but you cannot and you dont have a route to it you can add the route with
