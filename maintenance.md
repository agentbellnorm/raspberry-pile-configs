### Connect to nodes
ssh pi@192.168.50.136|controlplane (it's the cute password)

### Get k3s config from cluster
Copy from `/etc/rancher/k3s/k3s.yaml` on the pi to `~/.kube/config` on the remote and change the ip to the ip on the network, e.g. 192.168.50.136

https://docs.k3s.io/cluster-access

### Access the k3s dashboard
Create a proxy from the cluster to remote machine 

On the remote machine
```sh
kubectl proxy
```

Then go to http://127.0.0.1:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login

### Get the token
```sh
kubectl -n kubernetes-dashboard describe secret admin-user-token | grep '^token' 
```

https://docs.k3s.io/installation/kube-dashboard#obtain-the-bearer-token

### Access the longhorn dashboard
Add 
```sh
<ip e.g. 192.168.50.136> longhorn-ui
```
to `/etc/hosts` on remote machine

go to https://longhorn-ui/ 
self signed https is enabled according with https://github.com/agentbellnorm/raspberry-pile-configs/blob/main/longhorn/longhorn.ingress-tls.yaml

### Restart a deployment
```sh
kubectl -n <namespace> scale --replicas=0 deployment <deployment>

# e.g.
kubectl -n skum-matrix scale --replicas=0 deployment matrix-synapse
```
Then just scale it to 1 again.
