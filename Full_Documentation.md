# Creating and Launching an Ubuntu Server using Amazon Web Services

## Creating an Amazon Web Services (AWS) account 
Firstly, head to [Amazon Web Services](https://signin.aws.amazon.com/signup?request_type=register)
Create an account using your email address

## Launching your AWS Virtual Server
### Choosing your Server
* Once your account has been created, click on "Launch Instance" from the EC2 menu.  
* Use a Quick Start Amazon Machine Image of Ubuntu Server 24.04 - This is eligible for the "Free Tier".
Architecture is 64-bit   
* Instance type: t2.micro - This is more than sufficient for what we are hosting on the server, and is free tier eligible  

### Key pair (login) is required
* Select "Create new key pair"  
* Enter a name for your Key pair. For example, "Server_Project_ICT171" - Ensure the key file format is .pem  
* Select "Create Key Pair"
* Download your .pem key and save to the computer that you will be using to access your AWS Ubuntu machine

### Network Settings
* Select the "Edit" button in the right-hand corner
#### You will need three inbound security group rules
*   SSH - Ensure port is 22 - Source 0.0.0.0/0
*   HTTPS - Ensure port is 443 - Source 0.0.0.0/0
*   HTTP - Ensure port is 80 - Source 0.0.0.0/0

    
All other settings can remain as default. Once this has been completed, click "Launch Instance"

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
