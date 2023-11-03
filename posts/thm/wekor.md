<h2>WEKOR THM</h2>

OS = Linux
DIFFICULTY = Medium


##NMAP SCAN

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/b934e443-5db2-47c5-980d-bf8eeb5f625f)

let's start our enumeration from port 80 which is running http server

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/5df0a3fc-387b-4b8f-9f15-83c32337a2c0)

As you can see there is nothing interesting on the site hompage

so, checking ``robots.txt`` on the site shows this endpoints.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/f7562883-772b-4a3f-b4bd-6a17fcc40c91)

checking it one after the other gives nothing except the ``comingreallysoon`` directory

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/c06341fd-9c65-4bd9-876e-1ec7f01cfb3b)

And yeah there's is a note on the page telling us the location of their new website

``Welcome Dear Client! We've setup our latest website on /it-next, Please go check it out! If you have any comments or suggestions, please tweet them to @faketwitteraccount! Thanks a lot ! ``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/af7b0ed7-84f5-4eb4-9e1b-22c2f3cc3928)






