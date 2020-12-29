
once we have the list of active hosts from scanning we want to know more about services, OS's and other information about these hosts. the goal of this phase is to get a table of ip's with related OS and other information including confidence of that the OS is correct.

nmap can be used for OS fingerprinting:

```nmap -Pn -O <ip's>``` : -O os fingerprintging, this can be done more or less aggressively with --ossccan-guess/--osscan-limit, -Pn no ping, windows wont always respong to pings or other systems can be configured to not respond so this can be used to treat host as online.

```nmap -sT -O <ip range>``` :tcp connect scan
  
nmap can guess upto though service pack version even 

once you have access to the machine a uname -a can be used to check if the OS guess is correct


footprinting web servers is useful since it is one of the most public facing devices. Httprint tool can be used for this.

```httprint -P0 -h <target host> -s <signature file> ```: -P0 no pings

one of the first things to do for web servers is to check what http verbs it allows. using the options verb you can find if it allows PUT or DELETE which may be able to be exploited.

exploiting PUT may allow you to get a reverse shell by putting a PE on the target byt the PUT verb requires you to know the size of the file which can be done with linux command  ```wc -m <file>```

```sudo nmap -sV -n -v -Pn -p- -T4 -iL black-box-2-ips.txt -o black-box2-details-2.txt```

