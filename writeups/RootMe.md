# RootMe

https://tryhackme.com/room/rrootme

## Tasks

As for all machines I start with ```nmap``` to see the ports open

<img alt="image" src="https://github.com/user-attachments/assets/3d52709a-b770-43d2-a8e9-d60b70457697" />

So I can see 2 ports open, ssh and http

### Scan the machine, how many ports are open?

2

### What version of Apache is running? and What service is running on port 22?

Apache/2.4.29 and ssh

### Find directories on the web server using the GoBuster tool.

Now gonna run ```gobuster dir -u 10.10.201.109 -w /usr/share/wordlists/dirbuster/directory-list.2.3-small.txt```

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/8bb0ec69-3a83-4876-843e-b9c5779ff5cd" />

### What is the hidden directory?

From gobuster I can see the hidden directory ```/panel/```

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0a19b2bb-02c4-48aa-b271-e06e39ff85c4" />

Seems like I can upload files here

### Find a form to upload and get a reverse shell, and find the flag.

If I try to upload a ```php-reverse-shell.php``` it shows an error PHP not allowed. I got an idea to try different extension for php.

Changing the file to ```php-reverse-shell.php5``` allows it to upload

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/cc7c63a9-a9e2-4fcc-9199-0b40d2346bd4" />

Having the file in allows me to load it and having a netcat listen on my computer gives me access to the machine.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/d7d7c6c7-2bd0-4a09-9b22-5699208e92f6" />

Now we gotta find the user.txt flag somehow, using ```cat user.txt``` shows that no file found.

I googled around how to get more access and found that running ```Python pty module``` lets you run different things, so I ran ```python -c 'import pty; pty.spawn("/bin/bash")'```

Now I got more access I need to find the flag. I ran ```find . -name user.txt``` and found that it was in ```/var/www/``` where I found the flag.

### Now that we have a shell, let's escalate our privileges to root.

The task is ```Search for files with SUID permission, which file is weird?``` so I googled how I could do that and found ```find / -user root -perm / 4000 ```

I saw many normal files and then ```/usr/bin/python``` looked odd to me so I went to see GTFObins and found ```python -c 'import os; os.execl("/bin/sh", "sh", "-p")'```

After running that I got sudo priviledges and then going to ```/root/``` found the last flag.


## Conclusion

Quite easy except realizing that I could use ```.php5``` instead of the normal.
