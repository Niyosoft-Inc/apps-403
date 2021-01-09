## To be run only on Worker nodes

remember to run Get tokens on one of the Master node so you can add the token the command.
```
sudo cat /var/lib/rancher/k3s/server/node-token
```

## k3s agents / workers
```
curl -sfL https://get.k3s.io | K3S_URL=https://load_balancer_ip_or_hostname:6443 K3S_TOKEN=mynodetoken sh -
```