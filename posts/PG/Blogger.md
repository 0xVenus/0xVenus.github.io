### BLOGGER

ip = 192.168.159.217

difficulty = easy

os = linux

#### Nmap scan
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/fd87fd72-91cb-4063-88e8-0fbf2bc82576)
we have two ports open

so, let's start with port 80(http)
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/df21a51a-74aa-40f4-b2c4-1948199b65d3)
see what we have on the page

i clicked around to explore some features but it seems it's a Static page but note down the programmer's name "james"

let's fuzz for directories
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/751e1462-c090-46c4-8cd5-bd34543c6e12)

going over to the assets directory we have the sub directories and it's running wordpress
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/edb574bc-101e-4df1-8592-0553fbe7bdb0)
And we got the domain *blogger.thm*

so, let's add it to our */etc/hosts* file

let's enumerate the wordpress cms using wpscan
``` wpscan --url http://blogger.thm/assets/fonts/blog/ --plugins-detection aggressive```

it's shows the wp version is 4.9.8 and a vulnerable theme poseidon which runs an outdated version too (v2.1.1)
and a vulnerable plugin too *wpdiscuz v7.0.4*

tried exploiting the wp and the poseidon theme but non worked

so, let's try exploiting the wpdiscuz plugin

The vulnerability allows abitrary file upload

The details can be found [here](https://www.wordfence.com/blog/2020/07/critical-arbitrary-file-upload-vulnerability-patched-in-wpdiscuz-plugin/)

In the post comment field there is an option to upload/attach image to comments
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/836b6e24-7d8f-4f27-97cb-18c0cbd326ad)

trying to upload a php file gave error coz it accept image files only.

was able to bypass it by add the gif header ```GIF89a``` to the beginning of the code

start a netcat listener and fill the form with random data and upload the comment.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b1205e3f-9ed2-4326-94ba-251395fff848)

so let's get our uploaded reverse shell
since our target is running wordpress then the upload folder should be /wp-content/uploads/
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a4ac8d54-d3f0-471d-9a60-326de6215d5d)
As you can see the directory has our uploaded file.

clicking on it gave us a shell on the target system
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/1db703b7-6969-4898-8454-ca63489bb395)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/03807a63-c51f-44e4-b2c7-c2e804034fee)

#### Privilege escalation

There is an hidden file in the /opt directory
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ac04618a-369f-4208-9740-6c63df2c9dcc)
it contains hardcoded credentials 

seeing this i knew it's rot47 
so i used cyberchef for decoding the rot47 creds which output a base64 encoded chars
so decoding the base64 gives another base64 and decoding it again gives the output ```james:S3cr37_P@$$W0rd```
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ca8f65f0-aeb1-4fbd-aa51-0d91fe40f02c)

let's change user to james using the credentials gotten
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/46f68318-ffdb-4240-bd55-ac24ee204a6b)

after deep enumeration was able to switch to user vagrant by using vagrant as passwd
```su vagrant```

```password: vagrant```

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/019b119c-1f69-4425-9ac5-627d0d3c3469)

so, user vagrant can run anything as root

```sudo su``` gives us the root shell.


Thanks.
Bankai Tensa zangetsu


















