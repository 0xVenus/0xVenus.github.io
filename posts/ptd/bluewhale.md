## WHALE

DIFFICULTY= medium

OS = Linux


### Nmap scan

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e7ac9040-3910-472c-be9b-5ef758724426)

adding the domain to /etc/hosts
``echo "ip  bluewhale.net" >> /etc/hosts``

so, visiting the site shows it's running wordpress

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/016ff2dd-3aa3-4996-87f1-71fe567ed16f)

let's enumerate the wordpress using ``wpscan`` aggressive detection

```wpscan --url http://bluewhale.net/  --plugins-detection aggressive -t 120```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e4f489b7-a427-4c19-8ae1-ac24d5acb083)

it gives us a vulnerable plugin; the plugin is vulnerable to arbitrary file read

so, we can exploit it using [this](https://www.exploit-db.com/exploits/33004)

doing that,we should be able to read the wordpress config file ``wp-config``

```bluewhale.net/wp-content/plugins/post-pdf-export/dompdf/dompdf.php?input_file=php://filter/read=convert.base64-encode/resource=../../../../wp-config.php```

reading it gives us the gives us the base64 encoded chars.

decoding it shows the mysql credential

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/01cdc783-aa0d-4bb4-90b5-4cc1923258e5)

let's login to mysql with it 
``mysql -u wordpress -h bluewhale.net -p``
and input the password

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/7780d4f1-3484-4965-9a8e-160e4e8cad08)
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8e86ab4c-12bc-4a85-b364-48d9a0198a5a)

as u can see we have the first flag already

let's proceed by checking the wp_users table 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/eb5268df-f706-4f33-9883-980684964c78)

and yeah we have the credentials for the wordpress login

so, instead of cracking the password hash we can actually change the password to our desired own for easier loggin(cool trick right?) lol

```UPDATE wp_users SET user_pass = MD5('hacked') WHERE ID = 1;```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/bc564284-6efa-44b7-a82f-dcd6707a4d05)

so, we can now login to wordpress and proceed

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/4b971843-adc4-4474-90ba-1f82bfa63aca)

login and upload a reverse shell using the add plugin feature
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/288de2a8-c124-488d-9af6-0499c0212844)

and let's access our shell in the upload directory
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/49a87b3e-5c6e-4a98-952d-ae3f2b0020b0)

 getthe reverse shell and stablize it

 ![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/4f5fedf6-4f12-4775-b36c-3350bc222824)

 enumerating further i got the ssh private key for the user ``whale`` in the whale home directory ``.bak`` cool :)

 ![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b03ecfd8-664d-4866-b2d6-155715944b35)

 so we can now ssh into the box as user whale

 ![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/dfe9578b-01d0-4564-b69a-2779e77e4964)

 so let's read the FLAG58 which we ain't able to read before.

 ![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/dc6da781-061d-45c5-80dc-f1c0ab394633)

 










