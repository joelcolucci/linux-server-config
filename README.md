Linux Server Configuration
=====================
###Nanodegree Project
School: Udacity

Program: Full Stack Web Developer Nanodegree

Project #5

Supporting course(s):

Linux Basics for Web Developers*

*Not available at time of completion of project

###Project Overview
You will take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

###Project Tasks
#####Launch your Virtual Machine with your Udacity account
  * Status: Complete

#####Follow the instructions provided to SSH into your server
  * Status: Complete

#####Create a new user named grader
  * Status: Complete
```
sudo adduser grader
```

#####Give the grader the permission to sudo
  * Status: Complete
```
visudo
```
Find root user line that looks as follows:
```
root ALL=(ALL:ALL) ALL
```
Add new user by entering the following line:
```
grader ALL=(ALL:ALL) ALL
```

#####Update all currently installed packages
  * Status: Complete
```
apt-get update
apt-get upgrade
```

#####Change the SSH port from 22 to 2200
######Status: Complete
Create backup of sshd_config file:
```
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults
```
Open sshd_config file, comment out "Port 22" and add "Port 2200".
Snippet of sshd_config file:
```
# What ports, IPs and protocols we listen for
# Port 22
Port 2200
```

#####Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
######Status: Complete
```
ufw enable

# Ensure we do not lock ourselves out!
ufw allow ssh
ufw allow 2200 # Handle changed ssh port
ufw allow http
ufw allow ntp
```

#####Configure the local timezone to UTC
######Status: Incomplete

#####Install and configure Apache to serve a Python mod_wsgi application
######Status: Incomplete

#####Install and configure PostgreSQL:
######Status: Incomplete

#####Do not allow remote connections
######Status: Incomplete

#####Create a new user named catalog that has limited permissions to your catalog application database
######Status: Incomplete

#####Install git, clone and setup your Catalog App project (from your GitHub repository from earlier in the Nanodegree program) so that it functions correctly when visiting your server’s IP address in a browser. Remember to set this up appropriately so that your .git directory is not publicly accessible via a browser!
######Status: Incomplete
