# Simple CTF

https://tryhackme.com/room/easyctf

## Questions

### How many services are running under port 1000?

Im gonna just run basic ```nmap``` to figure out the services, I find 3 open ports ```21, 80 and 2222```. So under port 1000 we have 2 services.

<img width="359" height="144" alt="nmap" src="https://github.com/user-attachments/assets/a4cdd2cd-81e6-4843-af41-9b9965dac272" />

### What is running on the higher port?

From the nmap we see what is running on the port ```2222/tcp open ssh```

### What's the CVE you're using against the application?

Since this question didn't make sense to me at first I decided to run gobuster to find other pages in the web server.

<img width="359" height="144" alt="image" src="https://github.com/user-attachments/assets/1686d50c-b5d1-42be-873b-77d95de82757" />

Looking at ```/simple``` page we found that it was running using ```CMS Made Simple version 2.2.8``` and doing a CVE search I found ```CVE-2019-9053```

### To what kind of vulnerability is the application vulnerable?

This is a sql injection vulnerability.

### What's the password?

Getting the exploit from exploit database and it is for python2, so I translated it to python3 using chatgpt. Now I could run it.

I ran it using ```python 46635python3.py -u http://10.10.249.229/simple/ --crack -w /usr/share/wordlists/rockyou.txt```

<img width="359" height="144" alt="image" src="https://github.com/user-attachments/assets/978a2dde-abaa-4d5f-8400-945e5acc8b45" />


### Where can you login with the details obtained?

This is ssh

### What's the user flag?

Let's login with the ssh ```ssh mitch@10.10.249.229 -p 2222```

<img width="359" height="144" alt="image" src="https://github.com/user-attachments/assets/1fbac4b5-047f-4e56-bdb1-511420f218ef" />

### Is there any other user in the home directory? What's its name?

Going back with ```cd ..``` and we find another user ```sunbath```

### What can you leverage to spawn a privileged shell?

Let's do ```sudo -l``` to find what rights I have, then check that with GTFObins.

<img width="359" height="144" alt="image" src="https://github.com/user-attachments/assets/24dfae66-5aa1-4a88-8a52-39cda52fa89b" />

so I can use vim and running ```sudo vim -c ':!/bin/sh'``` gives me root access.

### What's the root flag?

Now that I have root access we can head to ```/root/``` folder where I find root.txt.

## Conclusion

This was quite fun CTF getting to use exploit database which I haven't used that much lately. Overall quite easy CTF as the name would suggest.
