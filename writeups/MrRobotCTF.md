# Mr Robot CTF

https://tryhackme.com/room/mrrobot

## Tasks

In this CTF I have 3 keys I need to find, so I will begin as always with ```nmap```

<img width="360" height="150" alt="image" src="https://github.com/user-attachments/assets/31f5fefa-2e74-4756-904d-d59baea8b336" />

Going to the https page opens a cmd where you can type but first I wanna know anything the program would try to hide.

For that I will do ```gobuster``` and check ```/robots.txt```. From robots.txt I find ```key-1-of-3.txt``` so I go there and see first key... that was easy.

While my gobuster is doing it's thing I tried the cmd and it told me to use ```help```

<img width="360" height="150" alt="image" src="https://github.com/user-attachments/assets/230e9be4-ee96-4dec-886b-6df123163ae7" />

Running these commands take us to different pages of videos and pictures

<img width="600" height="325" alt="image" src="https://github.com/user-attachments/assets/5099bfd9-ee3a-459e-82a9-6a50816a86d5" />
<img width="600" height="399" alt="image" src="https://github.com/user-attachments/assets/614f5f4c-38cf-4ad5-b80d-5ccbaadedab8" />
<img width="600" height="361" alt="image" src="https://github.com/user-attachments/assets/7afed7d5-ca31-4b6c-9ba8-239c6fd7624a" />
<img width="600" height="321" alt="image" src="https://github.com/user-attachments/assets/e3c1cb20-283e-4e2f-aa5d-a4d0af30b986" />

These aren't probably important just propaganda from the ```"fsociety"``` but after running ```join``` I get greeted by mr. robot.

<img width="600" height="248" alt="image" src="https://github.com/user-attachments/assets/b6c306e3-a7a5-4f95-987b-3831f4784bcc" />

Tho after giving my fake email it just put me back to the start. Although my gobuster wasn't finished yet I saw ```wp-admin``` and ```wp-login``` there so I knew it was a wordpress page and went to login page

<img width="200" height="360" alt="image" src="https://github.com/user-attachments/assets/524548fb-61e5-4226-93b5-4261dbcb0309" />

Doing a robots.txt I found another page ```fsociety.dic``` which I had downloaded incase I need it, so that I can use it with hydra.

<img width="400" height="200" alt="image" src="https://github.com/user-attachments/assets/0bdc7e11-01d8-45e6-a1f1-babe57b5775b" />

So I found a user ```Elliot```, lets try to hydra it's password with the same dictionary and get ```ER28-0652```

<img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/f711ccef-f59f-460e-bd9a-4ed9292f412c" />

I went around the tabs and found Editor where I can change different pages, so I can put a reverse shell there.

I updated the 404 Template and put a ```netcat``` to listen to port 4444, after going to 404.php page I got access to shell

I found the key2 but I cannot cat it, so I checked password.raw-md5 and got ```robot:c3fcd3d76192e4007dfb496cca67e13b```

<img width="350" height="46" alt="image" src="https://github.com/user-attachments/assets/09327c97-9d19-4bb3-80dd-f50a80f9cb16" />

So now we can ```su robot``` and get the second flag.

After that I was a bit stuck so I looked at the hint and it said nmap, so I went to check GTFOBins for nmap.

<img width="600" height="361" alt="image" src="https://github.com/user-attachments/assets/20455b97-f7a5-4e89-8718-a3e0600f3d4f" />

So I ran ```nmap --interactive``` and in there ```!sh``` and I got root access, then I headed to ```/root/``` and found the last flag

## Conclusion

Definitely on the more difficult side for me, but also interesting, although I didn't get any references since it was based on a movie apparently. 
