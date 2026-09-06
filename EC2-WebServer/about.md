\# EC2 Web Server — Complete Documentation



\## 1. Project Overview



This project demonstrates how to host a static website on an Amazon EC2 instance using Apache HTTP Server.



An EC2 instance was launched using Amazon Linux and configured with Apache HTTP Server. A custom HTML webpage was created and placed in the Apache web server directory. The website was then accessed through the EC2 instance's public IPv4 address.



\## 2. Objective



The main objective of this project is to learn how to launch and configure an Amazon EC2 instance, connect to it using SSH, install and configure Apache HTTP Server, and host a static HTML website using the EC2 instance's public IPv4 address.



\## 3. AWS Services Used



\### Amazon EC2



Amazon EC2 (Elastic Compute Cloud) was used to create and run the virtual server that hosts the website.



\### Security Groups



A Security Group was used to control inbound traffic to the EC2 instance.



The following inbound rules were configured:



| Type | Protocol | Port | Source |

|---|---|---:|---|

| SSH | TCP | 22 | My IP |

| HTTP | TCP | 80 | Anywhere (0.0.0.0/0) |



\### SSH — Port 22



Port 22 was allowed only from \*\*My IP\*\* so that the EC2 instance could be accessed through SSH from my computer.



\### HTTP — Port 80



Port 80 was allowed from \*\*Anywhere (`0.0.0.0/0`)\*\* so that the hosted website could be accessed through the internet using the EC2 instance's public IPv4 address.



\## 4. Architecture



The project uses a simple architecture where a Windows PC is used to connect to the EC2 instance through SSH, while a web browser accesses the hosted website through HTTP.



!\[EC2 Web Server Architecture](architecture.png)



\## 5. EC2 Instance Setup



An Amazon EC2 instance was launched to act as the web server.



\### Instance Configuration



\- \*\*Instance Name:\*\* `My-Web-Server`

\- \*\*Operating System:\*\* Amazon Linux

\- \*\*Key Pair:\*\* `my-web-key`

\- \*\*Key File:\*\* `my-web-key.pem`

\- \*\*Inbound Traffic:\*\*

&#x20; - SSH — Port 22 — My IP

&#x20; - HTTP — Port 80 — Anywhere (`0.0.0.0/0`)



The EC2 instance was successfully launched with the above configuration.



\### Key Pair Details



A key pair was used to securely connect to the EC2 instance through SSH.



\- \*\*Key Pair Name:\*\* `my-web-key`

\- \*\*Private Key File:\*\* `my-web-key.pem`



When the EC2 instance was created, the `my-web-key` key pair was selected. The private key file `my-web-key.pem` was downloaded to the local Windows computer.



The `.pem` file is required when establishing the SSH connection to the EC2 instance. It acts as the private key for authentication.



The private key must be kept secure and should never be uploaded to GitHub or shared with anyone.



\## 6. Connecting to EC2 Using SSH



After the EC2 instance was launched, I connected to it from my Windows PC using SSH through Windows PowerShell.



The connection was made using the private key file `my-web-key.pem` and the EC2 instance's public IPv4 address.



\### SSH Command



```bash

ssh -i "my-web-key.pem" ec2-user@YOUR\_PUBLIC\_IP

```



After connecting to the EC2 instance through SSH, the system packages were updated using the `dnf` package manager.



\### Command



```bash

sudo dnf update -y

```



\## 7. Installing Apache HTTP Server



Apache HTTP Server was installed on the EC2 instance to act as the web server and serve the HTML website.



\### 7.1 Installing Apache



The Apache HTTP Server package was installed using the `dnf` package manager provided by Amazon Linux.



```bash

sudo dnf install -y httpd

```



\- `sudo` — Runs the command with administrator privileges.

\- `dnf` — Package manager used by Amazon Linux.

\- `install` — Installs a software package.

\- `-y` — Automatically confirms the installation.

\- `httpd` — Package name for Apache HTTP Server.



\### 7.2 Starting Apache



After installing Apache, the Apache service was started using:



```bash

sudo systemctl start httpd

```



This starts the Apache HTTP Server immediately, allowing it to begin serving web pages.



\### 7.3 Enabling Apache



Apache was enabled so that the web server starts automatically whenever the EC2 instance is restarted:



```bash

sudo systemctl enable httpd

```



Enabling the service is different from starting it. The `start` command runs Apache now, while `enable` configures Apache to start automatically during future system boots.



\### 7.4 Checking Apache Status



The status of the Apache service was checked using:



```bash

sudo systemctl status httpd

```



This command displays information about the Apache service, including whether it is currently running.



The Apache service was successfully started and was running on the EC2 instance.



\## 8. Web Server Directory



After installing Apache, the website files were placed in Apache's default web root directory.



\### 8.1 Navigating to the Web Directory



The Apache web root directory is:



```bash

/var/www/html

```



I navigated to this directory using:



```bash

cd /var/www/html

```



\- `cd` — Changes the current directory.

\- `/var/www/html` — The default directory from which Apache serves website files.



\### 8.2 Creating the Website File



Inside `/var/www/html`, an `index.html` file was created using the `nano` text editor:



```bash

sudo nano index.html

```



The `index.html` file contains the HTML code for the website.



Apache uses `index.html` as the default webpage when a user accesses the server through a web browser.



\### 8.3 Verifying the File



After creating the file, its contents were checked using:



```bash

cat index.html

```



The command displays the contents of `index.html` directly in the terminal, allowing the HTML code to be verified.



\## 9. Website Code



The website was created using HTML and saved as `index.html` inside the Apache web root directory.



\### 9.1 HTML Code



The following HTML code was used for the website:



```html

<html>

<head>

&#x20;   <title>My EC2 Website</title>

</head>



<body>



&#x20;   <h1>Hello from AWS EC2!</h1>



&#x20;   <p>Hii, this is Bishwaroop Banerjee and you are in my first AWS website hosted using AWS EC2.</p>



</body>

</html>

```



\### 9.2 Saving the Website



The HTML code was saved in:



```text

/var/www/html/index.html

```



Apache serves the `index.html` file from this directory when the EC2 instance receives an HTTP request.



\## 10. Accessing the Website



After Apache was installed, configured, and the `index.html` file was created, the website was accessed through the EC2 instance's public IPv4 address.



\### 10.1 Getting the Public IPv4 Address



The EC2 instance's \*\*Public IPv4 address\*\* was obtained from the EC2 instance details in the AWS Management Console.



\### 10.2 Opening the Website



The public IPv4 address was entered into a web browser using the HTTP protocol:



```text

http://YOUR\_PUBLIC\_IP

```



For example:



```text

http://3.XX.XX.XX

```



The browser sent an HTTP request to the EC2 instance on \*\*port 80\*\*.



The Security Group allowed HTTP traffic on port 80, so the request reached the Apache web server.



Apache then served the `index.html` file located at:



```text

/var/www/html/index.html

```



The webpage was successfully displayed in the browser.



\### 10.3 Result



The website was successfully hosted on the Amazon EC2 instance and accessed through its public IPv4 address.



\### Website Screenshot



!\[Hosted Website](screenshots/website.png)



\## 11. Cost Considerations



Amazon EC2 is a paid service, and the cost depends on the instance type, region, usage duration, and other resources associated with the instance.



For this project, the EC2 instance was used for learning and experimentation. To avoid unnecessary charges, the instance can be stopped when it is not being used.



\### Stopping the EC2 Instance



When the project is not being used, the EC2 instance can be stopped from the AWS Management Console.



Stopping the instance stops the compute usage, but some associated resources may still incur charges depending on the configuration.



The EC2 instance can be started again when the project needs to be continued.



\### Public IPv4 Address



The EC2 instance's public IPv4 address may change when the instance is stopped and started again.



Therefore, the new public IPv4 address should be checked in the EC2 console before accessing the website after restarting the instance.



\## 12. Conclusion



This project provided hands-on experience with hosting a static website using Amazon EC2.



An EC2 instance was launched using Amazon Linux and configured with Apache HTTP Server. SSH was used to connect to the instance, and the required Apache web server software was installed using the `dnf` package manager.



A custom `index.html` webpage was created and placed in Apache's default web root directory:



```text

/var/www/html/index.html

```



The Security Group was configured to allow SSH traffic on port 22 from my IP address and HTTP traffic on port 80 from anywhere.



Finally, the website was successfully accessed through the EC2 instance's public IPv4 address.



This project helped build a practical understanding of Amazon EC2, Security Groups, SSH, Linux commands, Apache HTTP Server, and basic web hosting on AWS.

