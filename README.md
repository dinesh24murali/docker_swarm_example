# Docker swarm example

Integrating Docker swarm on a simple NodeJS Application

Step 1:

To host the repositories locally we can use a docker container called [registry:2](https://hub.docker.com/_/registry).


```
docker service create --name registry --publish published=5000,target=5000 registry:2
```

Step 2:

Build the nodeapp service to create the image

```
docker compose -f docker-compose.yml build nodeapp
```

Publish the image to the local registry

```
docker compose -f docker-compose.yml push nodeapp
```

Step 3:

Run docker swarm:

retrieve the private IP address of the machine using the following command:
```
hostname -I | awk '{print $1}'
```

run the following command to enable docker swarm

```
docker swarm init --advertise-addr <public ip address>
```

```
docker stack deploy -c docker-compose.yml node_stack
```

Goto [http://localhost:3030/](http://localhost:3030/) in you browser to see the text `Hello world!`

It means you have successfully ran docker swarm with traefik
