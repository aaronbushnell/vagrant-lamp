# Simple LAMP server using Vagrant

This is a simple LAMP stack driven by Vagrant and Virtualbox. Vagrant works best when every site you work on has its own Vagrant setup (so you can configure memory limits, upload limits, etc to be the same as what is on the production server). However, this encourages an approach similar to MAMP (use this Vagrant setup to house all of your PHP projects).

## Before you install

You'll need to install a couple pieces of software

- [Install Vagrant 1.6.5](https://www.vagrantup.com/download-archive/v1.6.5.html). Newer versions might not work, so use 1.6.5 for now.
- [Install Virtualbox 4.3.x](https://www.virtualbox.org/wiki/Download_Old_Builds_4_3). Newer versions might not work, so use 4.3.x for now.

## Installation

```sh
# Create a directory for all of your Vagrant data to live. We'll use ~/Projects for this tutorial
$ mkdir ~/Projects

# Clone this repo into a PHP directory within ~/Projects
$ git clone [repoUrl] ~/Projects/PHP

# Delete the .git/ directory (we don't want to track your config changes) and create the ~/Projects/PHP/public where your sites will live
$ rm -rf ~/Projects/PHP/.git/ && mkdir ~/Projects/PHP/public

# Change to the PHP directory and kickstart Vagrant
$ cd ~/Projects/PHP && vagrant up
```

## How to setup a new site

```
# Edit the config file (using Sublime, but use whatever you want)
$ subl ~/Projects/PHP/puphpet/config.yaml

# Find the "vhosts" block under the "apache" section (not "ngnix")
# Copy one entire block that starts with a 12-character random ID
# Change the ID to another unique 12-character ID
# Provide a "servername" and a "docroot"

# Reload your Vagrant box with the new config settings
$ cd ~/Projects/PHP && vagrant reload --provision

# Open up your computer's hosts file
$ subl /etc/hosts

# At the bottom of this file add in the newly created domain and your Vagrant IP. Swap "mysite.dev" with the value from "servername" in config.yaml
192.168.55.25 mysite.dev
```

## How to up Sequel Pro for database management

[Install Sequel Pro](http://www.sequelpro.com/) and create a new favorite in Sequel Pro with the following info:

```
Type: SSH
MySQL Host: 192.168.55.25
Username: root
Password: vagrant

SSH Host: 192.168.55.25
SSH User: vagrant
SSH Key: click the key icon and then select ~/Projects/PHP/puphpet/files/dot/ssh/id_rsa
```

Once logged in you can now create/edit/delete databases and import/export SQL files from them.

## Quick Vagrant commands

```sh
# Checks the status of your Vagrant box (up, halted, suspended, etc)
$ vagrant status

# Resumes your Vagrant box from being halted, suspended, off
$ vagrant up

# Shuts down your Vagrant box
$ vagrant halt

# Shuts down your Vagrant box (if on) and restarts the box based on new config changes in config.yaml
$ vagrant reload --provision
```

## Versions/Other Info
- **PHP**: 5.4.35-1
- **Apache**: 2.4.10
- **MySQL**: 5.6.21-1
- **PHP memory_limit**: 512M
- **PHP upload_max_size**: 2M
