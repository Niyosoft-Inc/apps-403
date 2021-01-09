## Create a load balancer using 

nginx.conf
```
#uncomment this next line if you are NOT running nginx in docker
#load_module /usr/lib/nginx/modules/ngx_stream_module.so;

events {}

stream {
  upstream k3s_servers {
    server <controller 1 private ip>:6443;
    server <controller 2 private ip>:6443;
  }

  server {
    listen 6443;
    proxy_pass k3s_servers;
  }
}
```
