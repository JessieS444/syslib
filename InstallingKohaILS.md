# Installing Koha ILS

Let's try this again. I had already typed out a lot of documentation but hadn't saved it and accidentally hit the back button through a touchpad shortcut (UGH). Future self, remember to save work.

To start the Koha ILS installation process I first followed the directions from earlier in the semester to create a new VM instance that is capable of what we need it to do. Here is what I did:


    Click on the hamburger icon (three vertical bars) in the top left corner.
    Click on Compute Engine and then VM instances
    Next, click on Create Instance.
    Provide a name for your instance.
        E.g., I chose scond-ubuntu for this second VM instance.
    In the Machine configuration section, make sure E2 is selected.
    In the Machine type section, select e2-medium (2 vCPU, 1 core, 4 GB memory)
        This is the machine type needed for Koha.
    Under Boot disk, click on the Change button.
    In the window, select Ubuntu from the Operating system drop down box.
    Select Ubuntu 20.04 LTS x86/64
    Leave Boot disk type be set to Balanced persistent disk
    Disk size should be set to 10 GB.
    Click on the Select button.
    Check the Allow HTTP Traffic button
    Finally, click on the Create button to create your VM instance.

Okay, after creating that second VM instance I needed to go to the hamburger menu and find VPN Network in order to create a firewall that will allow web traffic to come in and out from port 8080. I couldn't find an option for VPN Network, but I did see an option for VPC Networks which is just one letter off. I googled to find the differences and I didn't understand but there is a firewall option under VPC Networks so I'm assuming that is the right place.

After going to firewall, I clicked "create a firewall rule" (NOT "create a firewall policy") and followed the following steps:


    At the top of the page, choose Create a firewall rule (do not choose Create a firewall policy)
        Add name: koha
        Add description: open port 8080
    Next to Targets, click on All instances in the network
    In the Source IPv4 ranges, add 0.0.0.0/0
    Click on Specified protocols and ports
        Click on TCP
        Add 8080 in the Ports box
    Click on Create


Next, I connected to the new VM instance and ran `sudo apt update` and `sudo apt upgrade` to check for updates then install. I had 37 I needed to update. Then I ran `sudo apt autoremove -y && sudo apt clean` to save disk space.

Then I used the command `sudo apt install gnupg2` to install gnupg2, which is "used to create digital signatures, encrypt data, and aid in secure communication."

After installing, I needed to reboot so it could be effective. I used the command `sudo reboot now` and then reconnected using the gcloud command.



## Adding Koha Repository

To add the Koha repository, we need administrator access, so we have to use the `sudo su` command to log in as the root user.

After logging in as the root user, I used the following command to add the Koha repository:
`echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list`

Then added the digital signature that verifies the repository:
`wget -q -O- https://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -`



## Installing and Configuring Koha

Finally we are installing. I followed the below instructions and they worked perfectly (still in the root user):

1. Next we need to update/sync the new repository with the Koha remote repository. This just means that we use `apt update` command again.

2. Now we view the package information for Koha using the command `apt show koha-common`

3. And install it: `apt install koha-common`

The above command will download and install a lot of additional software, and therefore the process will take several minutes. (which it did for me).


Onto configuring. I followed the instructions provided and it seemed again to work perfectly:

1. Next we need to edit some configuration files for Koha: `nano /etc/koha/koha-sites.conf`

2. In the above koha-sites.conf file, change the line that contains the following information:

INTRAPORT="80"

To:

INTRAPORT="8080"

3. Next install and setup mysql-server: `apt install mysql-server`

4. Next we set the root MySQL password (kept the default password shown but I made my own instead): `mysqladmin -u root password bibliolib1`

5. When we installed Koha, the Apache2 web server was installed with it as a prerequisite. We need to enable URL rewriting and CGI functionality.
```
a2enmod rewrite
a2enmod cgi 
```

6. Now we need to restart Apache2 in the normal way: `systemctl restart apache2`

7. Next we create a database for Koha: `koha-create --create-db bibliolib`

8. We need to tell Apache2 to listen on port 8080: `nano /etc/apache2/ports.conf`

And add:

Listen 8080

9. Make sure Apache configuration changes are valid: `apachectl configtest`

If you get an error message, trace the error in the file and line listed. (I did not thankfully.)

10. Restart Apache2: `systemctl restart apache2`

11. We'll disable the default Apache2 setup, enable traffic compression using deflate, enable the bibliolib site, and then reload Apache2's configurations and restart again:
```
a2dissite 000-default
a2enmod deflate
a2ensite bibliolib
systemctl reload apache2
systemctl restart apache2
```

## Koha Web Installation

I followed these instructions and my Koha installation went well! I'm very pleased that this week's work has went so smoothly. After the catastrophic error messages of last week I was expecting the worst this week, but I guess being very very careful helped a decent amount.

The last thing I did was set up the URL for my OPAC:
When the install and setup are complete, you will have access to the staff interface. To view the public facing OPAC, you need to make a setting change.

    Click on More in the top drop down box
    Click on Administration
    Click on Global System Preferences
    Click on OPAC in the left hand side bar
    Scroll down to the OPACBaseURL line.
    Enter the IP address of your server: http://IP-ADDRESS
    Click on Save all OPAC Preferences

Once you save these preferences, you should be able to visit your public facing OPAC at the server IP address.

And now I'm off to flesh this ILS and OPAC out! Yay!
