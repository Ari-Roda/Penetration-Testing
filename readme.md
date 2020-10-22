# General Advice/Recommendations
These are points which I thought were useful which have been taken from various blogs and articles listed in the OSCP-resources file under Blogs.

- Offensive Security has restricted the following tools: Commercial tools or services (Metasploit Pro, Burp Pro, etc.), Automatic exploitation tools (e.g. db_autopwn, browser_autopwn, SQLmap, SQLninja etc.), Mass vulnerability scanners (e.g. Nessus, NeXpose, OpenVAS, Canvas, Core Impact, SAINT, etc.), Features in other tools that utilize either forbidden or restricted exam limitations

- Everything in a box is there for a reason. Enumerate everything available to you, and have a plan for how you're going to do that with tools set up before you go into the exam. Note everything you find down, even if it doesn't seem like anything. That tiny thing might be.

- If all you're doing for notes is pasting in creds and random things you find, you're going to have a really hard time reconstructing that for the report. Take the extra time when you finish a box to write down your steps and what you did, in order. It'll save you time later

- Time management is the hardest part of OSCP. Beware of rabbit holes. Take regular breaks, even if you don't think you need them. Physically walk away from the computer and take stock. Are you doing what you're supposed to? Are you missing something?

- TAKE SCREENSHOTS OF EVERYTHING. Do it more than once. Do it even if you don't think you need to. Nothing worse than not getting points you should have because you failed to get proof. It’s required during the labs and exam to have a lot of screenshot so you need a good one. Ubuntu 18.04 still have Shutter[link] in it’s official repositories which doesn’t exist in Kali’s. Shutter is able to automatically save the screenshot as a file and copy it to clipboard. Just set a keyboard shortcut for shutter -s and have fun with it.

- You will spend a lot of time on terminal, have a good terminal application. (tmux|terminator) Tmux has a handful set of plugins here. Tmux settings can be changed by modifying ~/.tmux.conf file.

- As a general rule, you can use /usr/share/wordlists/rockyou.txt file to decrypt/crack hashes you found on the lab machines and you will be most likely successful with rockyou if the hash you found is supposed to be cracked. You can use johntheripper or hashcat for password cracking Only other wordlists you will need are on Seclists which I gave link on resources section. You will mostly never need to brute force any user login page during your PWK but never forget to try default user/passwords like admin/admin admin/password. I have taken extensive notes and screenshots during my lab time and I highly suggest it to everyone. My note structure was as following: You should have recon, proof, loot, priv esc sub-sections for each host on both labs and exam. I highly suggest you to read full results from recon tools before trying to hack any machine. This way you will have an overview of the machine and services on it which will be helpful while you are trying to hack the machine. Don’t forget you may need to chain 2 or more vulnerability and/or service to exploit a machine. This method does apply to priv esc tool results.

- Used autorecon for each host that I had access to. I also did a full nmap scan of student network on a few overnights. When I was finished with the PDF, I had enough information about the machines on student network. First I checked the nmap output for an overview and started to hack machines. Note that, you shouldn’t work on machines by IP order but try to figure out low hanging fruits. Figuring out the low hanging fruits is an important pentesting skill, so do it on your own but not by asking to others on any community channel.

- Exploit-db is the most important resource for finding exploits. You can use it’s web interface or use searchsploit command line tool on Kali.

