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

# Obtaining and implementing a DNS

## Obtaining a DNS using Amazon Route 53
* First, head to AWS and log in via the Root user login.  
* Once logged in, go to the 9-square symbol ![image](https://github.com/user-attachments/assets/11febb89-4562-4080-bba7-30e3877e069b) in the top left-hand corner and navigate to "Route 53"  
* Scroll down and select "Registered Domains", and then select "Register Domains" in the top right corner.  
* Enter the domain name that you wish to use - in this scenario, it is "andrewciccotosto.com". Note that different Top-Level Domains (TLDs) range in pricing; pick an appropriate one.  

## Creating an A record
Creating an "A record" for the DNS is essentially linking the Public IP address to the created domain name so that the visitors only have to type in your domain name. To do this:

* When the domain has been registered, go to "Hosted Zones" and click on the registered domain name.
* Create a record for the chosen domain name
* Choose "Simple routing" and click next
* Click "Define simple record" and make sure that the record type is "A"
* Enter the public IP address under "Route Traffic to"
* Once completed, click define simple record
When visitors type in your DNS, this should now route to the public IP Address
# Obtaining a digital certificate  

Once all the above steps have been completed, you will need to obtain a digital certificate for the website that is being hosted. This ensures that the connection to the website is secure via the HTTPS port (443)  

To obtain a digital certificate (SSL/TLS protocol), LetsEncrypt is going to be used. Steps to obtaining the certificate are below:

* SSH into your AWS Ubuntu server and install snapd using the following: sudo apt install snapd
* Once installed, we will need to install Certbot using: sudo snap install --classic certbot (Please note that this may take a while)
After Certbot has been installed, a certificate needs to be generated. Follow below:
* In terminal, type in: "sudo certbot --apache"
* You will be asked to enter an email address. Click enter to skip
* Type in "Y" to agree to the Terms of Service
* Enter your domain name that was created in the previous step - This should be the one with the "A Record" pointing towards the public IPv4 address of your AWS Ubuntu Server
* Once entered, to test if this has worked, head to your webserver via the domain name (andrewciccotosto.com) and this should be using the HTTPS:// now. Example shown below
* ![image](https://github.com/user-attachments/assets/d3313a40-bc66-44a5-a6a0-3b50630b3137)
# Editing the HTML
Now is the time to create the web proxy. At this point, there should be a DNS with an "A" record pointing to our public IPv4 address, as well as a digital certificate.  
Currently, if you go to your DNS, it should be displaying the Apache2 Default page, as we have not yet edited the "index.html" file. This is a good start, as this is showing that our web server is still able to be accessed and is displaying what it should be displaying. The next task is to create the Web-Based Proxy server, which allows a user to type in a URL (e.g. https://whatsmyip.com), and the destination URL will appear at the end of the URL of the Web-Based proxy server. The user will be using the web server created to hide their own IP address and use the IP address of the web server.

Firstly, open a terminal and SSH connect to the web server as per the above. As the DNS you purchased is pointing to the IPv4 address, you should now be able to type in:
* ssh -i "yourpemkeyname.pem" ubuntu@DNS
  
When writing this, I am able to SSH connect to the webserver using ssh -i "yourpemkeyname.pem" ubuntu@andrewciccotosto.com

Once connected, you will need to locate the index.html file
* In terminal, type in "cd /var/www/html/"

This should now bring you to the location "/var/www/html". 
  
Before we start editing the html code, we are going to need to download images to the /var/www/html location.
First one that is needed is the GPLv3 License logo that will be displayed.
* Type in sudo wget https://raw.githubusercontent.com/andrewciccotosto/AndrewCiccotosto32350975/main/gplv3.png
  
You have just downloaded the following image into the /html directory: ![gplv3-with-text-136x68](https://github.com/user-attachments/assets/e0486820-458f-4742-9d68-696f5233dd3e)  
  
Lets rename that to gplv3.png using "mv gplv3-with-text-136x68.png gplv3.png"  
  
Next image we are going to download is the logo

* Type in sudo wget https://raw.githubusercontent.com/andrewciccotosto/AndrewCiccotosto32350975/main/logo.png
Both images are now saved in the /var/www/html directory, as these will be used later - It is easier to save in this directory, otherwise, you will need to type the full directory every time you would like to use the image in your code.


## Editing the index.html file
If you type in ls, there should be a file called "index.html" To change the web page that is visible to the public, we will need to edit this.
* Type in: "sudo nano index.html" - This is giving us superuser access to edit the index.html file, which is the home page for the website.  

Now, we are going to want to remove all the default Apache2 HTML code. The website we are creating is very basic, so not much code is needed.  

Once all the code is removed, we are going to start writing the code for the web-based proxy server.  

```
<?php 
if (isset($_GET['go'])){
        $whatsmyip=file_get_contents("https://whatsmyip.com");
}
?>
<html>
<title>Andrew's Web Based Proxy</title>
<br>
<img src="logo.png" alt="Andrew's web based proxy"/>
<br>
<p> Enter your destination below - IP Address will be:54.66.244.57 - The IPv4 address of this server </p>
<br>
<p> Only https://whatsmyip.com will work 
// Could not understand how other creators codes on how to 
// get the file_get_contents line to work for all websites
<form>
<input type="url" required="required" placeholder="https://whatsmyip.com"/>
<button name="go">Go</button
// button named "go" to align with the  "if" at the top of the code"
<br>
<br>
<img src="gplv3.png"/>
</html>
<?php 
echo $whatsmyip
// References
// Manual. (n.d.). Www.php.net. https://www.php.net/manual/en/function.file-get-contents.php
// W3Schools. (2019). HTML Input Types. W3schools.com. https://www.w3schoolscom/html/html_form_input_types.asp
// https://github.com/joshdick/miniProxy/blob/master/miniProxy.php
?>
```
You should now see the website up and running when you go to your domain name on a web browser.
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
