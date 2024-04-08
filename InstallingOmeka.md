# Installing Omeka

This week was very challenging for me. I didn't actually think it was going bad at first, but then I got to some of the final steps and it wasn't turning out. I got error message after error message and I kept going back into the db.ini file to change things, and while the error messages on the omeka page changed, nothing seemed to work. I decided enough was enough when I somehow got a fatal error message (HOW?) and decided to start all the steps over for this week fresh.

And it turns out I should have done that sooner because I did them again and for some reason it worked perfectly this time. I got past the point where I was getting all the error messages on the web browser and now I can finally start designing my website.

Honestly, if I listed all the steps I did this week I would not only have the longest doc ever, I would also look like an idiot (hopefully a lovable one). For future reference, I think possibly where I went wrong was either doing things slightly out of order (I didn't make the user/password in MySQL before modifying the db.ini file), not matching the stuff entered in MySQL to the db.ini file (though I thought I checked this to make sure), and/or forgetting to restart MySQL and Apache2 before going to the web based installation process.

For future reference of me, what I did this week was follow the directions in my last github doc (InstallingWordpress.md) but sub some of the info for the Omeka version. Last week's notes are very helpful for installing Omkeka as well, so I don't feel the need to trace my convoluted efforts at problem solving in order to write out cohesive steps. Make sure to write down what you put in the MySQL part to make sure you put the matching info in the db.ini file. Do things in the order as written. Just follow the steps and write down names and passwords as soon as you enter them.
https://cseanburns.github.io/systems-librarianship/5b-install-omeka.html

I got a lot more comfortable navigating around the terminal and different directories without having prompts this week. It took my hands some trial and error to remember exactly what to do at points but I got a lot faster as it went on. It was both extremely frustrating and gratifying.

Also for future reference of me: I did not change the directory name to plain ol' omeka, it is omeka-3.1.2.

