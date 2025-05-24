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


