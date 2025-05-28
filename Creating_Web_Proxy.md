# Creating the Web Proxy
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
* Type in sudo https://raw.githubusercontent.com/andrewciccotosto/AndrewCiccotosto32350975/main/gplv3-with-text-136x68.png
  
You have just downloaded the following image into the /html directory: ![gplv3-with-text-136x68](https://github.com/user-attachments/assets/e0486820-458f-4742-9d68-696f5233dd3e)  
  
Lets rename that to gplv3.png using "mv gplv3-with-text-136x68.png gplv3.png"  
  
Next image we are going to download is the logo

* Type in sudo https://raw.githubusercontent.com/andrewciccotosto/AndrewCiccotosto32350975/main/Untitled.png
Both images are now saved in the /var/www/html directory, as these will be used later - It is easier to save in this directory, otherwise, you will need to type the full directory every time you would like to use the image in your code.


## Editing the index.html file
If you type in ls, there should be a file called "index.html" To change the web page that is visible to the public, we will need to edit this.
* Type in: "sudo nano index.html" - This is giving us superuser access to edit the index.html file, which is the home page for the website.  

Now, we are going to want to remove all the default Apache2 HTML code. The website we are creating is very basic, so not much code is needed.  

Once all the code is removed, we are going to start writing the code for the web-based proxy server.  

Use the below: 

```
?php
 
 
if (!isset($_GET['url'])) {
?>
<title>Andrews Web Based Proxy</title>
<img src="Untitled.png" alt="Andrew's Web Based Proxy" />
<form>
  <input name="url" placeholder="Enter your destination - The protocol is needed. E.g https://whatsmyip.com" style="width:700px;" />
  <button>Enter</button>
</form>
 
<img src="gplv3.png" alt="GPLV3 License" />
 
<?php
    exit;
}
 
 
$url = $_GET['url'];

$page = @file_get_contents($url);
 
echo $page ? $page : "Page not found - ensure that the protocol is entered and try again"
 
?>
 
<a href="https://andrewciccotosto.com">
<button>Go Back</button>
</a>
```

Once copied in, you will then want to:
* Click "Ctrl + X" to exit.
* "Y"
* When asking "File name to write" type in "index.php" as we need to change the file type from HTML to PHP to allow the PHP to be correctly read.




To better understand, I have provided information of certain lines and what they are achieving within the code  

```
"if (!isset($_GET['url']))"  
"$url = $_GET['url'];"
```

The above lines in the code are PHP code, not HTML. The "$url = $_GET['url'];" line used when a user types in the URL into the form, and works with the if (!isset($_GET['url'])) line. If there is no url typed in, the "If"
line will not run. This will show the web page first, and then when a user clicks "Enter", the "If" line will start to work.  
This also 

```
$page = @file_get_contents($url);
echo $page;
```
The above line works when the user presses enter. The "@" symbol is forcing the page to load and does not advise of any errors. This line is the start of what causes the destination URL to appear after the URL of the web-based proxy server. The "echo" line then completes the job and results in the following: https://andrewciccotosto.com/?url=https%3A%2F%2Fwhatsmyip.com.  

```
<img src="Untitled.png" alt="Andrew's Web Based Proxy" />
<img src="gplv3.png" alt="GPLV3 License" />
```
The above lines are placing the images that are saved in the /html/ directory onto the webpage - They do not require the full directory as they are saved into the same file as the index.php file.



This is inspired by Joshdick (n.d) - Referencing at the end of the document.  


