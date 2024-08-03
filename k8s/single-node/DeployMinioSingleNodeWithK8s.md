# Deploy MinIO as Single Node with k8s

- Create namespace  `kubectl apply -f Namespace.yaml`
- Create persistent volume and persistent volume claim `kubectl apply -f PersistentVolume.yaml -f PersistentVolumeClaim.yaml`
- Create secrets for `MINIO_ROOT_USER` and ``MINIO_ROOT_PASSWORD`
```bash
echo -n 'CHNAGE_ME_FOR_MINIO_ROOT_USER' | base64
echo -n 'CHNAGE_ME_FOR_MINIO_ROOT_PASSWORD' | base64
```
Update the values in `Secrets.yaml` and  `kubectl apply -f Secrets.yaml`

- Create deployment and service `kubectl apply -f Deployment.yaml -f Service.yaml`
