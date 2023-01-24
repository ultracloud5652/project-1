# WEB STACK IMPLEMENTATION PROJECT
### IMPLEMENTATION OF LAMP STACK IN AWS
A **LAMP** stack is a bundle of four different software technologies that developers use to build websites and web applications. **LAMP** is an acronym for the operating system, *Linux*; the web server, *Apache*; the database server, *MySQL*; and the programming language, *PHP*.

Create an AWS account and I recommends that you create an IAM user for yourself for daily use of your resources.
Once you login into AWS successfully, you will see the main console with all the service listed as follows:

![Screen Shot 2023-01-23 at 3 41 57 PM](https://user-images.githubusercontent.com/117458922/214067870-a41ea075-3247-47f9-a52e-6057431fabf0.png)

Before creating an EC2 instance, it is a good practice to check and select a desired and closest region to you.
Choosing an AWS Region with close proximity to your user base location can achieve lower network latency. It can also increase communication quality, given that network packets have fewer exchange points to travel through. It is also good for security and regulatory compliance, Service Level Agreements (SLA), and most importantly the cost of resources you will be using.

![Screen Shot 2023-01-23 at 3 52 48 PM](https://user-images.githubusercontent.com/117458922/214070454-bae58f59-b43c-46d1-adaf-f396630ef332.png)

Navigate to Services and select EC2, then click on *Lauch Instance*

![Screen Shot 2023-01-23 at 4 05 44 PM](https://user-images.githubusercontent.com/117458922/214076953-b7059f0f-db74-4678-8549-8595a5a3820b.png)

Launch an "EC2" instance of t2.micro family with Ubuntu Server

![Screen Shot 2023-01-23 at 1 25 09 PM](https://user-images.githubusercontent.com/117458922/214077420-a490c35d-6824-4fc1-af66-09a7b4079151.png)
![Screen Shot 2023-01-23 at 1 23 13 PM](https://user-images.githubusercontent.com/117458922/214077712-804804e3-0d06-4eb4-ab17-aaf7c12c81e5.png)
![Screen Shot 2023-01-23 at 3 27 22 PM](https://user-images.githubusercontent.com/117458922/214077808-134196ff-92d7-484f-a345-9389f0a8280c.png)
![Screen Shot 2023-01-23 at 4 23 52 PM](https://user-images.githubusercontent.com/117458922/214078298-087ee066-0f92-4693-8cb2-c82939d8f454.png)

As shown above, be sure to create a security group which allows SSH remote connection to the server, and also create and download your private keypair which will be used to connect to your server.  If the keypair is lost, you will not be able to connect to your server ever again!

* Next step is to view the status of instance, click on your instance to view it. At this stage, you will see if your instance is running or still pending. mine is running, so now i can view my instance details

![Screen Shot 2023-01-23 at 3 27 22 PM](https://user-images.githubusercontent.com/117458922/214296738-32ce0eaa-d7bb-45b7-8c3e-8b0dc760dae6.png)

* Next step is to connect to my instance through SSH Client. In my own case, I am using the preinstalled Terminal on MacOS. If your system runs Windows or other operating system, you can decide to use MOBAXTERM or PUTTY or any other existing ones. And you need to connect using the public ip address or public DNS of the instance you want to establish remote connection with. Then select your instance name and click *Connect* at the top and navigate to *SSH Client* and follow the instructions under it.

![Screen Shot 2023-01-23 at 3 27 54 PM](https://user-images.githubusercontent.com/117458922/214301562-4575510c-cd11-49b7-a8f9-3f484b859f6a.png)

* The next thing is to open Terminal on my computer and establish SSH connection using the instructions in the above diagram.
Note that it is important to change directory to where my private keypair is downloaded to, and then run the command 'chmod 400 private key name' to make sure your key is not viewable to the public.

![Screen Shot 2023-01-23 at 3 28 58 PM](https://user-images.githubusercontent.com/117458922/214305876-ce184ec8-a01d-4994-bbc6-5af6af7de04b.png)
* Note that when prompted with the question 'Are you sure you want to continue connecting?', you should type in *yes*. If the connection is successful, you will see ubuntu@ip followed by an ip address, which will bw diiferent from mine.

So, back to the business of the day, which is to implement a LAMP stack. The name LAMP is an acronym of the following programs:
- Linux Operating System
- Apache HTTP Server
- MySQL database management system
- PHP programming language

### Below are steps that I used to implement a web solution using LAMP stack on Linux Ubuntu Server;

# Step 1 - Updating Linux Environment and Installing Apache2

* We need to update Linux and install Apache using Ubuntu’s package manager, apt:

```
sudo apt update
sudo apt install apache2
```

![Screen Shot 2023-01-23 at 3 30 18 PM](https://user-images.githubusercontent.com/117458922/214312437-2d5456bc-42bc-4ad2-83c5-3f850d77b81a.png)
![Screen Shot 2023-01-23 at 3 30 50 PM](https://user-images.githubusercontent.com/117458922/214312576-cc4fac0c-3cdc-4f57-9f70-a3e7f8d14577.png)
When prompted with question about the installation, reply with y, with means yes

* Use the following command to verify that apache2 is running as a Service on the server;

```
sudo systemctl status apache2
```
You should get something like this it the installation waas successful

![Screen Shot 2023-01-23 at 3 32 02 PM](https://user-images.githubusercontent.com/117458922/214313754-9a5d1eec-07e1-4f2b-9c01-b6c627aefd2f.png)

Before we can receive any traffic by our Web Server, we need to open TCP port 80 which is the default port that web browsers use to access web pages on the Internet

To open port 80, I went back to the instance, clicked on security, clicked on edit inbound rules and I added rules on port 80 for http and port 443 https and I saved the rules.

check out my output below:

![Screen Shot 2023-01-23 at 3 38 27 PM](https://user-images.githubusercontent.com/117458922/214314569-f2085b89-5fb4-4e33-9807-7cd9f40abfdd.png)

## Now, the server is up and running and we can access it both locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’).

* In other to verify that we can access it locally in our ubuntu shell and from the internet, use the command:

```
curl http://localhost:80
or
curl http://127.0.0.1:80
```

**You will see some strangely formatted test, do not worry, we just made sure that our Apache web service responds to ‘curl’ command with some payload.They look like what I have below;**

![Screen Shot 2023-01-23 at 3 33 02 PM](https://user-images.githubusercontent.com/117458922/214320377-beb1ba69-4d6e-4d1d-b140-be01c4e16e06.png)

* Open a web browser of your choice and try to access following url;

```
http://<Public-ip-address>:80
```

* **To retrieve your Public IP address, other than to check it in AWS Web Console, use the following command.**

```
$ curl -s http://169.254.169.254/latest/meta-data/public-ipv4
```

* If you see the following page, then your web server is now correctly installed and accessible through your firewall.

![Screen Shot 2023-01-23 at 3 37 21 PM](https://user-images.githubusercontent.com/117458922/214321782-596ca040-059a-46f3-9df2-12900a47e628.png)

# STEP 2 - Installing MySQL

### We need to install the database system to be able to store and manage data for our website. MySQL is a popular database management system used within PHP environments.

* To install mysql-server, run:

```
sudo apt install mysql-server -y
```
**note that the '-y' will skip the question "Do you want to continue?"
![Screen Shot 2023-01-23 at 4 39 46 PM](https://user-images.githubusercontent.com/117458922/214326299-963843cd-cdb9-4914-92ac-9a4711e03cce.png)


* After the installation it is recommended that we run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lockdown access to our database system.

* Start the interactive Script by running:


```
sudo mysql_secure_installation
```

* This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.


#### Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer Y for yes, or anything else to continue without enabling.

```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?
Press y|Y for Yes, any other key for No:
```

* If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.



### <p> If we enabled password validation, we’ll be shown the password strength for the root password we just entered and our server will ask if we want to continue with that password. If we are happy with our current password, enter Y for “yes” at the prompt:</p>



### For the rest of the questions, We press Y and hit the ENTER key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes we have made.

![Screen Shot 2023-01-23 at 4 45 10 PM](https://user-images.githubusercontent.com/117458922/214327890-8176ec95-a008-442a-8049-f30701490ffb.png)

when you are done, you will get this **output:** 

![Screen Shot 2023-01-23 at 4 46 53 PM](https://user-images.githubusercontent.com/117458922/214328121-5a4a4ecd-770c-4f8c-8b91-a9310a7d0748.png)

* When you're finished, test if you're able to login to the MySQL Console by running this command:

```
sudo mysql
```

![Screen Shot 2023-01-23 at 4 41 09 PM](https://user-images.githubusercontent.com/117458922/214328581-7a089fdb-39b0-4c0c-ace8-97d621a62e16.png)

* Use this command to exit the MySQL Console;

```
mysql> exit
```

#### Setting a password for the root MySQL account works as a safeguard, in case the default authentication method is changed from unix_socket to password. For increased security, it’s best to have dedicated user accounts with less privileges set up for every database, especially if we plan on having multiple databases hosted on our server.

### Our MySQL server is now installed and secured.


* Next, we will install PHP, the final component in the LAMP Stack.


## Step 3 — Installing PHP


### We've got Apache installed to serve our content and MySQL installed for database. PHP is the component of our setup that will process code to display dynamic content to the final user. In addition to the php package, we’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. We’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.


* To install these 3 packages at once, run:

```
$ sudo apt -y install php libapache2-mod-php php-mysql
```

![Screen Shot 2023-01-23 at 4 48 57 PM](https://user-images.githubusercontent.com/117458922/214330587-55c44286-f216-4c95-b96f-10303227a99a.png)

* You can run this command to confirm your PHP version when the installation is completed:

```
php -v
```

this is my output

![Screen Shot 2023-01-23 at 4 49 39 PM](https://user-images.githubusercontent.com/117458922/214331181-0b83c75a-5001-4d76-bc44-53f6c175d5c3.png)


* At this point, the LAMP stack is completely installed and fully operational.

* To test our setup with a PHP Script, it is best to setup a proper Apache Virtual Host to host our website's file and folders.
Virtual Host allows you to have multiple websites located on a single machine and users of the websites will not even notice it.

* We need to configure our Virtual Host using the following steps

#### Step 4 — Creating a Virtual Host for your Website using Apache

Now, you will set up a domain called projectlamp, but you can replace this with any domain name of your choice.


Apache on Ubuntu has one server block enabled by default that is configured to serve documents from the /var/www/html directory. We will leave this configuration as is and will add our own directory next to the default directory.


Create the directory for projectlamp using ‘mkdir’ command as follows:

```
sudo mkdir /var/www/projectlamp
```

Next, assign ownership of the directory with the $USER environment variable, which will reference your current user.

```
sudo chown -R $USER:$USER /var/www/projectlamp
```

* We can now open a new configuration file in Apache’s sites-available directory using our preferred command-line editor. Here, we’ll be using vi

```
sudo vi /etc/apache2/sites-available/projectlamp.conf
```

This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:

```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

![Screen Shot 2023-01-23 at 4 51 03 PM](https://user-images.githubusercontent.com/117458922/214333999-1b1ad277-c521-416c-a880-cfd3a035027b.png)

To save and close the file, simply follow the steps below:

* Hit the esc button on the keyboard
* Type :
* Type wqa. 
* Hit ENTER to write works in all tabs and quit vim


##### You can use the *ls* command to show the new file in the sites-available directory

```
$ sudo ls /etc/apache2/sites-available
```


* see my output below:


![Screen Shot 2023-01-23 at 4 53 17 PM](https://user-images.githubusercontent.com/117458922/214335197-38bca262-9e6a-45b3-9024-17c8e420dcbe.png)


#### With this VirtualHost configuration, we’re telling Apache to serve propitixhomes.local using */var/www/projectlamp* as the web root directory. If we like to test Apache without a domain name, we can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.



You can now use a2ensite command to enable the new virtual host:

```
$ sudo a2ensite projectlamp
```

* Also, we might want to disable the default website that comes installed with Apache. This is required if we are not using a custom domain name, because in this case Apache’s default configuration would overwrite our virtual host. To disable Apache’sdefault website use a2dissite command, type:


```
$ sudo a2dissite 000-default
```

* To make sure your configuration file doesn't contain syntax errors, run :

```
$ sudo apache2ctl configtest
```

* Finally, reload Apache so these changes take effect:

```
$ sudo systemctl reload apache2
```

As shown below:

![Screen Shot 2023-01-23 at 4 54 25 PM](https://user-images.githubusercontent.com/117458922/214338096-5279d071-9f05-49a2-8757-43b172ee5519.png)


Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

* Type and run :

```
sudo echo 'Hello LAMP, I am Kolawole Oduremi' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' 
(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```

Now go to your browser and try to open your website URL using IP address:

```
http://<Public-IP-Address>:80
```

See my outpu:

![Screen Shot 2023-01-23 at 4 58 15 PM](https://user-images.githubusercontent.com/117458922/214339584-270f9629-8b74-4c20-b633-12afe3228cd7.png)

You can leave this file in place as a temporary landing page for your application until you set up an index.php file to replace it. Once you do that, remember to remove or rename the index.html file from your document root, as it would take precedence over an index.php file by default.


* To check your Public IP from the Ubuntu shell, run :

```
$(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 
$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4)
```

## Step 5 — Enable PHP on the website


With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.

In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

```
sudo vim /etc/apache2/mods-enabled/dir.conf
```

<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

After saving and closing the file, you will need to reload Apache so the changes take effect:

```
$ sudo systemctl reload apache2
```


* Finally, we will create a PHP Script to test the PHP is correctly installed and configured on our Server.
* Now that we have a custom location to host our website's files and folders, we'll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.
* Create a new file named index.php inside our custom web root folder:

```
$ vim /var/www/projectlamp/index.php
```

This will open a blank file. Add the following text, which is valid PHP code, inside the file:

```
<?php
phpinfo();
```
* When you are finished, save and close the file, refresh the page and you will see a page similar to this :

![Screen Shot 2023-01-20 at 1 24 37 PM](https://user-images.githubusercontent.com/117458922/214341653-5fb37626-9e3e-4c5c-8f45-56524a66bc19.png)

* This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.

* If you can see this page in your browser, then your PHP installation is working as expected.

* After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:


```
$ sudo rm /var/www/projectlamp/index.php
```

* Note that it is a good practice to stop or terminate your AWS EC2 instances after the completion of your project.

**Thank You**
