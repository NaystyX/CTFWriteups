# Mustacchio

https://tryhackme.com/room/mustacchio

## Tasks

I started again with ```nmap``` to find which ports would be vulnerable.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/e514a10e-f289-41ca-91c5-739653715e3f" />

Going to http I found a website with some text and images so I decided to run gobuster

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/875c00ab-b4e4-46ee-b743-632561c24504" />

After looking at ```/custom``` I found a users.bak file 

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/fb4ae6b7-4756-4ce2-92e3-46b3a0e2e981" />

Which appeared to be a user database file with admin and password? ```admin1868e36a6d2b17d4c2745f1659433a54d4bc5f4b```

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/5e423231-f280-47c4-9115-570665675dab" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/fca0129c-d25f-4e27-93e3-6cc5709c8124" />

Running hashcat gave me the password for admin ```bulldog19```. I just needed to figure out where to put this so I ran nmap with more ports

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/8256d900-8c15-40fa-aed0-b018883a2be0" />

At port ```8765``` I found an admin panel

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/973f5cb7-3de1-427f-a5a4-8186706c1e46" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/6c5d9b41-0931-48df-9faf-0d90214608c1" />

I decided to open burpsuite and view what sending a comment does and it showed something about ```/auth/dontforget.bak```

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/ffd9e3be-34b7-4112-8a8a-148263ae3ada" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/c6304b5f-5902-47da-be29-09b93821d875" />

Seeing the file be xml I thought that it could have ```XML external entity (XXE) injection``` vulnerability

I made a injection payload and submitted it.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0a5fe6dd-0ef7-46e7-a25a-006e014b7477" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/b0b0d605-17bd-4c4a-b086-30619e11216e" />

Now I wanted to get barrys id_rsa file and I could do that by changing the request a bit.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/145c4a00-4ba7-42a0-aa6c-edb60c1757a5" />

Now I got the rsa now I just neet to use it to login

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/93daebbd-926f-4ea8-b61f-282e9f584530" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/daf21353-ad62-4552-837b-bf1a894d5088" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/51bd6fb2-d290-401a-b5b0-fe326b70206c" />

I started doing a priviledge escalation checklist and when doing ```find / -perm -u=s -type f 2>/dev/null``` I found ```/home/joe/live_log```

When viewing it I found this

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/25236aed-4a34-44e7-ad25-3bd91db06fff" />

Noticing that the command ```tail``` doesn't specify an absolute path, which opens it to vulnerability

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/aa9c71df-e728-4d56-b63f-f32958d2c136" />

So I decided to make a tail file and looked online what would be a good payload and found that version and after running ```./live_log``` I got root access and flag

# Conclusion

The hardest part was to find a way to get into the ssh but after that quite pleasable. Very good CTF in my opinion
