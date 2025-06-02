# Backup Script
Now, we need to create a backup script - This will allow us to always have a backup on the virtual machine incase of any mishaps. This will also be set to run daily at 12pm.  

### Creating the backup script
* Firstly, SSH into your virtual machine
* Make a directory called "backuphtml" by using the following
```
touch backuphtml
```
The permissions of the file need to be changed to allow for execution. Use the following
```
sudo chmod 777 backuphtml
```
And then we need to change the owner of the file to "Ubuntu"
```
sudo chown ubuntu backuphtml
```
Now the file should be able to be readable, writable and executable by all users, and the owner is "Ubuntu"  
Next, we need to edit the script

### Editing the script
To edit the script, use the following line in Terminal
```
nano backupscript
```
Once you are editing, we need to type in the following. What this will do is create a backup of the HTML file that is located in /var/www/ - This is where the web server index.php file is stored
```
#!/bin/bash
 
today=$(date +"%d_%m_%y")
sudo cp -R /var/www/html/ /home/ubuntu/htmlbackup/
zip -r $today.zip /home/ubuntu/htmlbackup/*
cp $today.zip /home/ubuntu/htmlbackup/
```
