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
