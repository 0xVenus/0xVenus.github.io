### Morty



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

so reading the extracted file gives rick's ssh password.
WubaLubaDub1!
