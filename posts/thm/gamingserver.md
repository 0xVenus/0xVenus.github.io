### Gaming Server tryhackme
[link](https://tryhackme.com/room/gamingserver)
### difficulty = easy
### os = linux

  Hi guys,
  
  <br> let's pwn another box named "gamingserver"
  
 <br> As we all know that enumeration is the key
  
  <br> so, let's start our enumeration with port scanning using *nmap*
  
  **Nmap scan**
  ![nmap](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8830bf4d-d824-4f5b-bedb-0017641a94f5)
we're done with our scanning
<br> As you can see there are lots of open ports

<br> let's start the open ports enumeration from port 80(http)

<br> so, visiting the homepage and viewing the source code revealed a username " john" (note it down)

![username_Found_in_homepage_source](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ddbebe41-a572-4713-8747-806265f24bf0)

so, let's proceed to directory bruteforce using my fav tool **ffuf** (fuzz fast u fool)
![dir_bruteforc](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/87d19d4f-7493-4a69-8e49-5d852a4b2312)
wow, we got few directories which "secret" and "upload" seems to be the sus ones (hacker mindset yunno lol)

<br> Navigating to the upload directory shows a password list file and a manifesto file

<br> now, let's download the file to our attackbox using wget

![wget_for_downldin_the_files](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/6d03f9c2-3acc-4b0a-be20-deb596b53af7)

Then let's navigate to the next directory which is secret
![found_ssh_key_in_the_dir](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/485b72c6-9b6f-4100-9757-a9c216cc3ea9)
As you can see there is an ssh key in the directory, copy the key to your attackbox.

<br> let's ssh into the box using the username found earlier "john" together with the ssh key
```
ssh -i ssh_key john@10.10.127.240
```
it is requesting for john's password which we don't have , it shows the ssh key is encrypted
<br> let's decrypt the key using **ssh2johh** 
<br> then, crack the pasword using john

![ssh_passphrase](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8cb8be19-49e7-4ee6-b4a0-215df3c4aa2a)

as you can see we've gotten the passphrase for the ssh key 
<br> let's login again and entering the passphrase gives us initial foothold on the box
![got-in-the-box](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ebb29abf-e63e-4e74-beb6-875507a8656b)
so, let's cat the user flag Hackerman :)
 
 ## privilege escalation
 upload [les](https://github.com/mzet-/linux-exploit-suggester) (linux exploit suggester) on the box
 
 ![les](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/9ee2575d-f648-47ec-9572-b9569a0ede76)

 so, LES outputs shows that our target is vulnerable to cve-2021-3156 **sudo baron sameedit**
 <br> run the exploit and pop a root shell
 
![root](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/7dcdfa7a-4fbc-4e59-885f-d848a523cdb6)

And we are done !!

*till next time, bye hackerman*








