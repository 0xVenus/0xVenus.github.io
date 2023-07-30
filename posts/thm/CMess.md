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




