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

## Setting up a new site

1. Open up ~/Projects/PHP/puphpet/config.yaml
2. Find the `vhosts:` block under `apache` (not `ngnix`).
3. Copy an entire block that starts with 12-character random ID
4. Change the ID to another unique 12-character ID
5. Provide a `servername` and a `docroot`.
6. Run `$ vagrant reload --provision` in ~/Projects/PHP
7. Open up your `/etc/hosts/` file in your favorite editor and type in `192.168.55.25 mysite.dev`. Make sure you replace mysite.dev with the value from `servername` in config.yaml

## Setting up Sequel Pro for database management

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
