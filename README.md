# Docker Swarm: A basic example with docker-in-docker

It consists of a docker swarm example initializing a manager node and other two workers nodes in the same local machine using **docker-in-docker**.

## How to run

First, run the **initSwarmNodes** script to initialize the docker swarm nodes - manager(s) and worker(s) - using the following command:

```console
.\initSwarmNodes.ps1
```

Then, run the portainer in order to manage and visualize the docker swarm status with the following command:

```console
docker stack deploy -c portainer.yml portainer 
```

## With services

In case you finally want to inject some kind of service into the docker swarm nodes, you can use the following template command:

### Using ports
```console
docker service create --name <service-name> --replicas <n-of-replicas> -p <port:port> <service-type> 
```

### or not
```console
docker service create --name <service-name> --replicas <n-of-replicas> <service-type> 
```

### Examples:
```console
docker service create --name web-server --replicas 3 -p 80:80 nginx
```
```console
docker service create --name redis --replicas 2 redis 
```

## How to stop

If you injected services on docker swarm nodes, you can remove all of them with the following command:
```console
docker service rm (docker service ls -q)
```

Instead, in case you don't, you can simply stop and remove all the containers with the following commands:
```console
docker stop (docker ps -q)
docker rm (docker ps -aq) 
```
Finally, you can leave the docker swarm created running the command:
```console
docker swarm leave --force
```
