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

### Network Settings
* Select the "Edit" button in the right-hand corner
#### You will need three inbound security group rules
*   SSH - Ensure port is 22 - Source 0.0.0.0/0
*   HTTPS - Ensure port is 443 - Source 0.0.0.0/0
*   HTTP - Ensure port is 80 - Source 0.0.0.0/0

    
All other settings can remain as default. Once this has been completed, click "Launch Instance"
