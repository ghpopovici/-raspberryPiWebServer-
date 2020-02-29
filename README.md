# -raspberryPiWebServer-
# Setting up a web server on a Raspberry Pi

You can use a web server on a Raspberry Pi to host a full website (locally on your network or globally on the internet), or just use it to display some information you wish to share to other machines on your network.

Various web servers are available, with different advantages for usage:

* Apache
* NGINX

## Setting up an Apache Web Server on a Raspberry Pi

Apache is a popular web server application you can install on the Raspberry Pi to allow it to serve web pages.

On its own, Apache can serve HTML files over HTTP, and with additional modules can serve dynamic web pages using scripting languages such as PHP.

## Setting up an NGINX web server on a Raspberry Pi

NGINX (pronounced engine x) is a popular lightweight web server application you can install on the Raspberry Pi to allow it to serve web pages.

Like Apache, NGINX can serve HTML files over HTTP, and with additional modules can serve dynamic web pages using scripting languages such as PHP.

### Refresh database of available packages

Ensure that the package manager has up-to-date information about which packages are available: 

`sudo apt update`

#### Uninstall Apache (if necessary)

`sudo apt-get purge apache2`

#### Install NGINX

First install the nginx package by typing the following command in to the Terminal:

`sudo apt install nginx`

and start the server with:

`sudo /etc/init.d/nginx start`

#### Test the web server

By default, NGINX puts a test HTML file in the web folder. This default web page is served when you browse to http://localhost/ on the Pi itself, or http://192.168.1.10 (whatever the Pi's IP address is) from another computer on the network. To find the Pi's IP address, type hostname -I at the command line (or read more about finding your IP address).

Browse to the default web page either on the Pi or from another computer on the network and you should see the following:

![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)

