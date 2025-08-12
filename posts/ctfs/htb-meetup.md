<a href="https://0xvenus.github.io" style="display:inline-block; padding:8px 12px; background:#0078d4; color:#fff; text-decoration:none; border-radius:4px;">
    ⬅ Back to Homepage
</a>

**FULL PWN write up (BACHIRA)**

My Username: Bachira

machine ip: `16.16.145.247`

so scanning the machine with nmap gives us 3 open ports which are :

25 -- smtp

80 -- http

587 --smtp
![image](https://github.com/user-attachments/assets/14248d72-e55a-4896-a899-4ea94c771946)

so i tried enumerating 25,587 but couldnt reach them. then i went back to port 80

found out that it is resolving to a domain `http://pfops.htb` when pasted in browser(like normal htb boxes lol)

so i added it to /etc/hosts file.

i opened the domain i got a 403

then i reached out to the admin if it was part of the challenege he said yes.

so i went back to read the rules. `we must add a custom user agent for every request for it to be successful`.

so, i downloaded a firefox extention which allowed to me to set a custom user agent for the domain.

then i fuzzz for directory using ffuf:

`ffuf -u http://pfops.htb/FUZZ -H "User-Agent: htbmeetupcmr bachira" -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt`

got some directories which aint Useful. except for the `dev` directory

i opened it but it's nothing. after much of time i retried fuzzing recursively then i got a hit at `dev/.git` which means .git is a hidden subdirectory

then i used the `git-dumper` tool to dump the .git folder into my machine

` python3 git_dumper.py http://pfops.htb/dev/.git -u "htbmeetupcmr bachira"`


then going through the dumped git folder i found out that an ``htaccess`` file was deleted

well i tried reading the htaccess file using `git show`

then it displayed some rules for having a succesful request to particular subdomain `dev.pfops.htb` which i fuzzed for earlier and it's returning 403 . I added the subdomain to /etc/hosts

then i followed the allowed rules in the htaccess file. which are:

The request must contain some headers
```
Special-Dev: only4dev

X-Forwarded-For: 192.168.100.0/24

Admins: Tom
```
so i added the headers to my firefox extension i got earlier.

Now i was able to reach the subdomain

going over to the subdomain i saw an `xml upload`  feature.

i tried XXE for many hours coz when i initially used a simple php web shell it was only rendering my payloads blank/plain.

Then i finally used  pentest monkey reverse shell with `.xml` extension instead of a normal cmd web shell.

then i was able to access my uploaded file at the upload directory coz i already fuzz for directory on that subdomain.

was able to search it with the time i uploaded it. using ctrl+f then inputing my uploaded time
![image](https://github.com/user-attachments/assets/e5f9a311-a1c4-4529-ae21-833eec6ce21b)

![image](https://github.com/user-attachments/assets/cd3aff07-d00a-4132-90b2-4794768757dd)

PS: i used portmap.io for portforwarding tho

Then i got reverse shell

![image](https://github.com/user-attachments/assets/8fffcf7c-99de-44ca-885d-4458f4d21e80)

i stabilized it and then proceed to my privilege escalation

**Privilege Escalation**

![image](https://github.com/user-attachments/assets/378e3930-36bb-42aa-8b2a-4fb609402b2f)

I got Tom's password and i tried it to login to myql but nothing good in the mysql db

so, i then tried `su tom` with that password and i got the user flag lol.

![image](https://github.com/user-attachments/assets/5b251c80-7b87-4015-9dc8-8605aa73f932)

then i ran `sudo -l` and see that user tom can run nmap with sudo permissiion. 

so i abused it to get root same way the iphoto challenge too. using the gtfobins

![image](https://github.com/user-attachments/assets/3078c1ff-d89b-468b-9c48-05fe6f48bdb4)

Thanks.






