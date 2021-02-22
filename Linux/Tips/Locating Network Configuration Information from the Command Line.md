## Locating Network Configuration Information from the Command Line

### Determine the IP Address

1. List the current working directory.
```
pwd
```

2. Run the following command:
```
sudo ip addr show
```

3. Enter your `cloud_user ` password at the prompt.
4. Locate the line that begins with `inet` (for the IPv4 address), or the line that begins with `inet6` (for the IPv6 address)
5. Note the address.


### Determine the MAC Address
1. In the output of the `sudo ip addr show` command, locate the line that begins with `link/ether`.
2. Note the address.

### Determine the Gateway
1. Show the routing table.
```
sudo ip route show
```
2. Locate the line that begins with `default via`, and note the address.


### Determine the DNS Server
1. Show the DNS nameserver.
```
cat /etc/resolv.conf | grep nameserver
```
2. Note the DNS server in the output.
