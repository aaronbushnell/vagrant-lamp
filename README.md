# Simple LAMP server using Vagrant

## Before you install
[Install Vagrant 1.6.5](https://www.vagrantup.com/download-archive/v1.6.5.html). Newer versions might not work, so use 1.6.5 for now.

## Installation

1. Create an empty directory that should house all of your projects `$ mkdir ~/Projects # if available`
2. Clone repo `$ git clone [repoUrl] ~/Projects/PHP`
3. Setup the public/ directory for your sites `$ mkdir ~/Projects/PHP/public`
4. Kickstart your new Vagrant box `$ cd ~/Projects/PHP && vagrant up`

You will now have a Vagrant box running at 192.168.55.25

## Setting up a new site

1. Open up ~/Projects/puphpet/config.yaml
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
