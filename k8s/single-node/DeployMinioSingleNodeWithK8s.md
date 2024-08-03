# Deploy MinIO as Single Node with k8s
Clone the repo or create the files as required from the repo path 
``

- Create namespace  `kubectl apply -f Namespace.yml`
- Create persistent volume and persistent volume claim `kubectl apply -f PersistentVolume.yml -f PersistentVolumeClaim.yml`
- Create secrets for `MINIO_ROOT_USER` and ``MINIO_ROOT_PASSWORD`
```bash
echo -n 'CHNAGE_ME_FOR_MINIO_ROOT_USER' | base64
echo -n 'CHNAGE_ME_FOR_MINIO_ROOT_PASSWORD' | base64
```
Update the values in `Secrets.yml` and  `kubectl apply -f Secrets.yml`

- Create deployment and service `kubectl apply -f Deployment.yml -f Service.yml`
