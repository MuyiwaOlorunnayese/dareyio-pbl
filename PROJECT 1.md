PROJECT TITLE: LAMP STACK IMPLEMENTATION
------------------------------------------
This is a project which implement the use of LAMP STACK In AMAZON WEB SERICES (AWS)

What is a Technology stack?

A technology stack is a set of frameworks and tools used to develop a software product. This set of frameworks and tools are very specifically chosen to work together in creating a well-functioning software. They are acronymns for individual technologies used together for a specific technology product. some examples are…

*LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)

*LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)

*MERN (MongoDB, ExpressJS, ReactJS, NodeJS)

*MEAN (MongoDB, ExpressJS, AngularJS, NodeJS

## I carried out this project using the followings steps

web stack implementation (lamp stack) in aws

step 1 — installing apache and updating the firewall

step 2 — installing mysql

step 3 — installing php

step 4 — creating a virtual host for your website using apache

step 5 — enable php on the website

-------------------------------------

web stack implementation (lamp stack) in aws


### Create a EC2 Instance in Aws


1. Select region (the cl and launch a new EC2 instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM)


1. Create a pair Key as while creating an instance on aws and download it on your machine.


1. Go into the folder where the pair key is downloaded and run the following command to connect to the instance

        sudo chmod 0400 <private-key-name>.pem
    
        ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
        
        
        
        
        

![Screenshot 2022-08-18 at 17 24 41](https://user-images.githubusercontent.com/108664973/185458460-dce0fad1-8a02-45d4-be7c-f205a2c70c1a.png)    


### Installing apache and updating the firewall


The first thing you need to do is to update a list of packages in package manager, the following command is used to carry this out

               sudo apt update
Then  run apache2 package installation using the following command

               sudo apt install apache2
To verify that apache2 is running as a Service in your OS, use following command

              sudo systemctl status apache2
You can try to check how you can access it locally in our Ubuntu shell, using the following command

               curl http://localhost:80
  
                             or
              
                curl http://127.0.0.1:80
The image below will be display with the ip address


<img width="801" alt="163705182-cd4d5d38-6943-41dc-bfb1-2184847c3a54" src="https://user-images.githubusercontent.com/108664973/185459145-81f5c2b5-8d21-473f-a8e0-a3bafb448f82.png">

        


### installing mysql


To install mysql use the following comman line to install the server

               sudo apt install mysql-server
Start the interactive script by running:

               sudo mysql_secure_installation
You can sudo in the the server using the command

                      sudo mysql
if you see the image below displayed, it showed it is sucessful.

<img width="559" alt="163705771-3ce79a3d-275d-440d-83f8-676a7bf58109" src="https://user-images.githubusercontent.com/108664973/185460194-d6238c15-2f9e-43a1-a804-73dab302f62f.png">


you can exit the server using the following command

                             exit


### installing php


In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies. We use the following command to install 3 packages at once

                      sudo apt install php libapache2-mod-php php-mysql
After the installation, you can run the check the php version with the following command

                                           php -v
                                           
                                           
                                          ![Screenshot 2022-08-18 at 17 22 33](https://user-images.githubusercontent.com/108664973/185490074-c5fc5993-f61b-457a-9dfd-8f118d31b0e3.png)

![Screenshot 2022-08-18 at 17 22 54](https://user-images.githubusercontent.com/108664973/185490191-db0d4cba-97f5-4d15-bd3a-b1aaf1409a2c.png)

![Screenshot 2022-08-18 at 17 23 09](https://user-images.githubusercontent.com/108664973/185490247-37075bdd-1f66-4cf7-b784-d85e17dd6860.png)



 At this point, your LAMP stack is completely installed and fully operational.
 
1. Linux (Ubuntu)
1. Apache HTTP Server
1. MySQL
1. PHP



### creating a virtual host for your website using apache


Create the directory for projectlamp using ‘mkdir’ using the command

                             sudo mkdir /var/www/projectlamp
Assign ownership of the directory with current system user using the command

                            sudo chown -R $USER:$USER /var/www/projectlamp
Create and open a new configuration file in Apache’s usinng the command line

                            sudo vi /etc/apache2/sites-available/projectlamp.conf
paste the command below in the vim file and save

                                  <VirtualHost *:80>
                                  ServerName projectlamp
                                  ServerAlias www.projectlamp 
                                  ServerAdmin webmaster@localhost
                                  DocumentRoot /var/www/projectlamp
                                  ErrorLog ${APACHE_LOG_DIR}/error.log
                                  CustomLog ${APACHE_LOG_DIR}/access.log combined
                                  </VirtualHost>
You can list us the command line below tp list what is in the file

                             sudo ls /etc/apache2/sites-available
Enable new virtual host using the command

                                    sudo a2ensite projectlamp
You can disable Apache default website using the command

                                    sudo a2dissite 000-default
Check for syntax error in the configuration file with the command

                                    sudo apache2ctl configtest
Reload Apache for the changes to take effect

                                    sudo systemctl reload apache2
Create an index.html file in that location to test that the virtual host works as expected using the command

 sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s                           http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
The website URL can be access using thr IP address

                                    http://<Public-IP-Address>:80
### Enable PHP on the website

Edit the conf file with the command

                             sudo vim /etc/apache2/mods-enabled/dir.conf
Paste in the command

                       <IfModule mod_dir.c>
                       #Change this:
                       #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
                       #To this:
                       DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
                       </IfModule>
Reload Apache

                             sudo systemctl reload apache2
                             
                             

                       
![Screenshot 2022-08-18 at 17 23 53](https://user-images.githubusercontent.com/108664973/185491929-197816ce-634e-4c63-b9ea-e5097a9bd19f.png)

Create index.php file

                             vim /var/www/projectlamp/index.php
Add the following text, which is valid PHP code, inside the file:

                                         <?php
                                        phpinfo();
Save and close the file, refresh the page and you will see a page similar to this:

![Screenshot 2022-08-18 at 17 26 06](https://user-images.githubusercontent.com/108664973/185491103-d8a01043-52a9-4e0a-8687-d5796b2ba302.png)


Its best to remove the file create, you can do that using the following command

                             sudo rm /var/www/projectlamp/index.php
                             
                             
 
 
 ### SUMMARY
 
 In this project i was able to learn different Technology Stacks used in Web development and how to implement the most commonly used one - LAMP.
