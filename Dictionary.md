

<b>Staging/Stager</b> : The stager is responsible for downloading a large payload (the stage), injecting it into memory, and passing execution to it. Essentially sending stager to machine which can then download files from a malicious server in stages to bypass size restrictions, AV and is more flexible since can be used to download various types of malware. Staging first came about out of necessity. Many exploitable situations constrain how many bytes an attacker may load, unchanged, into one contiguous location in memory. One way to do interesting post exploitation in these situations is to deliver the payload in stages. Staging makes it possible to deliver a variety of payloads with just a few stagers. So long as I have code that is compatible with a stager, I may deliver my code with all the exploits the stager supports (again, size is a constraint).
https://blog.cobaltstrike.com/2013/06/28/staged-payloads-what-pen-testers-should-know/#:~:text=The%20stager%20is%20responsible%20for,one%20contiguous%20location%20in%20memory.

<b>Downloader</b> : A "downloader" downloads a second stage (usually some kind of malware) which requires a network connection.

<b>Dropper</b> : A dropper means the malware drops something on the system that wasn't there before (like an executable). Often this is embedded in the original file but could also be downloaded.

<b>proof of concept (PoC)</b> : evidence, typically derived from an experiment or pilot project, which demonstrates that a design concept, business proposal, etc., is feasible.

<b>shell code</b> : quite literally is code that will open up a shell

<b>shell code</b> : quite literally is code that will open up a shell

###########################################################################
These methods hide the payload from the victim and from researchers that get their hands on the file.

<b>Packers</b> : This usually is short for “runtime packers” which are also known as “self-extracting archives”. Software that unpacks itself in memory when the “packed file” is executed. Sometimes this technique is also called “executable compression”. This type of compression was invented to make files smaller. So users wouldn’t have to unpack them manually before they could be executed. But given the current size of portable media and internet speeds, the need for smaller files is not that urgent anymore. So when you see some packers being used nowadays, it is almost always for malicious purposes. In essence to make reverse engineering more difficult, with the added benefit of a smaller footprint on the infected machine.

<b>Crypters</b> : The crudest technique for crypters is usually called obfuscation. Obfuscation is also used often in scripts, like javascripts and vbscripts. But most of the time these are not very hard to bypass or de-obfuscate. More complex methods use actual encryption. Most crypters do not only encrypt the file, but the crypter software offers the user many other options to make the hidden executable as hard to detect by security vendors as possible The same is true for some packers. FUD (Fully Undetectable) which is the ultimate goal for malware authors, going undetected by any security vendor. But if they can go undetected for a while and then easily change their files again once they are detected, they will settle for that.

<b>Protectors</b> : A protector in this context is software that is intended to prevent tampering and reverse engineering of programs. The methods used can, and usually will, include both packing and encrypting. That combination plus some added features makes what is usually referred to as a protector. So a researcher will be faced with protective layers around the payload, making reverse engineering difficult.

A completely different approach, which also falls under the umbrella of protectors, is code virtualization, which uses a customized and different virtual instruction set every time you use it to protect your application. Of these protectors there are professional versions that are used in the gaming industry against piracy. But the technique itself has also made its way into malware, more specifically ransomware. Which enables ransomware that doesn’t need a C&C server to communicate the encryption key. The protection is so efficient that the encryption key can be hardcoded into the ransomware. An example is Locky Bart that uses WProtect, an open-source code-virtualization project.

###########################################################################

<b>Reverse shells</b> are when the target is forced to execute code that connects back to your computer. On your own computer you would use one of the tools mentioned in the previous task to set up a listener which would be used to receive the connection. Reverse shells are a good way to bypass firewall rules that may prevent you from connecting to arbitrary ports on the target; however, the drawback is that, when receiving a shell from a machine across the internet, you would need to configure your own network to accept the shell. This, however, will not be a problem on the TryHackMe network due to the method by which we connect into the network.

<b>Bind shells</b> are when the code executed on the target is used to start a listener attached to a shell directly on the target. This would then be opened up to the internet, meaning you can connect to the port that the code has opened and obtain remote code execution that way. This has the advantage of not requiring any configuration on your own network, but may be prevented by firewalls protecting the target.

<b>Interactive shell</b> : If you've used Powershell, Bash, Zsh, sh, or any other standard CLI environment then you will be used to
interactive shells. These allow you to interact with programs after executing them. 

<b>Non-Interactive shells</b> don't give you that luxury. In a non-interactive shell you are limited to using programs which do not require user interaction in order to run properly. Unfortunately, the majority of simple reverse and bind shells are non-interactive, which can make further exploitation trickier.

############################################################################
DLL Attacks

Many times the functionality of the operating system itself can be used to the malware author's advantage as well. One such functionality within Windows Operating Systems is the side-by-side (WinSXS) feature. WinSXS is a directory on modern Windows Operating Systems, first introduced in Windows 98 SE, that can contain multiple DLL and file versions. It was introduced as a way to reduce dependency issues as well as problems with duplicate DLL files. If, for example, a new software is installed that uses an updated version of a DLL that currently exists on the host, the new version will be added and the old will remain. This reduces conflicts such as deleting the old version that may still be in use by another software component. This feature is a necessity in regards to the operation of the host but malware authors can also utilize it to hijack the flow of an application to ensure that their malicious code is executed.

<b>DLL Hijacking</b> : DLL highjacking takes advantage of the load order of legitimate DLLs by placing a spoofed version in a higher load position than the real DLL. And/Or DLL hijacking vulnerabilities happen when a program attempts to load a DLL from a location and can’t find it. For Example, the fax service can’t find the ualapi DLL when it tries to load it. The fax service runs as SYSTEM, so any code executed from the DLL will run in an elevated context. However, we need to write to the privileged folder C:\Windows\System32 to hijack the DLL. 

<b>DLL Sideloading</b> : DLL side loading, however, makes use of the WinSxS directory (C:\Windows\WinSxS). This directory holds multiple versions of DLL files and as stated earlier, resolves many issues that previous incarnations of Windows encountered. An application using this directory to retrieve a DLL will need to have a manifest. The manifest lists the DLL file that the program needs to load at runtime execution and is used by the DLL loader to determine which version should be used. A malicious DLL with a spoofed name could be placed in this location due to the lack of verifications that are performed on files in this folder. As a result, a vulnerability similar to the one that allows DLL hijacking exists in the side-by-side feature. Once an application on the host requests access of the legitimate DLL, the spoofed library is loaded. As I mentioned earlier, this has been observed in APT malware like PlugX.
