# Installing Apache, PHP, and MySQL

## Apache:
- I installed Apache as per this week's instructions.
- Both the `w3m 127.0.0.1` and `w3m localhost` commands worked for me to access the webpage I created.
- I don't know HTML so I coped and pasted the provided code in order to get started with building the content of my webpage.
- Code provided:
```
  <html>
  <head>
  <title>My first web page using Apache2</title>
  </head>
  <body>

  <h1>Welcome</h1>

  <p>Welcome to my web site.
  I created this site using the Apache2 HTTP server.</p>

  </body>
  </html>
  ```
- Overall, I found this process to be more simple than I thought it would be. It is interesting to see some of the pieces we have learned throughout the weeks coming together, like using nano to create files that are pages on the IP address site.
- I played with the HTML code we were given to make my website look like this:
  ![image](https://github.com/JessieS444/syslib/assets/157999229/efc3f274-97a4-4dcf-b135-23487f4e94d2)
- The nano file is index.html. We use nano files to create webpages through Apache.
  ![image](https://github.com/JessieS444/syslib/assets/157999229/3040dc17-6fce-4d27-b630-8178e6ca3418)



## PHP
- For the next part, I again followed the instructions to install PHP and configure it with Apache2.
- I used the `sudo apt install php libapache2-mod-php` command to install PHP, then restarted Apache2 using `sudo systemctl restart apache2`.
- I checked the install on the /var/www/html/ directory and it was good to go.
- One thing I found really interesting was switching the configuration for Apache to where when I go to my external IP address site, the default page is the index.php file instead of the index.html file. This was done via the instructions by switching the configuration in the dir.conf file.
- Here is the new default page on the IP address site:

![image](https://github.com/JessieS444/syslib/assets/157999229/4f5670f7-3d17-4343-8c7c-281c671414b9)



## MySQL

