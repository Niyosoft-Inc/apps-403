## To install kubectl see this link here:
### https://kubernetes.io/docs/tasks/tools/install-kubectl/

kubeconfig location on server is in this path
```
/etc/rancher/k3s/k3s.yaml
sudo cat /etc/rancher/k3s/k3s.yaml
```
copy the outcome of the contents to your dev machine

Create the file config
```
~/kube/config
```

Be sure to update the server: to your load balancer ip or hostname
