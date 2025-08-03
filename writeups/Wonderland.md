# Wonderland

https://tryhackme.com/room/wonderland

## Tasks

First I start with ```nmap``` as always to find what ports are in use

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/28d36a45-4a4d-432a-9e78-71494af8a884" />

Also running a ```gobuster``` on the http server.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/bcf9efa1-ceb8-43de-8812-9632a89cb8a8" />

After reading ```Follow the white rabbit``` and seing the first directory be ```/r/```, I thought of trying ```/a``` and so on and got to ```/r/a/b/b/i/t/```

Going to view page source I saw ```alice:HowDothTheLittleCrocodileImproveHisShiningTail``` which could be ssh login.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/b8ca6fe1-62d7-467c-ba72-6593489520bb" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0046d002-a9c4-4e3c-b47c-61dbd2c70ffb" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0f489dd1-fe9b-49aa-91e8-b60cd5f6fbb4" />

I can run the ```walrus_and_the_carpenter.py``` but I cannot edit it. Also going to ```/root/``` folder I found the user.txt flag.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/6e92e127-73ff-49e1-a1ce-1942dc2c31a7" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/4078402a-83a5-4ae0-9d21-77d95fb34772" />

Viewing the walrus and the carpenter show it importing random which game me the idea to create random.py that would run in the walrus py file.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/fe60c7af-5ecc-48bb-a283-f0cef97cbbc2" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/c9c266a9-3d08-44c5-af48-05b91cd60b5b" />

And this game me the rabbit role.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/7f4ca5fc-2925-442d-ba0c-fa499ebaf454" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/0ef63e57-f294-4a08-90f2-04c82ade6ef4" />

Reading the file I see this

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/5cb7a8fc-2960-47e0-b9be-d46fe9dc7bc1" />

So I though of doing a file date

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/f734e51a-2c4b-4b2f-949a-ca968c8ea7fc" />

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/6ac640ca-e2cb-46e5-851e-7c26d4ec3a59" />

```Hatters password: WhyIsARavenLikeAWritingDesk?```

Then I decided to run ```LinPeas``` to find priviledge escalation types.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/39272c34-114d-4578-b08e-65d2808aaf9b" />

Searching in GTFOBins I found a match.

<img style="max-width:75%; height:auto;" alt="image" src="https://github.com/user-attachments/assets/34656c9b-551e-49aa-8e87-c85408d6d2d6" />

And escalating my priviledges I got the root access and found the last flag

<img style="max-width:75%; height:auto;" src="https://github.com/user-attachments/assets/cb77849e-68f3-4093-939d-f336d6602da7" />

# Conclusion

Definitely on the harder side but also familiar types that I used to crack the machine.
