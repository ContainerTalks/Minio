# Deploy Minio with Docker

```bash
docker run -p 9000:9000 --name minio1 -v /mnt/data:/data -v /mnt/config:/root/.minio minio/minio server /data
```

# Deploy Minio on Docker Swarm

## Prerequisites

- [Install Docker Compose](https://docs.docker.com/compose/install/)
- [Get Overview of Swarm mode key concepts](https://docs.docker.com/engine/swarm/key-concepts/)
- Read Through [Getting started with swarm mode](https://docs.docker.com/engine/swarm/swarm-tutorial/)

##  Create a Swarm Cluster

- Go through the swarm cluster creation [Create a swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/).


## Create Docker secrets for Minio or remove the secret in .yml file and set th environment

```bash
echo "HEPCM04UHDHVM2RUOF" | docker secret create access_key -
echo "RUOF2017m11i22T19nio04CLUSTER" | docker secret create secret_key -
```

## run

```bash
docker stack deploy --compose-file=stack.yml minio_stack
```

OR

```bash
docker stack deploy -c minio-stack.yaml minio_stack
```

## check the status of the stack

#### list stack

```bash
docker stack ls
```

#### list services

```bash
docker service ls
```

#### check logs of the service

```bash
docker service logs <Service_ID>
```
