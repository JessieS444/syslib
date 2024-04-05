# Installing Wordpress

Before anything, I checked for upgrades using `sudo apt update` and installed them using `sudo apt upgrade`.
Then I restarted using `sudo reboot now`.

Next, I made sure that my PHP and MySQL were up to date. I used the commands `php --version` and `mysql --version`. Both my PHP and MySQL were updated enough to work with WordPress.

Next, I switched to the /var/www/html directory and downloaded WordPress using the `wget` program: `sudo wget https://wordpress.org/latest.tar.gz`.

Then, I unpacked it: `sudo tar -xzvf latest.tar.gz`. (the gz part of the file means it actually has many files)

Then I switched to the new wordpress directory within my /var/www/html directory: `cd wordpress/`



## Creating the Database and a User

First, I needed to switch to the root Linus user, then login as the MySQL root user.

1. `cd ..`--switched back to the /var/www/html directory (not wordpress directory)
2. `sudo su`--become root user
3. `mysql -u root`--login as mysql root user

Next, I needed to:
1. Create a new user for the WordPress database
2. Be sure to replace the Xs with a strong password
3. Create a new database for WordPress
4. Grant all privileges to the new user for the new database
5. Examine the output
6. Exit the MySQL prompt

which translates to these actions:

1. `create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';` (replaced the X's with my own password)--creates new wordpress user
2. `create database wordpress;`--create new database for wordpress
3. `grant all privileges on wordpress.* to 'wordpress'@'localhost';`--allows new user I just created to modify wordpress/directory
4. `show databases;`--make sure that wordpress database is there
5. `\q` and `exit`-- quits MySQL and exits root user

![image](https://github.com/JessieS444/syslib/assets/157999229/6fbc6ec8-bedd-4d06-b434-301f17f2869e)



## Set Up wg-config.php

