# 5. Komunikacja pomiędzy kontenerami

### 5.1 Sieć typu bridge
```bash
docker network create -d bridge mybridge
docker run -d --net mybridge --name db postgress:9.6
docekr run -d --net mybridge -e DB=db -p 8080:3000 --name web mywebapp:1.0

#
docker container run -itd --name ubuntu1 ubuntu bash
docker container run -itd --name ubuntu2 ubuntu bash
docker container inspect ubuntu1
# pobranie adresu IP kontenera ubuntu1- 172.17.0.2
docker container exec -it ubuntu2 bash
  apt-get update && apt-get install -y iputils-ping
  ping ubuntu1
  ping 172.17.0.2
  exit
docker network ls
docker network inspect bridge
docker network create -d bridge custombridge
docker network ls
docker container run -itd --name ubuntu3 --net custombridge ubuntu bash
docker container run -itd --name ubuntu4 --net custombridge ubuntu bash
docker container ls
docker container inspect ubuntu3  #IP: 172.18.0.2
docker container exec -it ubuntu4 bash
  apt-get update && apt-get install -y iputils-ping
  ping ubuntu3
  ping 172.18.0.2
  exit
docker network connect custombridge ubuntu1 #kontener podłączony do 2 sieci
docker network inspect custombridge
docker network inspect bridge
docker container inspect ubuntu1
docker network disconnect custombridge ubuntu4
docker container inspect ubuntu4
```
