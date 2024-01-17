# Project1: WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

**The LAMP stack comprises Linux, Apache, MySQL, and PHP—essential tools for web development. Developers use LAMP stacks to build, host, and manage web content, making it a prevalent choice for various websites.**

## The first step that was carried out was the installation of AWS EC2 instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM)

In the dynamic realm of cloud computing, Amazon Web Services (AWS) emerges as a cornerstone for scalability and efficiency. Our journey begins with creating an AWS account,  unlocking the vast array of services that would shape our technological Course.

<img width="797" alt="image" src="https://github.com/Felisobio/Devop_Project/assets/149904523/be52f45c-9703-4cac-acfb-629358fdfb59">


To establish SSH access to your EC2 server, follow these steps:

1. **Retrieve Key Pair:**

   Ensure you have the private key associated with your EC2 instance.

2. **Download Putty (Windows):**

    For Windows users, download and install Putty and Puttygen.

3. **Convert Key (Windows):**

    Use Puttygen to convert your private key (.pem) to a Putty-compatible format (.ppk).

4. **Open Putty:**

    Launch Putty and enter your EC2 instance's public IP address.

5. **Configure Connection:**

    Navigate to "Connection" -> "SSH" -> "Auth" and load the converted private key (.ppk).

6. **Initiate Connection:**

    Use command prompt to establish the connection using the SSH command below

    ssh -i C:\Users\HP\Downloads\Feliskey.pem ubuntu@13.60.19.96

This brief guide should help you quickly set up SSH access to your EC2 server, facilitating secure and efficient remote connections.

## The second step taken was to install APACHE

Apache commonly refers to the Apache HTTP Server, an open-source web server software that plays a fundamental role in serving web content over the internet. Developed and maintained by the Apache Software Foundation, Apache HTTP Server is widely utilized due to its reliability, performance, and extensibility. It supports various operating systems, providing a robust platform for hosting websites and applications. The term "Apache" is often synonymous with this web server software in the context of web hosting and server management.

**Installing Apache using Ubuntu's package manager 'apt'**

1. **Open a Terminal/Command prompt:**

    I used the command prompt to execute the Apache installation. 

2. **Update Package List:**
   
    Before installing any new software, it's a good practice to update the package list to ensure you're installing the latest versions. Run the following command:

    sudo apt update

3. **Install Apache:**
   
    Use the following command to install Apache:

   sudo apt install apache2

4. **Start Apache:**
 
    After the installation is complete, start the Apache service:

   sudo systemctl start apache2

5. **Enable Apache on Boot:**
   
    To make sure Apache starts automatically on boot, run:

   sudo systemctl enable apache2

6. **Check Apache Status:**
   
   Verify that Apache is running without errors:

   sudo systemctl status apache2

   If Apache is running, you should see an active (running) status. below is a screenshot of my experiment 

<img width="360" alt="image" src="https://github.com/Felisobio/Devop_Project/assets/149904523/6c35f106-95a0-4f3c-82e6-c237d06b25d8">



7.  **Access the Default Page:**

     This is the result of my experiment when I accessed it in a browser using http://13.60.19.96:80 in the address bar. and it brought me to the result below which is the default Apache welcome page.


    <img width="730" alt="image" src="https://github.com/Felisobio/Devop_Project/assets/149904523/ced3d74f-a781-41d5-befc-36b921a4dde3">


## The third step is to install MySQL

MySQL is a widely used open-source relational database management system. It is known for its reliability, scalability, and performance, making it a popular choice for various applications, from small projects to large-scale enterprises.

**The following outlines the steps I took installing MySQL.**

1. **Install MySQL Server:**

   Use the following command to install the MySQL server package: And after running the command below, When prompted, confirm installation by typing Y, and then ENTER.

   sudo apt install mysql-server

3. **Secure the MySQL Installation (Optional but recommended):**

   MySQL provides a script to secure the installation. This step includes securing the root user, removing anonymous users, disallowing remote root login, and removing the test database. Run the following command and        follow the instructions:

   sudo mysql_secure_installation

5.  **When the installation is finished, log in to the MySQL console by typing:**

    Use the following command to login to the MySQL server

    sudo mysql

6. **If you already created user and create a password:**

     YOu are expected to use the command below to login into the MySQL server

     $ sudo mysql -p

7. **To Exit the sever:**

     Run the command to exit MySQL server

     exit

**Below is the outcome of my experiment**


<img width="402" alt="image" src="https://github.com/Felisobio/Devop_Project/assets/149904523/9a88e221-4542-4e78-a811-ff0aa4461553">

## The Fourth step is to install PHP 

I have installed Apache to serve as my content and MySQL installed to store and manage my data. 
PHP, which stands for Hypertext Preprocessor, is the component of my setup that will process code to display dynamic content to the end user. It is embedded in HTML code and executed on the server, generating dynamic web content. PHP supports various databases, making it a versatile tool for creating interactive and dynamic websites. Developers commonly use PHP for tasks such as processing forms, managing sessions, and interacting with databases, contributing to its widespread adoption in web application development.

In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

1 **To install these 3 packages at once, run:**

    sudo apt install php libapache2-mod-php php-mysql

2. **Verify PHP Installation:**

   After the installation is complete, you can check the PHP version:

   php -v

The image provided illustrates the output of my technical exploration, confirming the successful installation of PHP on the system.


<img width="350" alt="image" src="https://github.com/Felisobio/Devop_Project/assets/149904523/f13ff36a-9205-4f68-a2dc-970d99433db7">


To test my setup with a PHP script, it’s best to set up a proper Apache Virtual Host to hold your website’s files and folders. Virtual host allows you to have multiple websites located on a single machine and users of the websites will not even notice it.

## The fifth step is testing my setup.

Firstly we will begin with **CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE**

1.  **Create directory for Felislamp using ***"mkdir"*** command as follows**
    
    sudo mkdir /var/www/Felislamp

2.  **Next, assign ownership of the directory with your current system user:**

    sudo chown -R $USER:$USER /var/www/Felislamp

    <img width="582" alt="image" src="https://github.com/Felisobio/Devop_Project/assets/149904523/6204a883-1cb5-4ecb-b0d7-d25115bdda02">


 3. **The next step is to create and open a new configuration file in apache's site available directory using my preferred command-line editor. Here, we’ll be using vim:**

     sudo vi /etc/apache2/sites-available/Felislamp.conf

     This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:

  <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


**To save and close the file, simply follow the steps below:**

1. Hit the esc button on the keyboard
2. Type:
3. Type wq. w for write and q for quit
4. Hit ENTER to save the file

I used the **ls** command to show the new file in the sites-available directory

sudo ls /etc/apache2/sites-available
