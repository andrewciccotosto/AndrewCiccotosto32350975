# Setting up the Web Server to get ready to host the website
#### If you have not yet used SSH to connect to the AWS Ubuntu server, go back one step  
  
I am using Apache2 to host the website - this will need to be downloaded from the command line onto our AWS Ubuntu Server
  
First, you need to run "sudo apt update"  
  
Once completed, you will need to download and install Apache2 using "sudo apt install apache2". When prompted, enter "Y" and execute.  

To verify that this has successfully launched a web server, copy the IPv4 address of the AWS Ubuntu machine and type it into a web browser. If the Apache2 default page is loaded, this has been successfully launched.

# Installing NMAP
Nmap is used to identify which ports are open at a specific IP Address. As we are setting up a web server via AWS, and we will be remoting into the computer, we will need port 22 open. This is the SSH port. When configuring the machine in the previous step, this port should be open, as well as port 80 (HTTP), which is used for hosting the web server and allowing others to visit the web server, and port 443 (HTTPS), which is the secure version of HTTP. We will require these ports to be opened for the webserver, and Nmap will allow us to see which ports are opened.

* Open terminal and SSH into your AWS Ubuntu Server.
* Type in "sudo apt update" and then "sudo apt install nmap" and enter "Y" when advised.
Nmap should now be installed. To test this use:
* nmap (the computer's IP address)
You should then see which ports are open and which are closed.
If any ports are closed, enter the following:  
        **sudo ufw allow (port number)/tcp **   
What we just did was create a rule for that specific port allowing traffic. When you Nmap the computer's IP address again, the specific port should now be open.
