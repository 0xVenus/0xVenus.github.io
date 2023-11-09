<h2>Inclusiveness PG</h2>


### NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b0e19282-780e-40e6-bafc-4f3346bf5f8a)

Anonymous ftp is enabled but there's nothing on the server

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2adfb636-b556-4793-a277-98ffc5535ea1)

let's proceed to port 80 http

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/64b94444-ebca-4d66-b74d-b8d760858d55)

we saw apache default page

so, let's check ``robots.txt``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/881bb90e-c274-41a2-aed6-660bc31fbca8)

we cant view it content from the web wow

we can actually bypass that by modifying useragent and we can use `curl` yeah

``curl -s --user-agent Googlebot http://192.168.204.14/robots.txt -v``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f2ae9a7e-3909-4304-ad75-1299c2e4b662)

we can see the new endpoint ``/secret_information/``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/363a5a04-fc35-4107-9fee-e347cef80da2)

Note on DNS ZONE TRANSFER and i dont think this box has something to do with that

so clicking on the language hyperlink showed this
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c9f5e123-dbb8-4ec3-9874-2052d2bacb79)

screaming file inclusion lool 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d0f09d00-d129-495f-ac3c-8f7d8d016447)
we have lfi fr

recall we can write to the ``/pub`` directory on the ftp server

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/fb4b01c5-8d7e-4426-918e-4f34546d0c71)

so we can put our shell into the directory and load it via the webserver though the ftp path to spawn a reverse connection 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e17282d4-5cee-43b8-85db-f1bd3e9b0297)

set your netcat and load it the shell

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/075d15dd-6172-4f2e-88a2-5887f4d929fb)

spawn it
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/3e5c036a-0702-4411-b65a-2f35cb34ed9d)

### PRIVILEGE ESCALATION












