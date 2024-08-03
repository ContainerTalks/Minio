# Configuring AWS CLI to Connect with MinIO and Basic Operations

## Prerequisites
1. MinIO Server
2. AWS CLI

## Installing AWS CLI

```bash
pip3 install awscli --upgrade --user
```

## Configuring AWS CLI for MinIO
### Create AWS CLI Profile for MinIO
#### Configure Credentials
Create or edit the `~/.aws/credentials` file and add your MinIO access key and secret key:

> Replace YOUR_MINIO_ACCESS_KEY and YOUR_MINIO_SECRET_KEY with the credentials you created for MinIO from [http://localhost:[MINIO_PORT]/access-keys]

```bash
[minio]
aws_access_key_id = YOUR_MINIO_ACCESS_KEY
aws_secret_access_key = YOUR_MINIO_SECRET_KEY
```

#### Configure the Endpoint

Create or edit the `~/.aws/config` file and set the endpoint URL 

```bash
[profile minio]
s3 =
    endpoint_url = http://192.168.1.40:30000
    signature_version = s3v4
```

In my case I am running on raspberrypi deployed application with nodeport 30000 for API. 

### Verify Configuration

```bash
aws s3 ls --endpoint-url http://192.168.1.40:30000 --profile minio
```

## Basic Operations with MinIO

-  List Buckets `aws s3 ls --endpoint-url http://192.168.1.40:30000 --profile minio`
-  List Objects in a Bucket `aws s3 ls s3://container-talks-docs --endpoint-url http://192.168.1.40:30000 --profile minio`
- Upload a File `aws s3 cp DeployMinioSingleNodeWithK8s.md s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md --endpoint-url http://192.168.1.40:30000 --profile minio`

```bash
balu@raspberrypi:~/Minio/k8s/single-node $ aws s3 ls s3://container-talks-docs --endpoint-url http://192.168.1.40:30000 --profile minio

balu@raspberrypi:~/Minio/k8s/single-node $ aws s3 cp DeployMinioSingleNodeWithK8s.md s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md --endpoint-url http://192.168.1.40:30000 --profile minio
upload: ./DeployMinioSingleNodeWithK8s.md to s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md

balu@raspberrypi:~/Minio/k8s/single-node $ aws s3 ls s3://container-talks-docs --endpoint-url http://192.168.1.40:30000 --profile minio
2024-08-04 00:57:58       2471 DeployMinioSingleNodeWithK8s.md
```

- Download a File `aws s3 cp s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md DeployMinioSingleNodeWithK8sTestDownload.md --endpoint-url http://192.168.1.40:30000 --profile minio`

OUTPUT 
```bash
download: s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md to ./DeployMinioSingleNodeWithK8sTestDownload.md

ls | grep .md
DeployMinioSingleNodeWithK8s.md
DeployMinioSingleNodeWithK8sTestDownload.md
```

- Delete a File `aws s3 rm s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md --endpoint-url http://192.168.1.40:30000 --profile minio`

OUTPUT `delete: s3://container-talks-docs/DeployMinioSingleNodeWithK8s.md`

