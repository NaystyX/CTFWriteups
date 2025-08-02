# Bounty Hacker

https://tryhackme.com/room/cowboyhacker

## Tasks

As with all machines I start with ```nmap``` to find open ports which is the first task. 

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/8e5cc2a8-8039-4413-a934-6345c09301c1" />

We find three ports open and anonymous login allowed to ftp. I also ran gobuster but that didn't help me much

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/04a23af9-5e14-465e-9369-d1bdb5072d0a" />

Using FTP I find two files, ```locks.txt, task.txt```

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/4fceb975-2429-4d9c-84c6-48462971d547" />

Since the question was who wrote task list I view it and find ```lin```, now that I have a username I could try ssh bruteforce with the locks.txt which seemed to have passwords.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/7f429e91-e5c5-4beb-b49a-72f734f6b5e6" />

So now I got a password time to try it and success.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0505d760-6162-4152-b43a-ee38fa71aa9c" />

From here I find the user.txt flag, now I jsut need root access. From what I previously have learned I decided to do ```sudo -l``` to find what access I have.

<img style="max-width:100%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/c8b97b0c-0245-47f4-be06-42a31fa1743c" />

After finding this I looked up tar in GTFOBins and found ```sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh``` and running it gave me root access.

Then I just headed to ```/root/``` to find the last flag.


## Conclusion

This challenge was fairly easy but it shows me that I am slowly starting to remember the steps what to do and how to give myself root access etc. So very important still
