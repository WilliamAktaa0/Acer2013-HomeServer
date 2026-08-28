# Acer2013 HomeServer:
## Model: Acer Aspire E1-571G (V2.14)
## Specs:
Intel Core(R) Core i5-3230M (4) @3.20 Ghz and Intel 3rd Gen Core processor Graphics Controller @1.10GHz (integrated).
NVIDIA GeForce 610M/710M/810M/820M / GT 620M 625M / 630M / 720M (Discrete).
4GB DDR3 and 500GB HDD.
## Software specifications:
Debian 13.6.0 amd64 netinst and docker containers to run each service in.


## Main Goals:
#### PS: I Might add or remove goals along the process. However until I have a functional homeserver, I will live update this repo and readme. 
#### Some of these might require an addition ssd/nvme as well as more RAM, so I will most probably upgrade the machine along the way.
### Pi Hole:
A network-wide ad blocker and privacy tool that acts as a Domain Name System (DNS) sinkhole for all devices connected to your home network.
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
1- Select your language of choice
2- Choose your primary network interface for the install. For a homeserver, wired Ethernet is highly recommended. However if you aren't close to one, you can use wireless internet temporarily for the install.
4- For hostname, I'm going to name it "homeserver", but you can choose whatever you want.
5- For domainname, leave it blank or just enter "local" or "home".
6- Enter root password. (You will need this to run commands that require administrative (sudo) privileges.
7- Enter full name, username, and add a password
8- Partitioning:
There are multiple options for partitioning the disk. I ended up choosing "Guided - use entire disk and set up LVM" because it wipes the drive and sets up a flexible, virtual storage pool. It also allows partitions to be resized dynamically or expanded across new physical drives later.
Make sure to select the hard drive for partitioning not the thumb drive and then select "All files in one partition (recommended for new users)", and finally write the current partitioning scheme to disk, then select yes twice to finish write changes to disk.
If Error: "No root file system is define. Please correct this from the partitioning menu", then you might has accidentally press enter again after selecting yes to write changes to disk the first time causing you to select no the second time. Go back and redo. 
Select enter to the amount of volume group to use for guided partitioning. Now select "Finish Partitioning" and finally, select yes to write changes to disks. 
At this point, it should start writing to the disk. Wait like 5 minutes and you will be taken to the next installation steps:
9- Configure the package manager. The goal is to find a mirror of the Debian archive that is close to you on the network - be aware that nearby countries, or even your own, may not be the best choice. In my case, I choose to enter information manually and go with the Debian Global CDM.
10- 
