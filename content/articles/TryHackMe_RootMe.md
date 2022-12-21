---
title: "TryHackMe: RootMe"
date: 2022-12-16T14:01:10-08:00
draft: fasle
---

![](https://miro.medium.com/max/1400/1*dwjTlOhlmeorJ0TLUNuOAA.png)

### This is a writeup of the TryHackMe Capture The Flag Room: RootMe. 
#### RootMe is a hosted website with some vulnerabilities. In this write up, I will include my steps and thought process. 

---------------------------------------------------------------------------------------------

### STEP 1: We deployed the machine on TryHackMe and were provided an IP Address 
My initial thought was “Okay, why would they give me an IP address? Clearly, it serves  some sort of purpose.”
My next step was to think about what  I could do with this IP address in order to get more information.

### STEP 2: Reconnaissance 
In this step, I decided that in order to get more information I needed to use an NMAP scan to identify any open ports, as well as the software they were using. 
I ran in my command line the following nmap scan:
- sudo nmap -sCV -O -vvv IP_Address -oA filename
- Sudo – superuser do 
- -sCV – Performs script scanning using the default set of scripts - extra info + performs version detection 
- -O – Performs OS detection.
- -v – Specify the verbosity. The more v's in the command the more verbose nmap will be.
- -oA – Outputs the Nmap scan

Once my nmap scan was finished, I received the following information:
- The software version was Apache 2.4.29
- 2 ports on the machine were open
	- Port 80 HTTP
	- Port 22 SSH

Through the nmap scan, we can see that the box has a web server running on port 80, which normally indicates that the machine is hosting a website.

### STEP 3: What do I do with this information?
Knowing that I have a website open on port 80, I decided to run gobuster which is “a brute-force scanner tool to enumerate directories and files of websites”
The following is the command I used: 
- gobuster dir -u http:// "IP" -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt

This command gave me the following information:
- /uploads 
- /css
- /js 
- /panel
- server/status 

The information above is essentially a path we can get to by simply adding it to the end of the web address. In this case, the following web address was:
- http://“IP Address/uploads”
- http://“IP Address/css”
- http://“IP Address/js”
- http://“IP Address/panel”
- http://“IP Address/server-status”

Once going through each of these, I realized that on http://“IP Address/panel” I could upload a document.
My first thought was “Alright, I can probably put in a malicious file,” so I did some research online and found a reverse shell payload by pentestmonkey. I downloaded the file,edited it to my specifications (port and ip) and attempted to upload it. 
Unfortunately, it did not work because the extension was a php file, so I decided to try a different extension (php5) which ended up working.

### Step 4: Shell
Once the file was uploaded,I had to set up my netcat listener on the specification I edited earlier.
- nc -lvnp 4444

In order for my netcat to pick up the connection, the document needs to be executed. So, while searching through the web address I found http://“IP Address/uploads” which had my php upload. I clicked on it –  and Boom!– I had the connection.
 We have now gained a shell but it is an unstable shell. In order to stabilize the shell, I ran the following commands:
- $ python -c ‘import pty;pty.spawn(“/bin/bash”)’
- Ctrl+Z
- stty raw -echo
- fg
- export TERM=xterm

Now that the shell was stable, I had to find a flag. I wanted to make it simple for myself, so instead of searching through every directory, I used the following command to find user.txt: 
- Find / -type f -name user.txt

This command gave me the directory for where user.txt was and I was able to change directories and cat the file.

### Step 5: Privilege Escalation
Just like in the prior example, I did not want to search through everything one by one so in order to check for SUID files on our system, I ran this simple command: 
- find / -perm -u=s -type f 2>/dev/null

A list of directories came up and I started looking for something I considered to be strange. I saw that there was something with python: 
- /usr/bin/python 

My first thought was to go to https://gtfobins.github.io/ and look for possible privilege escalation commands for elevating the privileges.
In there, I found the following command: 
- python -c ‘import os; os.execl(“/bin/sh”, “sh”, “-p”)’

After putting in that command: it worked.
To double check that it worked,I ran whoami and the output was root 
In order to finish the box, I needed to find root.txt 
Ran the command ls, then changed directory to root then ran the cat root.txt command and got the final flag.


