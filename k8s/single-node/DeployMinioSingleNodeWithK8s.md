# Deploy MinIO as Single Node with k8s
Clone the repo or create the files as required from the repo path 
``
### Namespace
- Create namespace  `kubectl apply -f Namespace.yml`

### Persistent Volume and Persistent Volume Claim

- Create persistent volume and persistent volume claim `kubectl apply -f PersistentVolume.yml -f PersistentVolumeClaim.yml`
> Update path when you do chnages in your machine for host volume path. 

### Secrets
- Create secrets for `MINIO_ROOT_USER` and `MINIO_ROOT_PASSWORD`
```bash
echo -n 'CHNAGE_ME_FOR_MINIO_ROOT_USER' | base64
echo -n 'CHNAGE_ME_FOR_MINIO_ROOT_PASSWORD' | base64
```
Update the values in `Secrets.yml` and  `kubectl apply -f Secrets.yml`

### Deployment and Service
- Create label for application to run on the selected node, deployment
- Add label to the k8s node where you want to run the application
```bash
$ k get nodes
NAME          STATUS   ROLES                  AGE   VERSION
raspberrypi   Ready    control-plane,master   12h   v1.30.3+k3s1

```

```bash
kubectl label nodes raspberrypi env=minio
```

- Update the label in the deployment file
```yml
selector:
    matchLabels:
      app: minio
```

`kubectl apply -f Deployment.yml -f Service.yml`
