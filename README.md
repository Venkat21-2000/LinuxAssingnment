# LinuxAssingnment
## Question 1
### Configure SMTP in Localhost
Step 1 : Install Postfix

`$sudo apt install postfix`

Step 2 :After that the installation will start and the postfix window will open. And we have to select some options on that window.<br>
1. select internet site and enter tab and enter enter.<br>
2. enter custom mail like ex: host.example.com<br>

Step 3 : After complition of installation we have to make changes in main.cf file present in path `/etc/postfix/main.cf`<br>

`cd /etc/postfix`<br>
`sudo nano main.cf`<br><br>
after this scroll down to bottom of file and change the line<br>
`inet_interfaces = all` to `inet_interfaces = loopback-only`<br>

Step 4 : Install mailutils<br>
`sudo apt install mailutils`<br>

Step 5 : Send a mail using the following command<br>
`echo mail -s 'enter a subject' resever@gmail.com`<br>
The above command will prompt to add CC and subject of mail. To end the edit mode and send the email use `Ctrl+D`

## Question 2
### Create a user in your localhost, which should not be able to execute the sudo command.
<br>

We can create a new user using `usradd` command as root user. <br>
Whenever we create  a user in linux, by default it will not have sudo access. To ensure that even with chmod the use should have sudo access we can add the user to `nosudo` group. We can do that by executing following command.<br>
`sudo usermod -aG nosudo <username>`<br><br>

## Question 3 
### Configure your system in such a way that when a user type and executes a describe command from anywhere of the system it must list all the files and folders of the user's current directory.

#### Method 1 : Using alias

In thus method we add `describe` as alias of `ls` command in `/home/sigmoid/.bashrc` file write as following <br>
`alias describe="ls"`<br>
at the end of the file and save it. Then restart the session now the `describe` will do desired task.

#### Method 2 : Creating custom command
In this method first we create a file by name describe in `/usr/local/bin/` location. Inside this file write following command.
```bash
#!/bin/bash
ls
```
After saving this file we need to executable permission to the above file. 
`chmod a+x describe`<br>
The above command will enable all the users in the shell to usse describe as command to list the files in current directory.

## Question 4










 













