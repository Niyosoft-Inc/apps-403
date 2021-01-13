## Understanding the Default NGINX Configuration.

Working with NGINX is all about configuration, and in this video, we’re going to learn what the default NGINX configuration is to see how it works.

Note: the commands in this video are run as the `root` user.

### Documentation For This demo:

- [user directive](http://nginx.org/en/docs/ngx_core_module.html#user)
- [worker_processes directive](http://nginx.org/en/docs/ngx_core_module.html#worker_processes)
- [error_log directive](http://nginx.org/en/docs/ngx_core_module.html#error_log)
- [pid directive](http://nginx.org/en/docs/ngx_core_module.html#pid)
- [events directive](http://nginx.org/en/docs/ngx_core_module.html#events)
- [worker_connections directive](http://nginx.org/en/docs/ngx_core_module.html#worker_connections)
- [include directive](http://nginx.org/en/docs/ngx_core_module.html#include)
- [default_type directive](http://nginx.org/en/docs/http/ngx_http_core_module.html#default_type)
- [http directive](http://nginx.org/en/docs/http/ngx_http_core_module.html#http)
- [log_format directive](http://nginx.org/en/docs/http/ngx_http_log_module.html#log_format)
- [sendfile directive](http://nginx.org/en/docs/http/ngx_http_core_module.html#sendfile)
- [access_log directive](http://nginx.org/en/docs/http/ngx_http_log_module.html#access_log)
- [keepalive_timeout directive](http://nginx.org/en/docs/http/ngx_http_core_module.html#keepalive_timeout)


## Default NGINX Configuration
We didn’t need to set up any configuration for NGINX to serve up the default index page. That is because NGINX comes with a default configuration that can be found at `/etc/nginx/nginx.conf`. Most of what we’re going to be doing would require `sudo`, so let’s switch to being the `root` user before we begin:
```
sudo su
cd /etc/nginx
```

Let’s take a look at what’s in the default configuration file:
```
/etc/nginx/nginx.conf
```

```
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;


log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent "$http_referer" '
                  '"$http_user_agent" "$http_x_forwarded_for"';

access_log  /var/log/nginx/access.log  main;

sendfile        on;
#tcp_nopush     on;

keepalive_timeout  65;

#gzip  on;

include /etc/nginx/conf.d/*.conf;

}
```

Let’s unpack this section by section to understand what’s going on. The first few lines of the file exist outside of any specific context:
```
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
```

- [user](http://nginx.org/en/docs/ngx_core_module.html#user) directive - specifies which user the worker processes should run under.
- [worker_processes](http://nginx.org/en/docs/ngx_core_module.html#worker_processes) directive - lets us specify the number of worker processes to use.
- [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log) directive - sets the file to log errors and what level of messages to log.
- [pid](http://nginx.org/en/docs/ngx_core_module.html#pid) directive - defines the files that store the PID of the main process.


The next section is our first “context” called `events`.
```
events {
    worker_connections  1024;
}
```

A context in NGINX is expressed using curly braces (`{` and `}`), and certain directives only work in very specific types of contexts.
The [events](http://nginx.org/en/docs/ngx_core_module.html#events) context exists to allow us to specify how a worker process should handle connections.
In this case, the [worker_connections](http://nginx.org/en/docs/ngx_core_module.html#worker_connections) specifies the maximum number of connections that a single worker can have open at one time.

The `http` Context.

The remainder of the default `/etc/nginx/nginx.conf` file is a single [http](http://nginx.org/en/docs/http/ngx_http_core_module.html#http) context.
Here’s the entire section:
```
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent "$http_referer" '
                  '"$http_user_agent" "$http_x_forwarded_for"';

access_log  /var/log/nginx/access.log  main;

sendfile        on;
#tcp_nopush     on;

keepalive_timeout  65;

#gzip  on;

include /etc/nginx/conf.d/*.conf;

}
```

The first directive that we see is [include](http://nginx.org/en/docs/ngx_core_module.html#include), which lets us separate our configurations into different files and load them in where we need them. The `mime.types` file defines the content return types that should be used for various files that the server might render. The [default_type](http://nginx.org/en/docs/http/ngx_http_core_module.html#default_type) directive states the content type to use if the content is not defined in the types file. The next two directives are all about logging. Looking at the [log_format](http://nginx.org/en/docs/http/ngx_http_core_module.html#http) directive, we see a lot of tokens that start with a dollar sign `($)`. These tokens are variables that are available when a request is being processed, and this directive defines which should be used (and in what position) to log the request information. [access_log](http://nginx.org/en/docs/http/ngx_http_log_module.html#access_log) defines the file to log request information to.

The next directive, [sendfile](http://nginx.org/en/docs/http/ngx_http_core_module.html#sendfile) is a little complicated, but it specifies whether or not to use the `sendfile()` system call when delivering content. [keepalive_timeout](http://nginx.org/en/docs/http/ngx_http_core_module.html#keepalive_timeout) sets how long to hold onto the TCP connection for a client before opening up the connection for a new client. Lastly, the [include](http://nginx.org/en/docs/ngx_core_module.html#include) directive is used one last time to load all of the `.conf` files in the `/etc/nginx/conf.d/` directory. This is where we’ll be defining our virtual hosts as we learn throughout this course.
