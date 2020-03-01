# Setting up a web server on a Raspberry Pi

You can use a web server on a Raspberry Pi to host a full website (locally on your network or globally on the internet), or just use it to display some information you wish to share to other machines on your network.

Various web servers are available, with different advantages for usage:

* Apache
* NGINX

Apache is a popular web server application you can install on the Raspberry Pi to allow it to serve web pages. On its own, Apache can serve HTML files over HTTP, and with additional modules can serve dynamic web pages using scripting languages such as PHP.

NGINX (pronounced engine x) is a popular lightweight web server application you can install on the Raspberry Pi to allow it to serve web pages. Like Apache, NGINX can serve HTML files over HTTP, and with additional modules can serve dynamic web pages using scripting languages such as PHP.

## Setting up an NGINX Web Server on a Raspberry Pi

Ensure that the package manager has up-to-date information about which packages are available:

`sudo apt update`

#### Uninstall Apache (if necessary)

`sudo apt-get purge apache2`

#### Install NGINX

`sudo apt install nginx`

and start the server with:

`sudo /etc/init.d/nginx start`

## Test the web server

Check that the apache2/nginx service is running:

`sudo systemctl list-units --type=service`

By default, NGINX puts a test HTML file in the web folder. This default web page is served when you browse to http://localhost/ on the Pi itself, or http://192.168.1.10 (whatever the Pi's IP address is) from another computer on the network. To find the Pi's IP address, type `hostname -I` at the command line (or read more about finding your IP address).

Browse to the default web page either on the Pi or from another computer on the network and you should see the following:

![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)

## Enable HTTPS on your website

To enable HTTPS on your website, you need to get a certificate (a type of file) from a Certificate Authority (CA). Let’s Encrypt is a CA. In order to get a certificate for your website’s domain from Let’s Encrypt, you have to demonstrate control over the domain. With Let’s Encrypt, you do this using software that uses the ACME protocol which typically runs on your web host.

To figure out what method will work best for you, you will need to know whether you have shell access (also known as SSH access) to your web host. If you manage your website entirely through a control panel like cPanel, Plesk, or WordPress, there’s a good chance you don’t have shell access. You can ask your hosting provider to be sure.

### With Shell Access

We recommend that most people with shell access use the Certbot ACME client. It can automate certificate issuance and installation with no downtime. It also has expert modes for people who don’t want autoconfiguration. It’s easy to use, works on many operating systems, and has great documentation. 

Depending on the operating system and the the web server software, instructions can be found on 
[Certbot](https://certbot.eff.org/) 

#### SSH into the server

SSH into the server running your HTTP website as a user with sudo privileges.

`ssh user@78.233.56.229`

#### Find the architecture of the operating system

`hostnamectl`

#### Install Certbot

Run this command on the command line on the machine to install Certbot.

`sudo apt-get install certbot python-certbot-nginx`

#### Choose how to run Certbot

##### Option 1: Get and install certificates...

Run this command to get a certificate and have Certbot edit your Nginx configuration automatically to serve it, turning on HTTPS access in a single step.

`sudo certbot --nginx`

It modifies the configuration file `/etc/nginx/sites-enabled/default`

##### Option2: Get a certificate

If you're feeling more conservative and would like to make the changes to your Nginx configuration by hand, run this command.

`sudo certbot certonly --nginx`

#### Test automatic renewal

The Certbot packages on your system come with a cron job or systemd timer that will renew your certificates automatically before they expire. You will not need to run Certbot again, unless you change your configuration. You can test automatic renewal for your certificates by running this command:

`sudo certbot renew --dry-run`

Automatic renewal of certbot

`sudo crontab -e`

Add the following line 

`30 4 1 * * sudo certbot renew --quiet`

## Python

Python is a wonderful and powerful programming language that's easy to use (easy to read and write) and, with Raspberry Pi, lets you connect your project to the real world.

Python syntax is very clean, with an emphasis on readability, and uses standard English keywords. 

Check whether you already have an up to date version of Python installed by entering python in a command line window. If you see a response from a Python interpreter it will include a version number in its initial display. Generally any Python 3.x version will do, as Python makes every attempt to maintain backwards compatibility within major Python versions. Python 2.x and Python 3.x are intentionally not fully compatible. If python starts a Python 2.x interpreter, try entering python3 and see if an up to date version is already installed. 

`python3 --version`

### Executing Python files from the command line

The standard built-in Python shell is accessed by typing `python3` in the terminal.

This shell is a prompt ready for Python commands to be entered. You can use this in the same way as Thonny, but it does not have syntax highlighting or autocompletion. You can look back on the history of the commands you've entered in the REPL by using the Up/Down keys. Use `Ctrl + D` to exit.

You can write a Python file in a standard editor like Vim, Nano, or LeafPad,

hello.py
`print("Hello World!")`

Run it as a Python script from the command line. Just navigate to the directory the file is saved in (use cd and ls for guidance) and run with python3, e.g. 

`python3 hello.py`

### Installing Python libraries

#### apt

Some Python packages can be found in the Raspbian archives, and can be installed using apt, for example:

`sudo apt update`
`sudo apt install python-picamera`

This is a preferable method of installing, as it means that the modules you install can be kept up to date easily with the usual sudo apt update and sudo apt full-upgrade commands.

#### pip

Not all Python packages are available in the Raspbian archives, and those that are can sometimes be out of date. If you can't find a suitable version in the Raspbian archives, you can install packages from the Python Package Index (known as PyPI).

To do so, install pip:

`sudo apt install python3-pip`

Then install Python packages (e.g. simplejson) with pip3:

`sudo pip3 install simplejson`

Read more on installing software in Python [here] (https://www.raspberrypi.org/documentation/linux/software/python.md).

#### piwheels

The official Python Package Index (PyPI) hosts files uploaded by package maintainers. Some packages require compilation (compiling C/C++ or similar code) in order to install them, which can be a time-consuming task, particlarly on the single-core Raspberry Pi 1 or Pi Zero.

piwheels is a service providing pre-compiled packages (called Python wheels) ready for use on the Raspberry Pi. Raspbian is pre-configured to use piwheels for pip. Read more about the piwheels project at [www.piwheels.org](www.piwheels.org).


