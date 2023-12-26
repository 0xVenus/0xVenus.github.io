<h2>Exploiting SQLi without any SQL error in output</h2>

Hi hackers,

I will be showing you how to exploit SQLI when there are no SQL errors in outputs(tricky but simplified)

let's get started

let's assume our target is https://target.com

visiting the target page

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/06b1f5f2-d024-471f-a5bf-8a8af33fff1a)

then let's confirm the SQLi vulnerability by adding a single quote to the parameter value

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/0aa95256-4a7b-4148-9c08-327a416a4f03)

As you can see we've no sql injection error when i added a single quote, but notice the contents on the page are missing(compare both before and after adding a single quote)

this shows SQLI is possible

so, let's balance the url by appending a comment(url balancer) to the parameter value.

As you can see we have the normal page load after adding the comment ``--+-``  after the parameter value

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/789e1e84-16fd-4787-b0d6-04e2be93f5d7)

let's proceed by counting the number of columns present in the DB using the ``order by`` query

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/81541d07-6547-4208-88cc-ceefdf79a7ef)

``order by 1`` loads the normal page

so, keep increasing the number till you have the page with removed contents

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/09431fc0-0d04-4677-beff-74b7591f7f7b)

order by 19 gave the page with removed contents which means there are 18 columns in the DB

let's proceed to getting the vulnerable column 

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/3036036f-de61-42a1-b72e-8638cdceb1fd)

```https://target.com/page.php?pe=-36' union select 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18--+-```

column 9 is the vulnerable coulmn where we can inject our queries for dumping t5he datasbase








 



