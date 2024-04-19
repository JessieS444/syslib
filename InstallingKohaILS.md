# Installing Koha ILS

Let's try this again. I had already typed out a lot of documentation but hadn't saved it and accidentally hit the back button through a touchpad shortcut (UGH). Future self: SAVE YOUR WORK AS YOU GO DUMMY!

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

Now we're cooking with fire (I assume. It seems like we're getting somewhere).

Next, I connected to the new VM instance and ran `sudo apt update` and `sudo apt upgrade` to check for updates then install. I had 37 I needed to update. Then I ran `sudo apt autoremove -y && sudo apt clean` to save disk space.

Then I used the command `sudo apt install gnupg2` to install gnupg2, which is "used to create digital signatures, encrypt data, and aid in secure communication."

After installing, I needed to reboot so it could be effective. I used the command `sudo reboot now` and then reconnected using the gcloud command.


## Adding Koha Repository

To add the Koha 
