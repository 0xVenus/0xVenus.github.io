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

so let's Intercept the request (post comment) in Burp suite and Modify the wmu_files[0] section with PNG magic bytes, file name and content type for us to upload our php reverse shell successfully









