## To install kubectl see this link here:
### https://kubernetes.io/docs/tasks/tools/install-kubectl/

kubeconfig location is on Master server in this path;
```
/etc/rancher/k3s/k3s.yaml
```

copy the outcome of the contents to your dev machine
```
sudo cat /etc/rancher/k3s/k3s.yaml
```

Configuring Kubectl for Remote Access, to manage a remote cluster.
To do so Create the file config on your dev machine
```
~/kube/config
```

Be sure to update the server: to your load balancer ip or hostname
