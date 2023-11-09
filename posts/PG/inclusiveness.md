<h2>Inclusiveness</h2>


### NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b0e19282-780e-40e6-bafc-4f3346bf5f8a)

Anonymous ftp is enabled but there's nothing on the server

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/2adfb636-b556-4793-a277-98ffc5535ea1)

let' proceed to port 80 http

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/64b94444-ebca-4d66-b74d-b8d760858d55)s

we saw apache default http page

so, let's check ``robots.txt``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/881bb90e-c274-41a2-aed6-660bc31fbca8)

we cant view it content from the web wow

we can actually bypass that using `curl`

```curl -s --user-agent Googlebot http://192.168.204.14/robots.txt -v```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f2ae9a7e-3909-4304-ad75-1299c2e4b662)

we can see the new endpoint ``/secret_information/``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/363a5a04-fc35-4107-9fee-e347cef80da2)



