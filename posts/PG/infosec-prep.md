<a href="https://0xvenus.github.io" style="display:inline-block; padding:8px 12px; background:#0078d4; color:#fff; text-decoration:none; border-radius:4px;">
    ⬅ Back to Homepage
</a>



## Infosec prep


os = linux

difficulty = easy

### Nmap scan
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/cd1ed363-1281-47bd-a7f9-ef10c6fc8296)

lets start the enumeration from port 80.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/684db98c-3334-4f4f-ac78-7e258e17ec5d)

we have a potential username which is ```oscp```

so going over to the ```/secret.txt``` directory gotten from the nmap scan shows base64 encoded chars

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/03baa7fe-eed0-463b-a554-42571cdd94c0)

decoding it with cyberchef gives ssh private key

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/fcdd31a9-acd9-449c-8a15-304683c85bf0)

so, let's ssh into the box using the username and the key

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/4b1360b0-a285-4fe8-ac26-54aa45cfb302)


### Privilege escalation

Checking what binaries have SUID permissions, we find that /bin/bash is misconfigured

```find / -perm -u=s -type f 2>/dev/null```

so we can easily gain root by abusing it using ```/bin/bash -p```

 
**2nd way of gaining root**

found out that the machine is vulnerable to pwnkit 

so, exploitng it give us root.


![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/000483bb-9131-4d22-90f4-1cb1d3bb1876)





Thanks.


