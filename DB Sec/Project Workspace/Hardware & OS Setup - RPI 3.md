# Raspberry PI as a Server
Reference Video - [Raspberry Pi Home Server - Docker, Portainer, Plex, Wordpress, and More - YouTube](https://www.youtube.com/watch?v=yFuTAKq_j3Q&t=41s) 
## Plan, Resources
- Boot to Ubuntu from microSD on the Raspberry Pi 3
	- [How to install Ubuntu Server on your Raspberry Pi | Ubuntu](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview) 
## Set Up Ubuntu on Raspberry Pi 3
### Prepare the SD Card
- Inserted microSD
- [Raspberry Pi Imager for Windows](https://downloads.raspberrypi.org/imager/imager_latest.exe)
#### Image microSD for Ubuntu
- ![400](IMG-20231021165732624.png)
- ![400](IMG-20231021170429871.png)
- ![400](IMG-20231021165947400.png)
### Setup Raspberry Pi
- Plug in HDMI, then plug in power cord
- Run commands to get desktop for the Pi
	- sudo apt update 
	- sudo apt upgrade
	- Choose a desktop:
		- sudo apt install xubuntu-desktop
		- sudo apt install lubuntu-desktop
	- sudo reboot
	- Log into desktop

## Setup Applications for Postgres Hosting on Raspberry Pi 3
- 
