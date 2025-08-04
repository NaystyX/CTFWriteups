# LazyAdmin

https://tryhackme.com/room/lazyadmin

## Tasks

Running ```nmap``` shows me that there are 2 ports open so I go visit the http site

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/cb8011f9-624c-41fe-8b78-a1b8849e3a58" />

In the HTTP I found apache2 ubuntu default page, so I decided to run gobuster to find other directories.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0f44dd62-8804-4d2b-bd43-fa2a6930a3ca" />

Running gobuster on ```/content/``` I found a login page on ```/as/```

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/c1bd3d23-e3dd-4e2c-9949-5da89ee4672b" />

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/4996d4be-377c-4231-abef-eb1d832074bb" />

I decided to go check exploit database for sweetrice and found multiple exploits

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/ed83fad3-fcf7-4251-9494-f74115a2c8b5" />

Reading the first one ```backup disclosure```

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/8c0e76dd-ffd5-4bd4-9ad0-0e61d723e5e7" />

After trying multiple urls I got ```http://10.10.80.159/content/inc/mysql_backup/``` working and found a sql file

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/a8eb36df-c2d6-4f7f-8b5e-677825967e26" />

Viewing the file I found ```42f749ade7f9e195bf475f37a44cafcb``` and using hash identifier identified it as MD5 hash

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/88fbfd90-378e-465b-9c59-91dc6f2c160b" />

Running a hashcat on it I got it cracked with rockyou.txt, now I just need the login. Which is in the same sql file as password ```manager```

After looking around for a while I found that I could upload a file in the ```Media Center``` so I decided to send a php-reverse-shell.php there

First I couldn't send the .php file so I used a previously used trick so I renamed it to .php5

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/76e1d872-7852-4393-a1c1-9e659bb3b9ec" />

As I have done before I ran ```python -c 'import pty; pty.spawn("/bin/bash")'``` to give me more access to commands

After going to ```/home/itguy/``` I found the user flag, now I need root access.

Doing ```sudo -l``` I saw I can run ```/usr/bin/perl /home/itguy/backup.pl``` without password

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/b71dcfd8-0ccc-421c-95fb-a68cfed9358e" />

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/e1bc68a3-f1fc-46b4-bd73-d31b6d2ce647" />

Looking at the file I could run I noticed it ran another file ```copy.sh``` which had a reverse shell, so I changed the reverse shell to my ip so I could get root access.

After running the file I got the access and now I was root, after that I found the root flag

# Conclusion

This was an intresting one, I got to use previously known knowledge and had to also learn new ones like the ```SweetRice``` exploit. Also good training for reverse shelling.
