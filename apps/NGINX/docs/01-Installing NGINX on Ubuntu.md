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
```
curl -o nginx_signing.key http://nginx.org/keys/nginx_signing.key
```
```
sudo apt-key add nginx_signing.key
```

Now that we’ve added the signing key, we can set up the apt repository by appending the following lines to /etc/apt/sources.list:
```
sudo vim /etc/apt/sources.list
```

/etc/apt/sources.list (partial)
```
## Add official NGINX repository
deb http://nginx.org/packages/ubuntu/ xenial nginx
deb-src http://nginx.org/packages/ubuntu/ xenial nginx
```

With that file updated, we can install NGINX using apt-get after we update:
```
sudo apt-get update
sudo apt-get install -y nginx
```
Note: This command will install the “stable” version of NGINX, which might not be the newest version.

## Starting and Enabling NGINX
Although we’ve installed NGINX, it is not currently running. We’re going to use systemd to run NGINX as a service and set it to start when our server boots up.
```
sudo systemctl start nginx
sudo systemctl enable nginx
```

Next, we’ll stop and start the server. Once the reboot has finished, we should be able to visit the server’s IP address in our browser and see the default landing page.
