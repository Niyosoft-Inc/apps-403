## k3s servers

Here are the commands used in the demo, On your k3s servers/Control Plane/Master Node run this command
(note that these have to be run on both controller servers)

Set up some environment variables:
```
export K3S_DATASTORE_ENDPOINT='mysql://username:password@tcp(database_ip_or_hostname:port)/database'
```

then

```
curl -sfL https://get.k3s.io | sh -s - server --node-taint CriticalAddonsOnly=true:NoExecute --tls-san load_balancer_ip_or_hostname
```

test with
```
sudo k3s kubectl get nodes
```
---

In order to run kubectl without sudo on Master servers, run this;
```
sudo chmod 644 /etc/rancher/k3s/k3s.yaml
```

Get tokens
```
sudo cat /var/lib/rancher/k3s/server/node-token
```
