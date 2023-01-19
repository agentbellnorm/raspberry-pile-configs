### get ip of nodes 
```sh
sudo nmap -sP 192.168.1.1/24 | grep -B 2 Raspberry
```

### get bearer token for dashboard
```sh
kubectl -n kubernetes-dashboard describe secret admin-user-token | grep '^token'
```

### Artiklar
init: https://sahansera.dev/building-your-own-private-kubernetes-cluster-on-a-raspberry-pi-4-with-k3s/
resten: https://bryanbende.com/categories.html


## todo new nodes
```
sudo apt-get update && sudo apt-get upgrade
```

add `cgroup_memory=1 cgroup_enable=memory` to `/boot/cmdline.tx`

#### change hostname
```
sudo vi /etc/hostname
```
  
#### enable rancher
```
sudo apt-get install open-iscsi
```

### enable registry
- create `/etc/rancher/k3s/registries.yaml`
- add content from https://bryanbende.com/development/2021/07/02/k3s-raspberry-pi-jenkins-registry-p1
- own the file `sudo chmod go-r /etc/rancher/k3s/registries.yaml`
- add registry.docker.private to `sudo vi /etc/hosts`

 reboot

### install k3s
#### get token from host 
```
sudo cat /var/lib/rancher/k3s/server/token
```
#### join cluster
```
curl -sfL https://get.k3s.io | K3S_NODE_NAME="node02" K3S_URL="https://192.168.1.79:6443" K3S_TOKEN="<token>" sh -
```


  