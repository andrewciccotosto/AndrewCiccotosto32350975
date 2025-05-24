# Obtaining a digital certificate  

Once all the above steps have been completed, you will need to obtain a digital certificate for the website that is being hosted. This ensures that the connection to the website is secure via the HTTPS port (443)  

To obtain a digital certificate (SSL/TLS protocol), LetsEncrypt is going to be used. Steps to obtaining the certificate are below:

* SSH into your AWS Ubuntu server and install snapd using the following: sudo apt install snapd
* Once installed, we will need to install Certbot using: sudo snap install --classic certbot (Please note that this may take a while)
* 
