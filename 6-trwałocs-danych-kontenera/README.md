# 6. Trwałość danych kontenera

### 6.1 Dane kontenera oraz zapisywanie zmian zachodzących w kontenerze
```bash
# Zapisanie stanu kontenera jako obraz
docker container commit <CONTAINER_NAME> <IMAGE_NAME:TAG>
docker container commit my_ubuntu myubuntu:1.0

# 
docker container run -d -p 8080:80 --name mynginx nginx:latest
cd /var/lib/docker
sudo ls
cd containers
sudo su
cd containers
ls  ##katalogi o nazwach jak id kontenerów
docker exec -it mynginx bash
  apt-get update && apt-get install -y vim
  vi /usr/share/nginx/html/index.html
  exit
curl localhost:8080
docker container inspect mynginx | grep MergedDir # zapisanie zwróconej ścieżki
cd ..
cd overlay2
cd 7b24103b409d41442c466569b348189c73b8be1fc0049d7433bc7e90a6655faa
ls -l
cd merged
cat ./usr/share/nginx/html/index.html
cd /
docker container commit mynginx mynginx:1.0
docker image ls
docker container run -d -p 8081:80 --name mynginx1 mynginx:1.0
curl localhost:8081
docker container rm mynginx --force
docker container run -d -p 8080:80 --name mynginx nginx:latest
curl localhost:8080
curl localhost:8081
```
