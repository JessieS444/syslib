# Creating a Bare Bones Cataloging Module

In this lesson, we created the HTML and PHP pages needed to make our cataloging module work as well as added security so that random people couldn't add items to our catalog.

## HTML Page
1. We titled this page "index.html". To make it, first we created the new directory. We went to `cd /var/www/html` and then used the command `sudo mkdir cataloging`.
2. Then we used nano to create the file in the cataloging directory: `cd cataloging` and then `sudo nano index.html`.
3. The following HTML was the contents of the file:
```
   <!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="date" id="copyright" name="copyright">

        <input type="submit" value="Submit">
    </form>
</body>
</html>
```
4. Change all 11.111.111.111 to correct IP address. Done!

## PHP Page
1. With the index.html page set up, we already have a user interface for the PHP file but we still need to add PHP script.
2. Make the file "insert.php" on the cataloging directory using the `sudo nano insert.php` command.
3. Add the following PHP into the file:
```
<!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="date" id="copyright" name="copyright">

        <input type="submit" value="Submit">
    </form>
</body>
</html>
```
4. Change all 11.111.111.111 to correct IP address.


## Security

This section we added authentication to protect our cataloging module from outside users.

1. From the cataloing directory, use the command `sudo htpasswd -c /etc/apache2/.htpasswd libcat`. "Libcat" is the username.
2. The command `sudo nano /etc/apache2/apache2.conf` tells Apache2 to set up a username and password to control access to the cataloging module.
3. Navigate to the line 172 approximately or wherever the following stanza is:
```
<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride None
  Require all granted
</Directory>
```
4. Change the word "None" to "All".
5. In the cataloging directory, create a nano file called .htaccess: `sudo nano .htaccess`.
6. Add the following:
```
AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```
7. Check that configuration is okay: `apachectl configtest`.
8. If you get a Syntax OK message, restart Apache2 and check its status:
`sudo systemctl restart apache2` then `systemctl status apache2`.

## Permissions and Ownership

![image](https://github.com/JessieS444/syslib/assets/157999229/ecb93408-228d-4148-a168-d2f22fb427e0)
![image](https://github.com/JessieS444/syslib/assets/157999229/b7113c92-5cb7-46be-8ef4-fc0daa408aa9)



For the last part of the lesson, we connected to MySQL to view the books added from the cataloging module:
![image](https://github.com/JessieS444/syslib/assets/157999229/ce4fa6ee-fc5a-4f74-8b50-7608cc7f2a73)

1. I first connected to MySQL through using the `mysql -u opacuser -p` command.
2. After entering my password, used the `show databases;` command.
3. I connected to the opacdb database using `use opacdb;` command.
4. Then I used the `describe books;` command.
5. Finally, to get the chart of items I wanted, I used the `select * from books` command and then `;`.

### Overview
This week, I got all the way through security and could not figure out why I kept getting the following error message:

![image](https://github.com/JessieS444/syslib/assets/157999229/5e1cfd90-8d06-422a-8500-165f27fd406f)

I retraced my steps and found that I had not saved the PHP script before exiting the insert.php file. So that is what it does without the PHP script, which is interesting.
Other than that, this week was fairly smooth sailing. I feel like a lot of stuff finally clicked into place this week for me and I better understood a lot of the steps we were doing and why we were doing them (its about time). I've been waiting for this moment for much of the semester because I haven't done a lot of this stuff ever before so it was all feeling very foreign, but I guess I have finally done enough to start feeling more confident. Yay!
