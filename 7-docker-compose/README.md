# 7. Docker-compose

### 7.1 Wprowadzenie do docker-compose

```yml
version: '3.7'

services:
  servicename: # WYMAGANE: dowolna nazwa ustalona przez Ciebie
    image: # OPCJONALNE: może być pominięty gdy korzystamy z "build"
    container_name: # OPCJONALNE: wymuszamy nazwę kontenera.
    command: # OPCJONALNE: możemy zastąpić CMD z Dockerfile
    ports: # OPCJONALNE: mapujemy porty
    environment: # OPCJONALNE: zmienne środowiskowe. przykład: "-e MY_SQL_PASSWORD=1"
    volumes: # OPCJONALNE: odpowiednik "-v" w docker container run
  servicename-2:
    image: # OPCJONALNE: może być pominięty gdy korzystamy z "build"
    restart: # OPCJONALNE: określamy politykę restartów
      
volumes: # OPCJONALNE

networks: # OPCJONALNE
```

```bash
cd 7.1
docker-compose up
docker container ls -a
docker-compose up -d
docker-compose ps
docker-compose down
docker container ls -a
docker volume ls
docker-compose down -v #-v usuwa również utworzone volumeny
```

### 7.2 Automatyczne budowanie obrazów
```bash
docker-compose build # wymusza przebudowanie obrazu
docker-compose up --build # wymusza przebudowanie obrazu

#
cd 7.2
docker-compose config
docker-compose build
docker-compose up -d
docker-compose down
# zmiana w pliku 7.2/ui/src/App.js
docker-compose build
docker-compose up -d
docker-compose down
```
