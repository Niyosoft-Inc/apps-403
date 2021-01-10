## Creating a Load Balancer using HAProxy.

Labs Servers name:
```
Server1
Node2
Node1
Client1
```

The Scenario
A business unit is requesting our assistance in resolving some performance issues. They've had additional application nodes created, but need us to build a load balancer that acts as their front end.

The application nodes will listen on port 8080, and the load balancer should listen on port 80 for web traffic.

Get logged in
Use the credentials and server IP in the hands-on lab overview page to log into our lab server. Notice there are multiple machines we're working with. Pay attention in the lab guide, as the shell prompt will reveal which one we're working with at the moment.

Install HAProxy on Server1
Before we do anything else, let's run a sudo -i right off. Then we'll be root and won't have to keep typing in a password.

Now, we'll start off by installing HAProxy:
```
yum -y install haproxy
```

Enable and start the service:
```
systemctl enable haproxy
systemctl start haproxy
```

Then verify that incoming port 80 traffic is permitted through the firewall.
Running ```firewall-cmd --list-all``` should show `http` in the list of allowed services.

Configure HAProxy on `Server1`
We need to configure the HAProxy's frontend and backend. HAProxy should listen on port 80, and use `node1` and `node2` as the backend nodes.
Let's edit :
```
/etc/haproxy/haproxy.cfg
```
and add the configuration code:
```

    timeout check            10s
    maxconn                  3000

# Our code starts here:

frontend app1
        bind *:80        
        mode http
        default_backend apache_nodes

backend apache_nodes
        mode http
        balance source        
        server node1 10.0.1.20:8080 check
        server node2 10.0.1.30:8080 check

# End of our code
#-------------------------------------------------------
# main frontend which proxys to the backends
#-------------------------------------------------------
```

We'll have to restart the daemon so that our changes take effect, then check with `ss`:
```
systemctl restart haproxy
ss -lntp
```

Configure the `node1` and `node2` Firewalls
We need to permit incoming port 8080/TCP traffic on `node1` and `node2`. On each node (after logging in, then becoming `root`), perform the following:
```
firewall-cmd --permanent --add-port=8080/tcp
```

Then reload the firewall configuration:
```
firewall-cmd --reload
```

From `Client1`, Validate That Settings Are Correct
On `Client1`, we can run a `curl` on the `Server1` private IP address:
```
curl <Server1_IP_ADDRESS>
```

We should get a reply from either `node1` or `node2`. Something like `<h1>Node 1<h1>`.

While this means we're up and running, if we ``really`` want to test, we'll go shut down the one we didn't hear from. In this case, we got a reply from `node1`, so if we log into it (with SSH), then shut down the web server (with `sudo systemctl stop httpd`), another `curl` command from `Client1` will get us a reply. But this time it will be `node2` serving up the web page.

Conclusion
We have two web servers, and they're each serving up traffic sent to them by a load balancer that we've just set up and tested. This is exactly what we wanted to have working. Congratulations!



