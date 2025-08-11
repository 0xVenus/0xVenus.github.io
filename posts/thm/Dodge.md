## Dodge

### Difficulty: Medium

### OS: Linux

`Description: Test your pivoting and network evasion skills. `


Summary: Discovering vhosts and updating firewall rules to enable a port then to ssh access via private keys from the enabled port then to privilege escalation.

Let's get started


### STARTING WITH NMAP SCAN

<img width="1920" height="644" alt="image" src="https://github.com/user-attachments/assets/d6a4a1ff-3963-4a49-94b4-b61b9015b1cc" />

we have 3 ports open as you can see which are ssh,http and https

Accessing port 80 is forbidden. So, let's proceed to port 443 (https)

Recall from the nmap scan we have some vhosts exposed 

Add them to your /etc/hosts file

`10.10.234.171 dodge.thm www.dodge.thm blog.dodge.thm dev.dodge.thm touch-me-not.dodge.thm ball.dodge.thm netops-dev.dodge.thm`

The vhosts ain't accessbile i.e we are forbidden to access them. Except for the `netops-dev.dodge.thm`

Visiting the virtual host we have a blank page which is sus

<img width="1355" height="436" alt="image" src="https://github.com/user-attachments/assets/b3bb6875-c73e-4829-9049-4421696796db" />

Viewing the source (CTRL+U) we can see a js file. Checking the js file shows:
It sends an AJAX request (asynchronous HTTP request) to a file called `firewall10110.php` on the server, asking for data (via a GET request). 

<img width="1108" height="572" alt="image" src="https://github.com/user-attachments/assets/1997742b-b199-4470-9113-ac732cd36721" />

let's check whats really happening in the directory

<img width="1359" height="746" alt="image" src="https://github.com/user-attachments/assets/a9988158-875e-401d-844c-75dd57367514" />

so it's basically for updating firewall rules.

And yeah as we can see there are other ports which are not available or opened in our Nmap scan because it's blocked

Let's enable the port 

`sudo ufw allow 21`

<img width="1595" height="864" alt="image" src="https://github.com/user-attachments/assets/38d82176-36d6-4bea-a7e1-b56b24bea264" />

As you can it's now allowing connections which was denying earlier

so, let's re run nmap scan after updating the rule

<img width="1915" height="929" alt="image" src="https://github.com/user-attachments/assets/d6be2623-3e34-4c3f-965a-a7d6204f2e9b" />

Now we have a new open port which wasnt opened before. `port 21 FTP` which allows anonymous login

<img width="1158" height="468" alt="image" src="https://github.com/user-attachments/assets/77f05d7d-279f-4f34-baf5-50a82866ec3d" />

so listing all the contents on the server revealed an ssh directory which contains private keys

<img width="1914" height="893" alt="image" src="https://github.com/user-attachments/assets/1a1908b0-ee3d-45a4-b649-29dbb685a11c" />

As you can see we only have the permission to get the `authorized_keys and id_rsa_backup`

so, i downloaded the files to my local machine. Let's Read the `authorized_keys` file to know the user that owns the private key

<img width="1919" height="177" alt="image" src="https://github.com/user-attachments/assets/b8d63b72-def9-45af-aa6b-e66bcbda1a42" />

The user `challenger` owns the private key. So, let's ssh into the machine and with the private key (you dont need a passowrd to ssh)

`chmod 600 id_rsa_backup && ssh -i id_rsa_backup challenger@ip` then read the user.txt flag

<img width="1920" height="933" alt="image" src="https://github.com/user-attachments/assets/1833e0bd-dc71-46e9-ba1e-ed5d2d12d947" />

### PRIVILEGE ESCALATION

There's an encoded strings in the `/var/www/notes/api/posts.php` file

Looking at it you can tell it's in `base64`

so, decoding it revealed the user `cobra's passowrd`

<img width="1920" height="726" alt="image" src="https://github.com/user-attachments/assets/b47f2920-9a38-455d-8ab4-c604b66ccd00" />

```
challenger@thm-lamp:/var/www/notes/api$ echo "W3sidGl0bGUiOiJUby1kbyBsaXN0IiwiY29udGVudCI6IkRlZmluZSBhcHAgcmVxdWlyZW1lbnRzOjxicj4gMS4gRGVzaWduIHVzZXIgaW50ZXJmYWNlLiA8YnI+IDIuIFNldCB1cCBkZXZlbG9wbWVudCBlbnZpcm9ubWVudC4gPGJyPiAzLiBJbXBsZW1lbnQgYmFzaWMgZnVuY3Rpb25hbGl0eS4ifSx7InRpdGxlIjoiTXkgU1NIIGxvZ2luIiwiY29udGVudCI6ImNvYnJhIFwvIG16NCVvN0JHdW0jVFR1In1d" | base64 -d
[{"title":"To-do list","content":"Define app requirements:<br> 1. Design user interface. <br> 2. Set up development environment. <br> 3. Implement basic functionality."},{"title":"My SSH login","content":"cobra \/ mz4%o7BGum#TTu"}}
```

Now we can switch to user cobra since we have the password 

`cobra: mz4%o7BGum#TTu`

`su cobra` and paste the password. simple `sudo -l` showed that the user cobra can run `/usr/bin/apt` as root

<img width="1753" height="192" alt="image" src="https://github.com/user-attachments/assets/dd97933f-18ae-4ab9-97a9-8e61bd487b03" />

Quick search on gtfobins showed we can gain root by running this command `sudo apt update -o APT::Update::Pre-Invoke::=/bin/sh`

And now we have fully compromised the server 

<img width="1811" height="666" alt="image" src="https://github.com/user-attachments/assets/09231580-9a33-402c-9b1b-ccd7d7f2b700" />



#Firewall #UpdateRules #ftp #ssh #PrivilegeEscalation




















