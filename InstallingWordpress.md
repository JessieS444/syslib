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

When creating the bare bones OPAC, we made the file "login.php" to house the name of the database, the name of the database user, and the user's password; we kind of replicated this for wordpress, but we call it "wg-config.php".

To do this I:
1. `cd wordpress`--switch to wordpress directory
2. `ls-l` then `sudo cp wp-config-sample.php wp-config.php`--copy the "wp-config-sample.php" file to "wp-config.php" file
3. `sudo nano wp-config.php`--open up the file in nano to edit and add info
4. Replace database name, database user, and database password with desired options (I just did wordpress for the name of the db and user and the password I put in earlier).
4. add "define('FS_METHOD','direct');" to the end of the nano file in order to disable FTP uploads.
5. `sudo chown -R www-data:www-data /var/www/html/wordpress`--change file ownership


## Finishing up

The rest is done on browser? I went to my IP webpage to see what I've done: http://34.125.133.35/wordpress/wp-admin/install.php

Now it's time to decorate! Huzzah!
