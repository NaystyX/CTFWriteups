# Disk Analysis & Autopsy

https://tryhackme.com/room/autopsy2ze0

Info from the excersice page <br />
Username: administrator <br />
Password: letmein123!

Starting the machine I got put into a virtual machine where I had the case files and autpsy ready.<br />

## Questions

### What is the MD5 hash of the E01 image?

I opened the case file in autopsy and found the MD5 hash in the E01 images metadata
<pre><details>
<summary>MD5:</summary> 3f08c518adb3b5c1359849657a9b2079
</details></pre>

### What is the computer account name?

I looked at the different files in the results page on autopsy until I found Operating System Information
<pre><details>
<summary>Computer account name</summary> DESKTOP-0R59DJ3
</details></pre>

### List all the user accounts. (alphabetical order)

Looking for last questions answer I also saw Operating System User Account. When I opened it I found the different usernames. I filtered off the default accounts.
<pre><details>
<summary>User accounts</summary> H4S4N,joshwa,keshav,sandhya,shreya,sivapriya,srini,suba
</details></pre>

### Who was the last user to log into the computer?

On the same file there was Date Accessed on the users and I thought that would be the last log in, which in the end was correct.
<pre><details>
<summary>Last user to log in</summary> sivapriya
</details></pre>

### What was the IP address of the computer?

I started this by looking around a bit of the files and getting stuck, then I saw keyword list search and did a IP search. That resulted in over 2000 results so it didn't help me too much. 

After being stuck for a while I figured I'd look at installed programs, since there is a question later about network monitoring tool. I found a program Look@LAN and tried to search it in program files.

In the LookAtLAN program files I found a .ini file that had the LANIP inside. This was a tougher one.

<pre><details>
<summary>IP:</summary> 192.168.130.216
</details></pre>

### What was the MAC address of the computer? (XX-XX-XX-XX-XX-XX)

This answer was right under the Lan IP, just withoud the dashes.

<pre><details>
<summary>MAC: </summary> 08-00-27-2c-c4-b9
</details></pre>

### What is the name of the network card on this computer?

I was stuck for a bit here since I knew to look at windows registry but I couldn't look at the registry files. Then I found out that the case files had already regripper files outputted so I searched for SOFTWARE file there to view drivers.

There I searched for Networkcards and found my result.

<pre><details>
<summary>Network Adapter</summary> Intel(R) PRO/1000 MT Desktop Adapter
</details></pre>

### What is the name of the network monitoring tool?

This I already had found out while looking for the IP.

<pre><details>
<summary>Monitoring tool</summary>Look@LAN
</details></pre>

### A user bookmarked a Google Maps location. What are the coordinates of the location?

I looked at the Web Bookmarks to try and find it, I saw many unnecessary bookmarks so I sorted by title since coordinates have numbers so they should be at the top and found the location.

<pre><details>
<summary>Coordinates</summary>12°52'23.0"N 80°13'25.0"E
</details></pre>

### A user has his full name printed on his desktop wallpaper. What is the user's full name?

To start I opened the Images/Videos on autopsy since I didn't have anything else on mind. After looking at the users I saw Joshwa's wallpaper and a name on the top left.

<pre><details>
<summary>Name</summary> Anto Joshwa
</details></pre>

### A user had a file on her desktop. It had a flag but she changed the flag using PowerShell. What was the first flag?

For this I thought of searching for the powershell history but I needed to figure whose history to look at.

Viewing the different users desktop we can find shreya.txt which says ```flag{i_changed_it}```. Knowing this we can go to the powershell history of shreya and find the flag.

<pre><details>
<summary>Flag</summary>flag{HarleyQuinnForQueen}
</details></pre>

### The same user found an exploit to escalate privileges on the computer. What was the message to the device owner?

This we can see in the desktop of shreya again, there is an exploit.ps1 file. Reading the content we can find the flag.

<pre><details>
<summary>Flag</summary>flag{I-hacked-you}
</details></pre>

### 2 hack tools focused on passwords were found in the system. What are the names of these tools? (alphabetical order)

One of these I recognized before when going through the files which was ```mimikatz```

For the other one I looked through user downloads where mimikatz was but no luck. Didn't see any suspicous programs either. I did some googling on where to look for hack tools and saw talk about windows defender, so I googled where to find WD data and found scan history at ```C:/ProgramData/Microsoft/Windows Defender/Scans/History```.

There I found the mimikatz in detection history so I knew I was close. After going through the folders I found ```lazagne``` which I googled and was infact what I was looking for.

### There is a YARA file on the computer. Inspect the file. What is the name of the author?

I did a file search by attributes with .yara files but didn't find anything so I found out that YARA has another extension .yar so I did that. With that I found what I was looking for.

<pre><details>
<summary>Author</summary>Benjamin DELPY gentilkiwi
</details></pre>

### One of the users wanted to exploit a domain controller with an MS-NRPC based exploit. What is the filename of the archive that you found? (include the spaces in your answer) 

I began by googling about MS-NRPC exploits and found much articles about zerologon, so I decided to search that with keyword search.

With that search I found the encrypted zip file I was supposed to find.

<pre><details>
<summary>Answer</summary>2.2.0 20200918 Zerologon encrypted.zip
</details></pre>

## Conclusion

This challenge definitely taught me more about autopsy since I hadn't used it that much before. It also taught alot about where to at for files in windows in general.

Definitely was on the harder side for me and took a bit of googling to get forward with certain parts.
