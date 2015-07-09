Linux Server Configuration
===========================
Udacity Nanodegree Project
-----------------------------
__Program:__ Full Stack Web Developer Nanodegree

__Project:__ 5 of 5

__Supporting course(s):__
* Linux Basics for Web Developers

_Note: Course not available at time of completion of project_

####Project Description
You will take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

__Primary Resources__

Initial setup:
* https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04
* https://www.digitalocean.com/community/tutorials/additional-recommended-steps-for-new-ubuntu-14-04-servers

Extra info on creating/managing users:
* https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps

Installing and using PostgreSQL:
* https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-14-04
* https://www.digitalocean.com/community/tutorials/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps--2
* https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps

Apache Configuration
* https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts

Installing git
* https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-14-04

Installing Flask
* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps


Project Overview
---------------------------
###Setup Details
IP Address: 52.27.139.93

SSH Port: 2200

__System Details__
* Distribution: Ubuntu
* Release: 14.04
* Codename: trusty
* Full: Ubuntu 14.04.1 LTS

###Project Tasks
####Task: Launch your Virtual Machine with your Udacity account
__Status:__ Complete

####Task: Follow the instructions provided to SSH into your server
__Status:__ Complete

####Task: Create a new user named grader
__Status:__ Complete
```
adduser grader
```

####Task: Give the grader the permission to sudo
__Status:__ Complete
We can grant the new user the permission to sudo by adding them to the 'sudo' group.
```
gpasswd -a grader sudo
```

####Task: Update all currently installed packages
__Status:__ Complete
```
apt-get update
apt-get upgrade
```

####Task: Change the SSH port from 22 to 2200
__Status:__ Complete
Create backup of the sshd_config file:
```
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults
```

Open the sshd_config file, comment out "Port 22" and add "Port 2200".
See applicable snippet of the sshd_config file below:
```
# What ports, IPs and protocols we listen for
# Port 22
Port 2200
```

####Task: Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
__Status:__ Complete
```
# Ensure we do not lock ourselves out!
ufw allow ssh
ufw allow 2200 # Handle changed ssh port
ufw allow 80/tcp
ufw allow ntp

# Check our settings.
ufw show added

# Enable the firewall.
ufw enable

# Reboot
reboot
```

####Task: Configure the local timezone to UTC
__Status:__ Complete

I set the local timezone to UTC by configuring the tzdata package.
```
dpkg-reconfigure tzdata
```
I then selected "None of the above" and finally "UTC".

####Task: Install and configure Apache to serve a Python mod_wsgi application
__Status:__ Complete
```
apt-get update
apt-get upgrade

apt-get install apache2

apt-get install python-setuptools libapache2-mod-wsgi

service apache2 restart
```

####Task: Install and configure PostgreSQL:
__Status:__ Complete

To install PostgreSQL:
```
apt-get update
apt-get install postgresql postgresql-contrib
```

####Task: Within postgres do not allow remote connections
__Status:__ Complete

Verified that no remote connections are allowed by inspecting the pg_hba.conf file.

This file can be viewed with the following command
```
less /etc/postgresql/9.3/main/pg_hba.conf
```

####Task: Within postgres create a new user named catalog that has limited permissions to your catalog application database
__Status:__ Complete

Login to postgres with :
```
sudo -i -u postgres
```
```
createuser --interactive
Enter name of role to add: catalog
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) n
Shall the new role be allowed to create more new roles? (y/n) n
```

####Task: Install git, clone and setup your Catalog App project (from your GitHub repository from earlier in the Nanodegree program) so that it functions correctly when visiting your server’s IP address in a browser. Remember to set this up appropriately so that your .git directory is not publicly accessible via a browser!
__Status:__ Complete

__Install git:__
```
apt-get update
apt-get install git
```

__Install python pip package manager:__
```
apt-get update
apt-get upgrade

apt-get install python-pip
```

__Install mod_wsgi (may already be installed):__
```
apt-get install libapache2-mod-wsgi
```

__Install dependencies for psycopg2 package:__
```
apt-get install libpq-dev python-dev
```

Create necessary directories/files for apache2 virtual host and clone project
to the applicable directory.

_Apache2 applicable directories_

/etc/apache2/sites-available/

/var/www/

__Install, setup, launch virtual environment:__
```
pip install virtualenv
virtualenv venv
source venv/bin/activate
```

__Clone Appplication__

Navigate to the app directory /var/www/catalogapp.

Clone the application from GitHub
```
git clone https://github.com/joelcolucci/vanillanote.git
```

Make necessary file naming adjustments to work with apache2.

__Install project dependencies__
```
pip install -r requirements.txt
```
