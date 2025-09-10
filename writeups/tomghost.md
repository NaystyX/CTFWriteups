# Tomghost

https://tryhackme.com/room/tomghost

## Tasks

I started the task by running a ```nmap``` to try to figure out vulnerable ports that could give me access to the files

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/068aaeb7-bd4c-4c5c-b328-027805e26ef8" />


Seeing 4 open ports, ```22 ssh```, ```53 tcpwrapped```, ```8009 ajp13```, ```8080 http```

As I had never heard of tcpwrapped or ajp13 I decided to go google and try to find out if they had vulnerabilities.

Looking at secwiki.org I found that when nmap shows this result that port is protected by a tcpwrapper so a TCP handshake happened but host closed the connection without receiving data.

Looking at ajp13 I found a possible exploit in exploit-db, using msfconsole I used tomcat_ghostcat exploit and got a username:password ```skyfuck:8730281lkjlkjdqlksalks```. Using ssh I got logged in.

When logged in I tried to find files I could open and went to ```/merlin/``` and found user.txt and got the first flag. 

Now I just need to try to escalate my priviledges to get the root flag. in ```/skyfuck``` I found tho files I got them to my computer with ```scp skyfuck@10.10.154.122:/home/skyfuck/* .``` I got credential.pgp file and tryhackme.asc. Getting the hash with gpg2john from tryhackme.asc and then running johntheripper got the key from the hash ```alexandru```

<img style="max-width:100%; height:auto;" alt="image-1" src="https://github.com/user-attachments/assets/04d0c0fb-36db-49d1-9710-f5207ea35750" />

Now I just need to use this secret key to get the other credentials. 

<img style="max-width:100%; height:auto;" alt="image-2" src="https://github.com/user-attachments/assets/f6a40864-2ee6-4722-980c-65476d885fcd" />

Now using the decrypted key I got merlins username:password ```merlin:asuyusdoiuqoilkda312j31k2j123j1g23g12k3g12kj3gk12jg3k12j3kj123j```

<img style="max-width:100%; height:auto;" alt="image-3" src="https://github.com/user-attachments/assets/3254254f-e907-4522-88ab-8b7a030996eb" />

After running ```sudo -l``` I can see commands I can run as root with nopasswd and find ```zip``` looking at GTFOBins I find myself an priviledge escalation I can use to get root.

I find an exploit 
```
TF=$(mktemp -u)
sudo zip $TF /etc/hosts -T -TT 'sh #'
sudo rm $TF
```

and running it gives me root access. Going to ```/root/``` I find the flag.

<img style="max-width:100%; height:auto;" alt="image-4" src="https://github.com/user-attachments/assets/94236d50-241f-4441-9c45-7607de5dffa1" />

# Conclusion

Got to use msfconsole again and train it's use,  this task was on the easier side but still required some background check to find the vulnerabilities.
