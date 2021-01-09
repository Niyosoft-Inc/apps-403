## Installing NGINX on Ubuntu 16.04

To start digging into NGINX, we first need a server. In this demo, we’ll set up an Ubuntu 16.04 cloud server with Nginx.

Documentation For This demo
- Official NGINX Installation Documentation can be found here:
  ##### http://nginx.org/en/linux_packages.html
- systemd
  ##### https://www.freedesktop.org/wiki/Software/systemd/

Update the Server’s Applications
Before we get too far, let’s update the software that’s already installed on our server (you can skip this if you’d rather not or know that nothing is out of date):
```
sudo apt-get update
```
```
sudo apt-get upgrade -y
```

## Installing NGINX.
For us to install NGINX, we’re going to need to add an apt repository for it. Thankfully, we can follow the official documentation (http://nginx.org/en/linux_packages.html) for how to do this.
The first thing that we need to do is download the signing key and add it using apt-key:
