<h2>WEKOR THM</h2>

OS = Linux

DIFFICULTY = Medium


##NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b934e443-5db2-47c5-980d-bf8eeb5f625f)

let's start our enumeration from port 80 which is running http server

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/5df0a3fc-387b-4b8f-9f15-83c32337a2c0)

As you can see there is nothing interesting on the site hompage

so, checking ``robots.txt`` on the site revealed some endpoints.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f7562883-772b-4a3f-b4bd-6a17fcc40c91)

checking it one after the other gives nothing except the ``comingreallysoon`` directory

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c06341fd-9c65-4bd9-876e-1ec7f01cfb3b)

And yeah there's is a note on the page telling us the location of their new website

``Welcome Dear Client! We've setup our latest website on /it-next, Please go check it out! If you have any comments or suggestions, please tweet them to @faketwitteraccount! Thanks a lot ! ``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/af7b0ed7-84f5-4eb4-9e1b-22c2f3cc3928)

going over to the cart page and applying a single quote throws SQL error indicating possible sql injection

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/d89d5ee3-1a0f-4c2d-854b-0ce4d1c18b4a)

so, intercept request with burpsuite and copy the request into a file.

Then dump the database by running ``sqlmap`` on the file











so, add the domain ``wekor.thm`` to your /etc/hosts file

Then fuzz for subdomains using ffuf

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f360b5f8-1fdf-4b7b-ae0c-792c7e6b52e3)

And yeah, we have a valid subdomain. So, add the subdomain ``site.wekor.thm`` to your /etc/hosts file too.

let's check the subdomain now
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/ca75b5b2-6d86-4890-9da7-d3e7f1f64de8)

we have a possible username ``jim``

let's fuzz for directories on the subdomain

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/fab4824b-d202-4dc6-bf36-75de7af115c7)

we have a wordpress directory let's have a look at it.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b13aa8f7-baeb-4d18-87a8-b940f11580c7)

Enumerate the wordpress site using ``wpscan``












