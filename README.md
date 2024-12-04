# Assignment 3 Part 2

This repository constists of files required to configure a script to run everyday at 05:00. The first step is to create a new user

## Creating a User
For this task, you will need to create a user with no login and ownership of a directory and its subdirectories.

Creating a new user:

``` bash
sudo useradd -r -d /var/lib/webgen -s /usr/sbin/nologin webgen 
```

-r creates a new user

-d sets the home directory to the location /var/lib/webgen

-s sets the settings of the user to no login

## Creating the directory:

``` bash
sudo mkdir -p /var/lib/webgen/{bin, HTML, Documents}
```
This command will create a new directory for the user webgen and also create subdirectories.

## Setting the ownership:

``` bash
sudo chown -R webgen:webgen /var/lib/webgen
```
This command sets the ownership of the directory "webgen" and all its subdirectories to the user webgen.

## Benefits of a system user

Having a system user for this activity will allow us to prevent any accidental changes to the system. The user will have limited permissions.

## Troubleshooting
In this activity, there are times where you will need to check if the files are running or not. The below commands may help

### Enabling the timer:

``` bash
sudo systemctl enable --now generate-index.timer
```
This command will enable and start the timer

### Checking logs and confirming service's execution:

``` bash
sudo journalctl -u generate-index.service
```
This command will generate a list of logs for .service file

### Check status of nginx services and check configuration:

``` bash
sudo nginx -t
sudo systemctl status nginx
```
These two commands will show nginx's status and test it's configuration.

It is important to set up a new config file for nginx rather than making changes to the main file as it helps prevent any accidental overwriting of the main configuration file. It also makes it easier to manage.

### Checking firewall's status:

``` bash
sudo ufw status verbose
```
This command will show what the firewalls allows for incoming and outgoing.