# ArgoCD

Followed guide: https://argo-cd.readthedocs.io/en/stable/getting_started/

Installerade:
```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Set default namespace:
```sh
kubectl config set-context --current --namespace=argocd
```

Port forwarding to access:
```sh
kubectl port-forward svc/argocd-server -n argocd 8082:443
```

Get password
```sh
argocd admin initial-password -n argocd
```
