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

# Setting up the Web Server to get ready to host the website
#### If you have not yet used SSH to connect to the AWS Ubuntu server, go back one step  
  
I am using Apache2 to host the website - this will need to be downloaded from the command line onto our AWS Ubuntu Server
  
First, you need to run "sudo apt update"  
  
Once completed, you will need to download and install Apache2 using "sudo apt install apache2". When prompted, enter "Y" and execute.  

To verify that this has successfully launched a web server, copy the IPv4 address of the AWS Ubuntu machine and type it into a web browser. If the Apache2 default page is loaded, this has been successfully launched.

## Installing NMAP
Nmap is used to identify which ports are open at a specific IP Address. As we are setting up a web server via AWS, and we will be remoting into the computer, we will need port 22 open. This is the SSH port. When configuring the machine in the previous step, this port should be open, as well as port 80 (HTTP), which is used for hosting the web server and allowing others to visit the web server, and port 443 (HTTPS), which is the secure version of HTTP. We will require these ports to be opened for the webserver, and Nmap will allow us to see which ports are opened.

* Open terminal and SSH into your AWS Ubuntu Server.
* Type in "sudo apt update" and then "sudo apt install nmap" and enter "Y" when advised.
Nmap should now be installed. To test this use:
* nmap (the computer's IP address)
You should then see which ports are open and which are closed.
If any ports are closed, enter the following:  
        **sudo ufw allow (port number)/tcp **   
What we just did was create a rule for that specific port allowing traffic. When you Nmap the computer's IP address again, the specific port should now be open.

