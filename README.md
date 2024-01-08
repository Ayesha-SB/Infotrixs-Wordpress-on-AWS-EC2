# Infotrixs-Wordpress-on-AWS-EC2
Word-press deployed on AWS EC2 monolithic and micro-service architecture

Deploy application in monolithic and micro services architecture
❖ Description:
- For monolithic: 1 EC2 instance, deploy WordPress and MYSQL on the same instances
Configure the necessary security group for the instances
- EC2 instance type: t2-micro, AMI: Ubuntu-*

SOLUTION: FOR MONOLITHIC ARCHITECTURE 

IN EC2 CONSOLE CREATE A SECURITY GROUP first, in security group allow HTTP, HTTPS, SSH, MYSQL protocols, (for anywhere address, that is 0.0.0.0)
![Instance creation](https://github.com/Ayesha-SB/Infotrixs-Wordpress-on-AWS-EC2/assets/155983579/b4b75101-7732-458d-a34f-ea68c0a9284f)

CREATE AN EC2 INSTANCE with required configuration ,attach your newly created group to this instance ,after launching an instance use EC2 CONNECT  to connect your Instance to SSH ,there we have to give commands as mentioned below 
 (NOTE: WE CAN ALSO USE ANY OTHER SSH CLIENTS like putty and mobax), here I have used EC2 instance connect

1   sudo apt update 
(The sudo apt update command is used to update the local package index and provide the system with the latest information about available packages.)

2   sudo apt upgrade
(The sudo apt upgrade command downloads and installs the latest packages for a system, replacing any older versions. This command can be used to free up system memory)

3   sudo apt install apache2
(Apache HTTP Server is a free, open-source web server software. It's the most commonly used web server on Linux systems)


4 sudo apt install php libapache2-mod-php php-mysql

 (To install core PHP packages as dependencies)


5   sudo apt install mysql-server 
(This installs the package for the MySQL server, as well as the packages for the client and for the database common files.)

6   sudo mysql -u root
(TO login IN SQL)

7 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Ayesha@123';
(Change authentication plugin to mysql_native_password (change the password to something strong)


8 .CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Ayesha@123';
(TO create a new database user for WordPress (change the password to something strong))

9 CREATE DATABASE wp;
(TO create a new database user for WordPress (change the password to something strong))

10 GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;
(Grant all privilege on the database 'wp' to the newly created user)

USE crtl+d to exit from sql terminal

11 cd /tmp
wget https://wordpress.org/latest.tar.gz
(TO download WordPress ZIP File)

12 tar -xvf latest.tar.gz
(To unzip file)

13 sudo mv wordpress/ /var/www/html
(TO Move wordpress folder to apache document root)

13 sudo systemctl restart apache2
(Command to restart/reload apache server)


NOW for testing purpose copy the IP address of your instance and paste it in any browser in this format (http/: “instance ip address"/wordpress)  
Here we can see wordpress site, enter your database name, username and password

At this step we may get error, here he have to troubleshoot this error, for that we just need to follow the steps as given in wordpress dialogue box

The error was  'wp.config.php file (as mentioned) was missing' so we have to create a new file by name wp.config.php (as mentioned).
SO to create a new file, first we have to go for wordpress file location, for this we need to give commands as 
14. cd /var/www/html/wordpress 
Now to create a new file in this location use command as 
15 nano “file name”
(File name as mentioned in wordpress dialogue box) 
![Resolving Error](https://github.com/Ayesha-SB/Infotrixs-Wordpress-on-AWS-EC2/assets/155983579/111b91b4-aa14-4bd3-9f0f-8be7b1d35bac)

 After giving above command new empty terminal will be visible, we have to copy and paste entire content as seen in wordpress dialogue box. 
For saving this f use ctrl+o, HIT Enter, ctrl+x, hit enter.
DONE

![Wordpress installation (2)](https://github.com/Ayesha-SB/Infotrixs-Wordpress-on-AWS-EC2/assets/155983579/cfe08b1a-578b-4ac5-a9c0-5eabb5b315f4)
![Installation complete](https://github.com/Ayesha-SB/Infotrixs-Wordpress-on-AWS-EC2/assets/155983579/9aefb3c4-113f-4a98-b18c-5237f6e935de)

Now to verify, Refresh your http/: “your ip address"/wordpress tab, you will get welcome note from wordpress 

TASK IS COMPLETED 
![Wordpress landing page](https://github.com/Ayesha-SB/Infotrixs-Wordpress-on-AWS-EC2/assets/155983579/b8ad87d7-3c55-4fc1-b489-54d4912a555b)

![Wordpress Homepage](https://github.com/Ayesha-SB/Infotrixs-Wordpress-on-AWS-EC2/assets/155983579/69f9c4de-d173-45c2-97fb-8742a363f1fe)





