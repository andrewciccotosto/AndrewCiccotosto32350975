# Setting up the Web Server to get ready to host the website
#### If you have not yet used SSH to connect to the AWS Ubuntu server, go back one step  
  
I am using Apache2 to host the website - this will need to be downloaded from the command line onto our AWS Ubuntu Server
  
First, you need to run "sudo apt update"  
  
Once completed, you will need to download and install Apache2 using "sudo apt install apache2". When prompted, enter "Y" and execute.  

To verify that this has successfully launched a web server, copy the IPv4 address of the AWS Ubuntu machine and type it into a web browser. If the Apache2 default page is loaded, this has been successfully launched.
