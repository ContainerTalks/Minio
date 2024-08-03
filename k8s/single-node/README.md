# Deploy Minio as single node in kubernetes cluster

### Create namespace
kubectl apply -f namespace.yaml

### Create persistent volume and persistent volume claim

kubectl apply -f persistentvolume.yaml
kubectl apply -f persistentvolumeclaim.yaml

### Create secrets
# echo -n 'your-root-user' | base64
# echo -n 'your-root-password' | base64

update the values in secrets.yaml

kubectl apply -f secrets.yaml

### Create deployment and service

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
