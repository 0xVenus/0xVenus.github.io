### Morty


![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ea6ae596-3dd7-4683-8660-1e8155880a0a)

os - linux

difficulty - medium




#### Nmap scan

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/215af980-a294-4ccd-8328-f182716a1db2)
let's start with port 80


![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/597ee851-5ed4-4e7e-b612-238b6d42bacb)
potential usernames ```morty and rick```
and add the domain to your /etc/hosts file
going over to the site shows this below
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/77cea032-b5dc-4cbf-ae9f-672e5ba40ec7)

found a password ```Fl4sk#!``` tried for it ssh but it didnt work.

so the image looks sus
let's download the image and extract it with steghide using the password found earlier

```wget http://mortysserver.com/screen.jpeg```

```steghide extract -sf screen.jpeg```

```passphrase: Fl4sk#!```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/336f855e-7a36-4f3f-8a99-f8cef4f9363f)

so reading the extracted file gives rick's password.

tried it for ssh but it didn't work too

so, let's move to the other port which is dns (port 53)


**enumerating port 53**

let's perform a dns zone transfer**

``` dig axfr @10.150.150.57 mortysserver.com```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/7aa6ea9a-3444-4b1c-9e0f-4f8cd70348d6)

```This procedure is abbreviated Asynchronous Full Transfer Zone (AXFR).```

let's add the domains to our /etc/hosts file too

so, visiting the rickscontrolpanel.mortysserver.com shows phpmyadmin login page

let's try  loggin in with ricks username and pasword we found earlier

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/5ba3cc46-7c21-493a-8012-bb4ff20be1da)

dope it worked!

After spending some time trying to upload a webshell which i wasn't able to' coz i couldn't find a writable path.

i found out that the phpmyadmin version is vulnerable to RCE

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d2ce2e0c-ad27-4058-9f08-aaa951673869)

using searchsploit to find exploit
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/4d0697c7-3714-4779-9fe1-1aff87cca1bb)

so get the exploit using ```searchsploit -m 50457```

then run it to get a reverse shell

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/69ae7b48-9777-412f-8dae-0f544f98ceae)



Thanks.










