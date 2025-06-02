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

