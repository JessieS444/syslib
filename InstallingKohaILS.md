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

Okay, after creating that second VM instance I 
