# Longhorn

`00-longhorn.yaml` is a copy of the original  [v1.1.1/deploy/longhorn.yaml](https://raw.githubusercontent.com/longhorn/longhorn/v1.1.1/deploy/longhorn.yaml) with the default number of replicas modified from 2 to 3.

An alternative is to create a custom storage class that has 2 replicas. For an example, see `05-longhorn-custom-storage-class.yaml`.

If creating the longhorn ingress with TLS, then the `cert-manager` setup must be completed first.

## Upgrading

https://longhorn.io/docs/1.7.2/deploy/upgrade/

- scale down all deployments with pvc:s
- make sure upgrade path is supported (only patch + 1 typically e.g. 1.6.x -> 1.7.x)
- apply the upgrade (e.g. kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/v1.7.2/deploy/longhorn.yaml)
- upgrade the engine image of all the volumes
 - can do for all volumes at the once.


## Backups

- get the access key and secret access key from aws, encode them with `pbpaste | base64`
- update `s3-backup-secret.yaml`
- apply with `kubectl -n longhorn-system apply -f s3-backup-secret.yaml`
