# Week 7 Notes

## The `sudo` Command
- The `sudo` command allows us to execute commands as if we were the root user.
- It allows us to make changes to things without logging in as the root user.
- We will be using `sudo` down the line to modify files, create directories, and perform other maintenance tasks needed to install and manage software.

> Sudo syntax: use `sudo` at the beginning of other commands we already know how to use. For example:
```
cd /usr/local/bin
sudo mkdir data
```
> This command would make a directory called "data" in the location \usr\local\bin. The `sudo` command makes it to where making this is possible from our home directory.


## The `apt` Command
The `apt` command is used for searching.
We will use a lot of `sudo apt` commands, such as:
- `sudo apt update` : checks for updates.
- `sudo apt upgrade` : applies any needed updates.
- `apt search` : does not need `sudo` because it does not change the system at all. This command searches for package name (name of software).
- `apt show` : gives more info about a package (software).
- `sudo apt install` : installs application if you add package name at the end (ex: `sudo apt install tldr`)
- `sudo apt remove` : removes package/application/software (`sudo apt --purge remove` also removes unneeded configuration files).
- `sudo apt autoremove` : removes software that was installed to run other software that has been deleted.
- `sudo apt clean` : removes extra files that were installed with other files in order to free up disc space.



# Library Search

I found library search to be pretty interesting. I've read about the Z39.50 protocol for classes, but not in much depth. It was interesting to retrieve information in this format.

- `yaz-client` pulls up the program.
- To connect to a library OPAC, use the `open` command followed by the server address (ex: `open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY` for UK's OPAC.

<img width="783" alt="Screenshot 2024-02-25 at 2 47 21 PM" src="https://github.com/JessieS444/syslib/assets/157999229/2950175b-50e3-42c8-be4e-a4b92ca72a24">
