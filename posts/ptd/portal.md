<h1>PORTAL PWNTILLDAWN</h1>

## IP = 10.150.150.12
## DIFFICULTY = EASY

 Hi guys lets solve another fun box again

### NMAP scan
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/1925b8d8-abb8-451c-a00e-34f173f1184d)
we have 2 open ports

### ENUMERATION AND EXPLOITATION
so, let's start our enumeration from port 21 which runs FTP by default and which allows anonymous login
```username: anonymous and password: hit enter(blank password)```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a8b72bfd-a743-4eda-8a53-7a499e090871)
And yeah we have nothing on the FTP server

so, going back to our nmap scan shows the FTP server is running vSFTPD version 2.3.4
searching for exploit led me to this [exploit](https://github.com/ahervias77/vsftpd-2.3.4-exploit)

so, running the exploits gives us root.
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/9a848a75-dcd1-4b21-b89c-1c7fb63ae2b0)

Stabilizing the shell using ``` python3 -c "import pty;pty.spawn('/bin/bash')"``` then ```export TERM=xterm``` 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f1099d57-55be-4515-a756-69b50807e87d)

And we are Done

Thanks.






