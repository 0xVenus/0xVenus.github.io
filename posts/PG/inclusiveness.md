<h2>Inclusiveness PG</h2>

Let's hack the target 🤭

### NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b0e19282-780e-40e6-bafc-4f3346bf5f8a)

Anonymous ftp is enabled but there's nothing on the server 🙂

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2adfb636-b556-4793-a277-98ffc5535ea1)

let's proceed to port 80 http

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/64b94444-ebca-4d66-b74d-b8d760858d55)

we saw apache default page

so, let's check ``robots.txt``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/881bb90e-c274-41a2-aed6-660bc31fbca8)

we can't view it content from the web 😯😯

we can actually bypass that by modifying the useragent and we can use `curl` yeah

``curl -s --user-agent Googlebot http://192.168.204.14/robots.txt -v``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f2ae9a7e-3909-4304-ad75-1299c2e4b662)

we can see the new endpoint ``/secret_information/``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/363a5a04-fc35-4107-9fee-e347cef80da2)

Note on DNS ZONE TRANSFER and i don't think this box has something to do with that

so clicking on the language hyperlink showed this
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c9f5e123-dbb8-4ec3-9874-2052d2bacb79)

screaming file inclusion lool 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d0f09d00-d129-495f-ac3c-8f7d8d016447)
we have lfi fr

recall we can write to the ``/pub`` directory on the ftp server

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/fb4b01c5-8d7e-4426-918e-4f34546d0c71)

so we can put our shell into the directory and load it via the webserver through the ftp path to spawn a reverse connection 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e17282d4-5cee-43b8-85db-f1bd3e9b0297)

set your netcat and load the shell

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/075d15dd-6172-4f2e-88a2-5887f4d929fb)

spawn it
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/3e5c036a-0702-4411-b65a-2f35cb34ed9d)

### PRIVILEGE ESCALATION

So, find command gave list of programs that has the SUID bit where I notice /home/tom/rootshell.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b45180eb-b46f-4ea7-bfef-0fd429b8ed74)

``Inside /root/tom/ I found rootshell.c file and a compile file rootshell that owns SUID permissions.
According this piece of code if the file is executed as Tom user by calling the function for “whoami” program for validation then you will get a privilege shell else it will print user-ID that is currently logged in will be displayed.``

In simple words the rootshell program give a high privilege shell if the output of whoami program will be “tom”.

You can easily take advantage of this configuration by abusing the PATH system. Here, we built a file as “whoami” in the / tmp directory, and write the following bash code to print “tom”

``cd /tmp``

``echo "printf "tom"" > whoami``

``chmod 777 whoami``


Add a temporary path variable with the help of the following command. you will observe that we had added /tmp as PATH variable.


``export PATH=/tmp:$PATH``

``echo path``

Execute the rootshell

``
cd /home/tom;./rootshell
``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/678f3e03-2613-4d6b-af49-848ee6964bc6)


And we are done.


Thank you 🔥.







