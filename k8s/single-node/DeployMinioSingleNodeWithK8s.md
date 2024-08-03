# Deploy Minio as single node with k8s

- Create namespace  `kubectl apply -f Namespace.yaml`
- Create persistent volume and persistent volume claim `kubectl apply -f PersistentVolume.yaml -f PersistentVolumeClaim.yaml`
- Create secrets
```bash
echo -n 'your-root-user' | base64
echo -n 'your-root-password' | base64
```
Update the values in secrets.yaml and  `kubectl apply -f Secrets.yaml`

- Create deployment and service `kubectl apply -f Deployment.yaml -f Service.yaml`
