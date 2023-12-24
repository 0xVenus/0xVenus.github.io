<h2>UNION BASED SQL INJECTION(manual)</h2>

HERE I SHOWCASE HOW TO PERFORM A BASIC UNION BASED SQL INJECTION (MANUALLY)

KINDLY CHECK NEXT POST FOR ADVANCED UNION BASED SQLI WHERE I SHOWED HOW TO BYPASS WAFS AND FILTERS

```
Performing a Union-Based SQL Injection attack manually involves injecting a crafted payload into an input field or parameter to manipulate a SQL query and retrieve unauthorized data from the database. Please note that attempting SQL injection on systems you don't own or have explicit permission to test is illegal and unethical. Only perform these actions in a controlled, legal environment with proper authorization.

```

Target: https://testphp.vulnweb.com/ (intentionally vulnerable site created for testing purpose)

**STEP 1:**

``Finding the injection point: we can simply find the injection point of a site by dorking for parameters with value``

dork example: ``site:testphp.vulnweb.com inurl:php?``. There are many dorks online you can search for more.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/71e2cbe6-2ad8-4704-b9f3-58d3157b6528)

clicking on any of those pages in the result should reveal the directory with parameter.

![image](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/58b964c7-9ede-40cd-8e2a-d4d19d435995)

As you can see we have a parameter and a value which we can then confirm the vulnerabilty



