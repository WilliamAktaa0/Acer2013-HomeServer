# 2013 Acer Aspire E1-571G HomeServer:

## Specs:
Intel Core(R) Core i5-3230M (4) @3.20 Ghz and Intel 3rd Gen Core processor Graphics Controller @1.10GHz (integrated).
NVIDIA GeForce 610M/710M/810M/820M / GT 620M 625M / 630M / 720M (Discrete).
4GB DDR3 and 500GB HDD.
## Software specifications:
Debian 13.6.0 amd64 netinst and docker containers to run each service in.


## Main Goals
#### PS: I Might add or remove goals along the process. However until I have a functional homeserver, I will live update this repo and readme. 
#### Some of these might require an addition ssd/nvme as well as more RAM, so I will most probably upgrade the machine along the way.
### Pi Hole:
A network-wide ad blocker and privacy tool that acts as a Domain Name System (DNS) sinkhole for all devices connected to your home network.
### Jelly Fin:
A volunteer-built media solution that allows you to stream to any device from the *totally legal license bought* media collection you have on your server. 
### Retro web page:
Retro web page or community platform reminiscent of the early 1990s and early 2000s days of the internet before corporate takeover.
### Miniflux:
a minimalist, open-source, and self-hosted RSS and Atom feed reader designed for speed, simplicity, and distraction-free reading.
### Lemmy
A free, open-source, and decentralized alternative to Reddit and Hacker News for hosting discussion forums and sharing links.
### Small Luanti Server
A free, open-source voxel game engine and creation platform. Paired with a game like MineClonia, it provides extremely similar Minecraft-like gameplay and mechanics while being free, open source, and lightweight.
### PairDrop:
A local, web-based file-sharing tool inspired by Apple’s AirDrop that lets you transfer files instantly between devices on the same network.


## OS Install:
After flashing the debian iso from debian.org on the USB flash/thumb drive and booting into the graphical install, 
### 1- Language
Select your language of choice
### 2- Network: 
Choose your primary network interface for the install. For a homeserver, wired Ethernet is highly recommended. However if you aren't close to one, you can use wireless internet temporarily for the install.
### 3- Host&Domain Name:
For hostname, I'm going to name it "homeserver", but you can choose whatever you want.
For domainname, leave it blank or just enter "local" or "home".
### 4- Login Credentials:
Enter root password. (You will need this to run commands that require administrative (sudo) privileges.
Enter full name, username, and add a password
### 5- Partitioning:
#### Use Entire Disk & LVM:
There are multiple options for partitioning the disk. I ended up choosing "Guided - use entire disk and set up LVM" because it wipes the drive and sets up a flexible, virtual storage pool. It also allows partitions to be resized dynamically or expanded across new physical drives later.
#### Writing changes to disk
Make sure to select the hard drive for partitioning not the thumb drive and then select "All files in one partition (recommended for new users)", and finally write the current partitioning scheme to disk, then select yes twice to finish write changes to disk.
#### If Error: "No root file system is define. Please correct this from the partitioning menu"
then you might has accidentally press enter again after selecting yes to write changes to disk the first time causing you to select no the second time. Go back and redo. 
Select enter to the amount of volume group to use for guided partitioning. Now select "Finish Partitioning" and finally, select yes to write changes to disks. 
#### Writing changes to disk (fr):
At this point, it should start writing to the disk. Wait like 5 minutes and you will be taken to the next installation steps:
### 6- Configuring the package manager. 
The goal is to find a mirror of the Debian archive that is close to you on the network - be aware that nearby countries, or even your own, may not be the best choice. In my case, I choose to go with the German mirror ftp.de.debian.org. Wait for debian to install core system.
### 7- Software Selection:
To keep this as lightweight and minimal as possible, we will keep standard system utils ticked, tick "SSH server", and untick "Debian desktop environment" and any desktop environment, which leaves us with just the standard system utilities and SSH server ticked. 
### 8- Grub:
Since we wiped the drive during paritioning, it should be safe to install grub. Select yes to do so and wait for the installation to finish.
### 9- Boot:
After installation, your system should reboot. After, simply enter os through the grub selection menu by simply pressing enter and you should be greeted by cli. Congrats, you just installed Debian. Simply enter username and password and you are in.
## Setup:
### Login to Root User 
    su -
and enter root password
### Update Apt and Install Sudo:
    apt update && apt install sudo -y
### Add Yourself to the Sudoers File
    sudo usermod -aG sudo username
(replace "username" with your actual username)
### Exit and Apply changes:
    exit
    newgrp sudo
### Disable the Laptop Lid Sleep
 Open the login config file:
    `sudo nano /etc/systemd/logind.conf'
  `Find `#HandleLidSwitch=suspend` and delete the "#". Finally, Ctrl+O to write changes to file and Ctrl+X to exit.
  
  After, Restart the systemd service to apply the changes:
    `sudo systemctl restart systemd-logind`

## Directory Structure
I plan to keep my data organized to prepare for future ssd upgrades, so I'm going to create a dedicated folder for each software service:
### Pi hole:
    mkdir -p ~/homeserver/pihole/config ~/homeserver/pihole/dnsmasq.d
    cd ~/homeserver/pihole

## Create the Docker Compose File Inside /homeserver/pihole:
    nano pihole.yaml
Note: Make sure you are in the previously created Pihole directory. Should look like this:
 `yourusername@homeserver:~/homeserver/pihole$: nano pihole.yaml`

