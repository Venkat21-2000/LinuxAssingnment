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

after saving this run command `sudo systemctl restart postfix`<br>

Step 4 : Install mailutils<br>
`sudo apt install mailutils`<br>

Step 5 : Send a mail using the following command<br>
`mail -s 'enter a subject' resever@gmail.com`<br>
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

In this method we add `describe` as alias of `ls` command in `/home/sigmoid/.bashrc` file write as following <br>
`alias describe="ls"`<br>
at the end of the file and save it. Then restart the session now the `describe` will do desired task.

#### Method 2 : Creating custom command
In this method first we create a file by name describe in `/usr/local/bin/` location. Inside this file write following command.
```bash
#!/bin/bash
ls
```
After saving this file we need to executable permission to the above file. <br>
`chmod a+x describe`<br>
The above command will enable all the users in the shell to usse describe as command to list the files in current directory.

## Question 4
#### Users can put a compressed file at any path of the linux file system. The name of the file will be research and the extension will be of compression type, example for gzip type extension will be .gz. You have to find the file and check the compression type and uncompress it.
##### Method 1
Go to `/usr/local/bin/` directory using `cd` commmand and create a file  by name uncompress the  write and save  following  script<br><br>     

```bash

#!/bin/bash

# Find all compressed research files
files=$(find / -name "research.*" -type f 2>/dev/null)

for file in $files; do
    file_extension=$(file $file | grep -Po "(?:gzip|bzip2|zip|xz)")
    if [[ $file_extension == "gzip" ]]
    then
        gunzip $file
	echo "The file is  found in path $file and compression type is $file_extension"
    elif [[ $file_extension == "xz" ]]
    then
        unxz $file
        echo "The file is  found in path $file and compression type is $file_extension"
    elif [[ $file_extension == "bzip2" ]]
    then
        bunzip2 $file
        echo "The file is  found in path $file and compression type is $file_extension"
    elif [[ $file_extension == "zip" ]]
    then
        unzip $file
        echo "The file is  found in path $file and compression type is $file_extension"
    else
        echo "The file is not compressed"
    fi
done
```

after this  ececute `sudo chmod a+x uncompress` command to give executable permission.<br>
Now we can use uncompress as a command to find and uncompress the file.<br><br>
##### Method 2
we can also use following command to find and uncompress of one type of compression <br><br>
`find / -name "*research.*" -exec sh -c 'gunzip -d "{}" \; 2>/dev/null`<br><br>	
in the above command by replacing sutaible unzip type we can uncompress different types.

## Question 5 
#### Configure your system in such a way that any user of your system creates a file then there should not be permission to do any activity in that file.
Add umask value 0777 at the end of  bash.bashrc file
`umask 0777`
 
## Question 6
#### Create a service with the name showtime , after starting the service, every minute it should print the current time in a file in the user home directory.
Create a service by name `showtime.service` in `/etc/systemd/system` and write a service here.<br>

Step 1 :<br>
```bash
[Unit]
Description=Linux Assingnment
After=network.target

[Service]
WorkingDirectory=/home/sigmoid/Desktop/
ExecStart=/home/sigmoid/Desktop/showtime.sh


[Install]
WantedBy=multi-user.target
```
The above code snippet will create a service.

Step 2 : create  a shell script to record time.
```bash
#!/bin/bash



while true;
do
	date >> /home/sigmoid/showtime.log
	sleep 60
done
```
Then give the script executable permission using `chmod a+x showtime.sh`.<br>
The above script will write current date and time to `showtime.log` which is created in home directory.

Then before starting the service we have to enable it.<br>
To enable we use `sudo systemctl enable showtime.service`<br>
To start the service : `sudo systemctl start showtime.service`<br>
To know status of service : `sudo systemctl status showtime.service`<br>
To Stop the service : `sudo systemctl stop showtime.service`<br>

















 













