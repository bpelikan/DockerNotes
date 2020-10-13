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

### 7.3 Zmienne środowiskowe
Plik `.env` 
* zmienne środowiskowe na hoście mają większy priorytet
* zmienne środowiskowe zdefiniowane w terminalu mają najwyższy priorytet
lub `env_file` do załączenia w docker-compose.yml
* przekazanie zmiennych bezpośrednio do kontenera

```bash
docker-compose config
export DB_NAME="FromShellDbName"
docker-compose config
docker-compose -f docker-compose.envfile.yml config
docker-compose up -d
docker-compose down
```
### 7.4 Wiele instancji na podstawie tego samego pliku YAML
```bash
cd 7.4
export WP_PORT="9091" #$Env:WP_PORT="9091" dla PowerShella
docker-compose -p dev up -d
export WP_PORT="9092"
docker-compose -p staging up -d
export WP_PORT="9093"
docker-compose -p prod up -d
docker container ls
docker-compose -p prod down
docker-compose -p staging down
docker-compose -p dev down
docker container ls
```
