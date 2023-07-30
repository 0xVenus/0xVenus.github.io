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
And set ur ncat listener then click on the assets directory to load the uploaded shell
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/97a033da-8bd5-477d-b5d8-ccc11be3dea4)
clicking on it spawned us a shell on the target system

we have our sweet reverse shell. so, stabilize it
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c3f9e157-3537-45e9-a1d4-35b28bc19cc8)






