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
