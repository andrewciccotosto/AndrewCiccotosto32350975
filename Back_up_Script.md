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

This script is creating a ZIP file with the current date as the name of the ZIP file and saving into /home/ubuntu/htmlbackup.  

### Running the script
Before the script is run, we need to install ZIP to allow the file to be compressed when creating the backup.  
* In terminal, type the following
```
sudo apt update
sudo apt install zip
```  
Once ZIP has been installed, we can test the script. 

### Testing the Script
In terminal, type in:
```
./backupscript
```
Navigate through to /home/ubuntu/htmlbackup and there should be a ZIP file with the current days' date as the file name, as shown:  
![8ee9cab2-2b5e-4a4b-b07c-648d843be4a4](https://github.com/user-attachments/assets/edace753-7127-42e6-a72f-3e4e5fa28c68)+

### Finishing touches

Now we are going to move the script to the /usr/bin directory. This will allow the script name to be typed into terminal from anywhere to be ran manually
```
sudo mv /home/ubuntu/htmlbackup /usr/bin/
```
Now we are going to schedule the script to run daily at 12pm to ensure that there is always a backup.

```
sudo nano /etc/crontab
```

Once the file has opened, you will see scripts that are already running automatically. Leave them, and you are going to navigate to the bottom and type in the following:
```
0 12   * * *   ubuntu  /usr/bin/backupscript
```
This is scheduling the script to run at 12pm daily, every day.



