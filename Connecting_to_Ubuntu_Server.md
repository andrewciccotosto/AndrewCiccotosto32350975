# Connecting to your AWS Ubuntu Server
Now we need to connect to the newly created AWS Ubuntu Server using SSH.

#### Log onto your physical linux machine

##### Ensure you have changed permissions on the .pem key file to 400 otherwise you will unable to connect to your Ubuntu Server
* Open AWS EC2 as well as Terminal on your Linux machine
* Click on your instance and then click "Connect"
* Navigate to "SSH Client" and see below image for what is needed to copy into terminal (Please note that the SSH example (as highlighted below) will differ due to the Public IPv4 Address and the .pem key that was created earlier)

  
  
![image](https://github.com/user-attachments/assets/6d19c3e2-541a-4fc4-abaf-c7fa8a093ca5) 

Terminal should now be asking if you wish to continue connecting - Type "Yes"  
You should now be connected to your Web Server - This is known by the command line no longer having the physical computers name or location but the username of the cloud server
