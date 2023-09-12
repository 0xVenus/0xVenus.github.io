## STUNTMAN MIKE

IP - 10.150.150.166
OS - LINUX
DIFFICULTY - EASY

### Nmap scan
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/daba7f0d-89a0-4c77-a3de-fde0fa6f2d51)

we have two open ports

let's start enumeration from port 22

bruteforcing ssh with hydra gives password for the user mike
```hydra -l mike -P /usr/share/wordlists/rockyou.txt 10.150.150.166 ssh -t 4```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/1fc3d3b6-0184-44f7-b0fa-7f95d6569c2b)


let's login to the ssh server using the creds
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/7f5a7a4d-92b9-486c-b22b-359e4e45b3ad)

we have both the FLAG35 & 36 respectively

### Privilege escalation

Running ```sudo -l``` shows that the user mike can run ALL comands with sudo

so, ```sudo su``` spawned us a root shell.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/9a4dbbcf-4997-420f-ad45-97ddb09423a9)



Thanks.

