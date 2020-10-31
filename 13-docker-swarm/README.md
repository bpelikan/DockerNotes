# 13. Docker Swarm

### 13.1 Czym jest Docker Swarm

* [Play with Docker](https://labs.play-with-docker.com/)

### 13.2 Sieć overlay

```bash
docker swarm init
docker network create -d overlay myoverlay
docker network ls
docker container run -d -p 80:80 --name mynginx --network myoverlay nginx:1.17 #error - nie można podłączyć sieci do pojedynczego kontenera
docker network inspect myoverlay # "Attachable": false
docker network rm myoverlay
docker network create -d overlay --attachable myoverlay
docker network ls
docker container rm mynginx --force
docker container run -d -p 80:80 --name mynginx --network myoverlay nginx:1.17
docker network inspect myoverlay
```

### 13.3 Tworzenie klastra

```bash
# 1
docker swarm init --advertise-addr 192.168.0.13 
docker swarm join-token manager
docker swarm join-token worker
docker node ls
docker node promote node4
docker node ls
docker node demote node3
```
### 13.4 Docker Swarm Services
```bash
docker service create --name mynginx -d -p 8080:80 --replicas 3 nginx:1.16.1
docker service ls
docker service ps mynginx

docker service scale mynginx=6
docker service ls
docker service ps mynginx

docker service update --image nginx:1.17.8 mynginx
docker service ls
docker service ps mynginx

docker node update --availability drain manager2 #node2/manager2 przestaje być dostepny
docker service ls
docker service ps mynginx
```