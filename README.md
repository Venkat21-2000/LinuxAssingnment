# LinuxAssingnment
## Question 1
Configure SMTP in Localhost
Step 1 : Install Postfix

`$sudo apt install postfix`

Step 2 :After that the installation will start and the postfix window will open. And we have to select some options on that window.<br>
1. select internet site and enter tab and enter enter.<br>
2. enter custom mail like ex: host.example.com<br>
Step 3 : After complition of installation we have to make changes in main.cf file present in path `/etc/postfix/main.cf`<br>

```cd /etc/postfix`
`sudo nano main.cf```
after this scroll down to bottom of file and change the line
`inet_interfaces = all` to `inet_interfaces = loopback-only`




 














<br><br>
2nd step: After that the installation will start and the postfix window will open. And we have to select some options on that window as followes<br>
    1. select internet site and enter tab and enter enter.<br>
    2. enter custom mall like ex: host.example.com<br><br>
3rd step: After complition of installation we have to make changes in main.cf file present in path /etc/postfix/main.cf<br>
   
cd /etc/postfix
<br>
     
sudo nano main.cf
<br>
         after this scroll down to bottom of file and change the line <br>
     
inet_interfaces = all
to  
inet_interfaces = loopback-only
<br><br>
4th step: Is to install mailutils.<br>
sudo apt install mailutils
<br><br>
5th step: Send a mail using the following command<br>
echo 'Enter a mail body here' | mail -s 'enter a subject' resever@gmail.com
