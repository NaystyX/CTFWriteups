# Biohazard

https://tryhackme.com/room/biohazard

## Task 1 - Introduction

This task had just basic questions like how many ports open so I did a nmap

<img style="max-width:100%; height:auto;" alt="image-1" src="https://github.com/user-attachments/assets/4197f5c7-4cf6-48cb-9c9c-1dcbff223e14" />


## Task 2 - The Mansion

Visiting the http page showed me a page with the title ```The nightmare begins```

Nothing special here so I pressed the mansion link and went forward, I got into the main hall, I couldn't find anything here at first so I checked the page source.

There I found a hint ```/diningRoom/``` so I went there and there was a link to emblem and from there I got the flag ```emblem{fec832623ea498e20bf4fe1821d58727}```

It also told me to put it to refresh diningRoom but putting the flag in the input gave a text ```nothing happened```

Again since I had nothing to work with I checked the page source and found ```SG93IGFib3V0IHRoZSAvdGVhUm9vbS8=``` which seemed to be base64 encrypt so I put it to cyberchef and got ```How about the /teaRoom/```

Going to the teaRoom I found ```lock_pick{037b35e2ff90916a9abf99129c8e1837}``` and also the next hint to visit /artRoom/

Going to the artRoom I found the mansion map

```
Look like a map

Location:
/diningRoom/
/teaRoom/
/artRoom/
/barRoom/
/diningRoom2F/
/tigerStatusRoom/
/galleryRoom/
/studyRoom/
/armorRoom/
/attic/
```

So I decided to start going through the rooms in order first with /barRoom/, there I could put the lock pick key in the input and got inside, there was another input and a READ link which had a string inside ```NV2XG2LDL5ZWQZLFOR5TGNRSMQ3TEZDFMFTDMNLGGVRGIYZWGNSGCZLDMU3GCMLGGY3TMZL5```, which I again put to cyberchef and got ```music_sheet{362d72deaf65f5bdc63daece6a1f676e}```

Putting it in the input I got into a secret bar room which had a emblem slot, I got the gold emblem from there but it didn't fit to the input flag so I put the previous here which gave me a name ```rebecca```, and I decided to put this gold emblem to the first one and it gave me ```klfvg ks r wimgnd biz mpuiui ulg fiemok tqod. Xii jvmc tbkg ks tempgf tyi_hvgct_jljinf_kvc```, I googled this and found vigenere encoding and using the name rebecca as the key I got the text ```there is a shield key inside the dining room. The html page is called the_great_shield_key```, going there gave me ```shield_key{48a7a9227cd7eb89f0a062590798cbac}```

Now I visited the other rooms ```/diningRoom2F/```, nothing showed at first but viewing the page source showed ```Lbh trg gur oyhr trz ol chfuvat gur fgnghf gb gur ybjre sybbe. Gur trz vf ba gur qvavatEbbz svefg sybbe. Ivfvg fnccuver.ugzy``` which seemed to be some kind of cipher again, but wasn't the same, doing googling I found that it was ROT13 and I got the text ```You get the blue gem by pushing the status to the lower floor. The gem is on the diningRoom first floor. Visit sapphire.html```, there I got ```blue_jewel{e1d457e96cac640f863ec7bc475d48aa} ```

Now going to /tigerStatusRoom/ it had an input for gem flag so I put the blue jewel and got a long text

```
crest 1:
S0pXRkVVS0pKQkxIVVdTWUpFM0VTUlk9
Hint 1: Crest 1 has been encoded twice
Hint 2: Crest 1 contanis 14 letters
Note: You need to collect all 4 crests, combine and decode to reavel another path
The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it
```

I left that for now and went forward to /Gallery/ where I found

```
crest 2:
GVFWK5KHK5WTGTCILE4DKY3DNN4GQQRTM5AVCTKE
Hint 1: Crest 2 has been encoded twice
Hint 2: Crest 2 contanis 18 letters
```

Okay I might find them all quite easily, I went forward to /studyRoom/ which had a helmet symbol in it, I didn't have that tho so I continued forward

I got into /armorRoom/ which had the shield symbol flag after putting it I found another note

```
crest 3:
MDAxMTAxMTAgMDAxMTAwMTEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMTEgMDAxMDAwMDAgMDAxMTAxMDAgMDExMDAxMDAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAxMDAgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMDAgMDAxMTEwMDAgMDAxMDAwMDAgMDAxMTAxMTAgMDExMDAwMTEgMDAxMDAwMDAgMDAxMTAxMTEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAxMTAgMDAxMTAxMDAgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMTAgMDExMDAwMDEgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTAxMTEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAxMDEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMDAgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTEwMDAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMTAgMDAxMDAwMDAgMDAxMTAxMTAgMDAxMTEwMDA=
Hint 1: Crest 3 has been encoded three times
Hint 2: Crest 3 contanis 19 letters
```

Visiting the last room /attic/ asked the same shield key and after putting it I found the last crest note

```
crest 4:
gSUERauVpvKzRpyPpuYz66JDmRTbJubaoArM6CAQsnVwte6zF9J4GGYyun3k5qM9ma4s
Hint 1: Crest 2 has been encoded twice
Hint 2: Crest 2 contanis 17 characters
```

Now time to decipher them, starting from crest1

I put it in cyberchef and it showed me to first translate from Base64 and then from base32 and final text was: RlRQIHVzZXI6IG

Crest2 I put in and got from base32 and from base58 and final text was: h1bnRlciwgRlRQIHBh

Crest3 I recognized as base64 so I put that manually and then from binary and from hex and got: c3M6IHlvdV9jYW50X2h

Crest4 had from base58 and from hex and text was: pZGVfZm9yZXZlcg==

Now all them together in cyberchef and I got ```FTP user: hunter, FTP pass: you_cant_hide_forever```

## Task 3 - The Guard House

Logging in with ftp showed me 5 files

<img style="max-width:100%; height:auto;" alt="image-2" src="https://github.com/user-attachments/assets/c576b604-69f2-4d63-ae02-b38727b7eb87" />

So I used ftp get to get them to my computer, looking at the important.txt first I found a hidden directory ```/hidden_closet/``` but it required helmet symbol which I didn't have so back to the files

Using exiftool on the image files it didn't show on the 1 and 3 anything but on number 2 I saw comment ```5fYmVfZGVzdHJveV9```, possibly part of the gpg password

I was stuck for a while but then I looked at the hint ```Three picture, three hints: hide, comment and walk away``` I already had used the comment hint so now I had to figure out the others.

After a while of googling around and thinking I thought the hide could mean steghide and I used that tool to extract files ```steghide info 001-key.jpg``` showed a file ```key-001.txt``` and got the files with extract ```cGxhbnQ0Ml9jYW```

Using steghide didn't work for number 3 but from googling before I found binwalk which could work ```binwalk -e 003-key.jpg``` got me ```3aXRoX3Zqb2x0```

Now I had the full line ```cGxhbnQ0Ml9jYW5fYmVfZGVzdHJveV93aXRoX3Zqb2x0``` and putting it in cyberchef gave me ```plant42_can_be_destroy_with_vjolt```

With that I opened the gpg file and got ```helmet_key{458493193501d2b94bbab2e727f8db4b}```

## Task 4 - The Revisit

Going back to the /closetRoom/ and the /studyRoom/ I now got in

In the closet room I found MO Disk1 ```wpbwbxr wpkzg pltwnhro, txrks_xfqsxrd_bvv_fy_rvmexa_ajk``` and wolf medal ```SSH password: T_virus_rules```, also the answer to leader question ```Enrico```

In the studyRoom I found a gz file which had the text ```SSH user: umbrella_guest``` inside

## Task 5 - Underground Laboratory

Going through the files I found /weasker/ folder which had a weasker_note.txt, from looking at the note I found out that weasker was the traitor. And also the ultimate form ```Tyrant```

Now from previous I had the M0 Disk1 I decided to put it to a vigenere cipher decoder and automatic solver and got the text ```albert weasker login password stars members are my guinea pig```, so maybe it could be ```albert weasker login password: stars_members_are_my_guinea_pig```

I looked around and something was odd since the umbrella_guest folder was empty, so doing a ```ls -a``` showed me the hidden files, all looked normal except ```/.jailcell```, looking inside I found chris.txt

Now I tried to use the weasker password to change account to him using su and found out that I had root access so I finally got into the /root/ to get the flag

# Conclusion

This wasn't the normal type of CTF but rather a puzzle which in my opinion made it an amazing one, I really enjoyed this and it made me think differently and train my puzzle solving
