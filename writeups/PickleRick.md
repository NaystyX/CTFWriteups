# Pickle Rick

https://tryhackme.com/room/picklerick

The task is to exploit web server to find ingredients for Rick to turn back to human.

## Tasks

As always I start with ```nmap``` to check for open ports

<img width="359" height="144" alt="nmap" src="https://github.com/user-attachments/assets/75ef3e30-d30a-4acf-90c1-c49c32ae3f59" />

So it seems that ssh and http ports are open, so I went to see what shows in the html page. There is text from Rick to Morty.

```I need you to *BURRRP*....Morty, logon to my computer and find the last three secret ingredients to finish my pickle-reverse potion. The only problem is, I have no idea what the *BURRRRRRRRP*, password was! Help Morty, Help!```

So it seems I need to figure out username and password for Rick's account. Next I figured to go watch page source for info, there I found this
```
Note to self, remember username!

Username: R1ckRul3s
```

So now I have the username, now I just need password for it. First I thought of running gobuster to find if there are any other pages on the web server.

<img width="359" height="144" alt="gobuster" src="https://github.com/user-attachments/assets/9de11137-b52f-4635-83da-46d3f648b9b5" />

So we find ```/assets``` were we find different files.

<img width="359" height="144" alt="assets" src="https://github.com/user-attachments/assets/a8fa141c-7eb2-422a-9f99-9914d2343581" />

Last thing I checked was ```/robots.txt``` were I found this ```Wubbalubbadubdub``` possibly useful.

I decided to try the different assets as directories ```/fail /picklerick /portal /rickandmorty```. I found a login page at ```/portal.php```

There I had username and password, I decided to try Username: R1ckRul3s and password: Wubbalubbadubdub and success.

<img width="359" height="144" alt="CommandPanel" src="https://github.com/user-attachments/assets/54f12dc0-a7bb-4e5d-8697-1413bf6708f3" />

So now I have a command panel where I can execute commands. Using ```ls``` we find the first ingredient ```Sup3rS3cretPickl3Ingred.txt```.

Trying to cat that file gives ```Command Disabled``` return, so I have to get another way to read it. I tried ```less``` to read it and success I got the first ingredient.

<img width="359" height="144" alt="image" src="https://github.com/user-attachments/assets/22270c55-9eed-4947-bb6f-55b22f273673" />

Doing ```sudo -l``` to find out my sudo privileges and we find that I can run sudo commands freely. 

Looking at all the folders with ```sudo ls``` I found ```/root/3rd.txt``` which I read with sudo. Now I need to find the second one.

After looking around for the last flag I found ```/home/rick/``` folder where was ```second ingredients``` and read it with less.


## Conlusion

This was quite an easy machine to break most of the time went to find the flag files themselves. Still a good practice
