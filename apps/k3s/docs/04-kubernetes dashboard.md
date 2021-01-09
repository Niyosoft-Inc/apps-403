## kubernetes dashboard.

check releases for the command to use here;
### https://github.com/kubernetes/dashboard/releases

At time it's:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.4/aio/deploy/recommended.yaml
```

## Dashboard RBAC Configuration.

Create a first YAML file for the ServiceAccount;

dashboard.admin-user.yml
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```

Create a second YAML file for the ClusterRoleBinding;

dashboard.admin-user-role.yml
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```

Deploy the admin-user configuration:
(if you're doing this from your dev machine, remove sudo k3s and just use kubectl)
```
sudo k3s kubectl create -f dashboard.admin-user.yml -f dashboard.admin-user-role.yml
```

get bearer token
```
sudo k3s kubectl -n kubernetes-dashboard describe secret admin-user-token | grep ^token
```

start dashboard locally
```
sudo k3s kubectl proxy
```

Then you can sign in at this URL using your token we got in the previous step:
```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```
