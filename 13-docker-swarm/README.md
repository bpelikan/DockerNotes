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