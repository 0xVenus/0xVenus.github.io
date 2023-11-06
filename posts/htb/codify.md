<h2>CODIFY HTB</h2>


### NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8a6e7234-f883-4835-831b-61e6e38cfb69)

``Add codify.htb to /etc/hosts file``

visiting the url shows our target is a Node.js editor

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/43820d8b-1120-41a7-9fef-eeb654420e65)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8e5750d5-a53c-4997-939d-0ea60b9aba08)

And yeah we can see it's running `vm2 version 3.9.16` which is vulnerable to ``Remote code execution`` ``CVE-2023-30547``

so, a quick google search gave the [exploit](https://gist.github.com/leesh3288/381b230b04936dd4d74aaf90cc8bb244)

we can easily gain reverse shell by modify the execSync funtion and setting our netcat listener

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c5e6cc05-bfa4-45ee-8364-6f10b32018b9)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2735706b-e8f3-49ad-958a-6900386949fc)

### PRIVILEGE ESCALATION

Trying to read the files in joshua directory and permission was denied

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2ab2583d-61ff-42f2-8401-627c24c3256f)

so, there's a database file in the /var/www/contact directory which contains the user joshua password hash

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/764131ac-3120-402d-9083-2bb41ded93be)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/3120ca6f-a3d2-4699-8cc1-cfe24bd69a2a)















