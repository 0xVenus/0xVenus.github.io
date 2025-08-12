<a href="https://0xvenus.github.io" style="display:inline-block; padding:8px 12px; background:#0078d4; color:#fff; text-decoration:none; border-radius:4px;">
    ⬅ Back to Homepage
</a>


### FULLMOUNTY

OS = Linux

Difficulty = Easy

#### Nmap scan

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/dd23e073-c340-45ae-a2e2-dd28af07eaed)

Enumerating other ports gives nothing IG🧐.

let's move to nfs

you can learn more about NFS enumeration [here](https://book.hacktricks.xyz/network-services-pentesting/nfs-service-pentesting)


so let's list the shares mount it

```mkdir /tmp/mount```

```showmount -e 10.150.150.134```

```sudo mount -t nfs -o vers=3 10.150.150.134:/srv/exportnfs /tmp/mount/ -o nolock```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/23fda0de-c7d7-47fa-adc2-f7896d027f0f)


from the result we have an ssh private key which can be used for sshing into the box 🔥

reading the public key *id_rsa.pub* we have a user ```deadbeef```

let's give permission to the ssh key file

```chmod 600 id_rsa```

so ```ssh -i id_rsa deadbeef@10.150.150.134```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c9e63b9b-276b-46c1-ac5c-4594ec4a7c93)

And yeah we have the user flag 😎😎.

### Privilege escalation

The Kernel version is vulnerable to dirtycow exploit

to confirm that run ```uname -a```

Also, for you to be able to exploit it, you need to compile the exploit on an Ubuntu machine with the same kernel version😪.

Doing that i was able to escalate privilege successfully

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/39f5c047-110a-4ce5-a0fe-1e83b94f5b72)


Thanks.


