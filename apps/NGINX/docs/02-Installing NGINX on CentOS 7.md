## Installing NGINX on CentOS 7

To start digging into NGINX, we first need a server. In this video, we’ll set up a CentOS 7 server with Nginx.

Documentation For This demo
- `Official NGINX Installation Documentation` can be found here:
  #### http://nginx.org/en/linux_packages.html
- `systemd` documentation can be found here:
   #### https://www.freedesktop.org/wiki/Software/systemd/
   
## Adding the Official NGINX Repository.
For us to install NGINX using `yum` we will add the official NGINX repository by creating a file at `/etc/yum.repos.d/nginx.repo`:
```
sudo vim /etc/yum.repos.d/nginx.repo
```

`/etc/yum.repos.d/nginx.repo`
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

This repo will give us access to the “stable” branch of NGINX to install. If you’d like to install the “mainline” branch of NGINX, change the “baseurl” to “http://nginx.org/packages/mainline/centos/7/$basearch/”. Before we can install, we need to run `yum update`.
```
sudo yum update
```

## Installing NGINX.

Now that we have the repository, let’s install NGINX now:
```
sudo yum install -y nginx
```

Note: This command will install the “stable” version of NGINX, which might not be the newest version.

Starting and Enabling NGINX
Although we’ve installed NGINX, it is not currently running. We’re going to use systemd to run NGINX as a service and set it to start when our server boots up.
```
sudo systemctl start nginx
sudo systemctl enable nginx
```

Next, we’ll stop and start the server from the Linux Academy cloud server window. Once the reboot has finished, we should be able to visit the server’s IP address in our browser and see the default landing page.
