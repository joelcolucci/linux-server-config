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
#####Task: Launch your Virtual Machine with your Udacity account
######Status: Complete

#####Task: Follow the instructions provided to SSH into your server
######Status: Complete

#####Task: Create a new user named grader
######Status: Complete
```
sudo adduser grader
```

#####Task: Give the grader the permission to sudo
######Status: Complete
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

#####Task: Update all currently installed packages
######Status: Complete
```
apt-get update
apt-get upgrade
```

#####Task: Change the SSH port from 22 to 2200
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

#####Task: Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
######Status: Complete
```
ufw enable

# Ensure we do not lock ourselves out!
ufw allow ssh
ufw allow 2200 # Handle changed ssh port
ufw allow http
ufw allow ntp
```

#####Task: Configure the local timezone to UTC
######Status: Complete
I set the local timezone to UTC by configuring the tzdata package.
```
dpkg-reconfigure tzdata
```
I then selected "None of the above" and finally "UTC".

#####Task: Install and configure Apache to serve a Python mod_wsgi application
######Status: Complete
```
apt-get update
apt-get upgrade

apt-get install apache2

apt-get install python-setuptools libapache2-mod-wsgi

service apache2 restart
```

#####Task: Install and configure PostgreSQL:
######Status: Complete
```
apt-get install postgresql
```
Login to postgres with :
```
sudo -i -u postgres
```

#####Task: Within postgres do not allow remote connections
######Status: Complete
Verified that no remote connections are allowed by inspecting the pg_hba.conf file.

This file can be viewed with the following command
```
less /etc/postgresql/9.1/main/pg_hba.conf
```

#####Task: Within postgres create a new user named catalog that has limited permissions to your catalog application database
######Status: Complete
```
sudo su - postgres
psql
```
```
CREAT ROLE catalog LOGIN;
```

#####Task: Install git, clone and setup your Catalog App project (from your GitHub repository from earlier in the Nanodegree program) so that it functions correctly when visiting your server’s IP address in a browser. Remember to set this up appropriately so that your .git directory is not publicly accessible via a browser!
######Status: Incomplete
Install git:
```
apt-get update
apt-get install git
```

