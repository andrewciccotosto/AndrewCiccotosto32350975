# Creating the Web Proxy
Now is the time to create the web proxy. At this point, there should be a DNS with an "A" record pointing to our public IPv4 address, as well as a digital certificate.  
Currently, if you go to your DNS, it should be displaying the Apache2 Default page, as we have not yet edited the "index.html" file. This is a good start, as this is showing that our web server is still able to be accessed and is displaying what it should be displaying. The next task is to create the Web-Based Proxy server, which allows a user to type in a URL (e.g. https://whatsmyip.com), and the destination URL will appear at the end of the URL of the Web-Based proxy server. The user will be using the web server created to hide their own IP address and use the IP address of the web server.

Firstly, open a terminal and SSH connect to the web server as per the above. As the DNS you purchased is pointing to the IPv4 address, you should now be able to type in:
* ssh -i "yourpemkeyname.pem" ubuntu@DNS
  
When writing this, I am able to SSH connect to the webserver using ssh -i "yourpemkeyname.pem" ubuntu@andrewciccotosto.com

Once connected, you will need to locate the index.html file
* In terminal, type in "cd /var/www/html/"

This should now bring you to the location "/var/www/html".  
If you type in ls, there should be a file called "index.html" To change the web page that is visible to the public, we will need to edit this.
* Type in: "sudo nano index.html" - This is giving us superuser access to edit the index.html file, which is the home page for the website.

Now, we are going to want to remove all the default Apache2 HTML code. The website we are creating is very basic, so not much code is needed. 

