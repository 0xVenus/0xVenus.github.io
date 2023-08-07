### Boxname = BBScute
### difficulty = easy


### Nmap scan
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/9b8cdb3f-8296-4724-b6ce-88466fa846b8)
let's begin the enumeration from port 80

we saw apache index page on port 80
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e45e1011-af4f-4910-841d-538c04651816)

viewing the source doesn't reveal anything. So let's proceed to directory brute forcing using ffuf

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d1a11d14-7084-44c4-bc04-2b3543dd511f)

```
ffuf -w /usr/share/wordlists/dirb/common.txt  -u http://192.168.163.128/FUZZ
```
so, lets check the *index.php* directory first

we're presented with this page below

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/05f2d94e-04d6-4956-8163-dbea94a4e559)

so, let's search for possible exploits for the software version i marked above in the pics (cuteNews 2.1.2)

i got this [exploit](https://github.com/thewhiteh4t/cve-2019-11447)

so, we need to have an account for us to be able to use the exploit

moving on to the registration page and let's try to register an account.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a3eea2a3-da9d-43ac-9342-0c029b402805)

as you can see there's no captcha value to enter 

but viewing the source revealed the captcha directory

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c4ede2a0-02c0-4f0f-bf11-ddb39c1c250f)

going over to the captcha directory showed the captcha value

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b6cceaa3-734a-4045-b30a-46973ed1941c)

let's complete our registration.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/17666628-16f1-40e1-b735-78e793134918)
we are now authenticated so let's use the exploit again since we've gotten login credentials

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ac6650fa-3764-4204-b944-2f41f8c8e5cb)

we got bunches of errors due to the target hostname we provided

tho it's shows the target hostname so let's add it to our /etc/hosts file and run the exploit again

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a281cb4a-82e0-488a-b15f-92c89d0b9592)

And yeh we gained foothold on the machine

so  finding the user flag using the find command as specified in the above pics gave the user flag.

### Privilege escalation


i used bash to get a proper revershell (tty shell)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/6b36f57a-5c3e-4391-ab26-401c9531a79e)

so checking for suid binary shows we can run hping3 as root

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f855eff5-5425-4d71-90ab-e1a1b07f22ef)

so lets check gtfo bins for the payloads to use in abusing the SUID binary.


using ``` /usr/sbin/hping3 then /bin/bash/ -p ``` gives us root.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/bce4e3c1-ba95-464c-aa1e-ac592bf793e7)

Thanks and have a nice day.

reach out to me at [twitter](https://twitter.com/0x_venus)

Bankai TENSA ZANGETSU lol 😂😂

