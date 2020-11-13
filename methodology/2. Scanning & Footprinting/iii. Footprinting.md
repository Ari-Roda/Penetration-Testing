
once we have the list of active hosts from scanning we want to know more about services, OS's and other information about these hosts. the goal of this phase is to get a table of ip's with related OS and other information including confidence of that the OS is correct.

nmap can be used for OS fingerprinting:

nmap -Pn -O <ip's> : -O os fingerprintging, this can be done more or less aggressively with --ossccan-guess/--osscan-limit, -Pn no ping, windows wont always respong to pings or other systems can be configured to not respond so this can be used to treat host as online.

nmap -sT -O <ip range> :tcp connect scan
  
nmap can guess upto though service pack version even 

once you have access to the machine a uname -a can be used to check if the OS guess is correct



