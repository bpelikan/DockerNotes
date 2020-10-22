# 10. Docker Advanced

### 10.2 Konfiguracja Docker Engine

Konfiguracja:
* Linux: /etc/docker/daemon.json
* Windows: Settings -> Docker Engine
* MacOS: Preferences -> Daemon -> Advanced

### 10.3 Komunikacja z Docker Daemon po HTTP

* Domyślnie komunikacja Docker Daemona z DockerCLI odbywa się przez Unix Sockets (/var/run/docker.sock) i wymaga uprawnień dla grupy ,,docker"
* Istnieje możliwośc komunikacji po TCP: Domyślnie komunikacja nie jest szyfrowana oraz nie posiada uwierzytelniania

#### Komunikacja z Docker Engine po HTTP
1. Dodajemy w pliku /etc/docker/daemon.json wpis:
```json
"hosts":["unix:///var/run/docker.sock", "tcp://0.0.0.0:2375"]
```

2. Debian/Ubuntu należy stworzyć plik /etc/systemd/system/socker.service.d/docker.conf
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd
```

3. Uruchamiamy polecenie: sudo systemctl daemon-reload
4. Korzystamy z Dockera po HTTP: docker -H tcp://0.0.0.0:2375 ps

```bash
cat /etc/docker/daemon.json
sudo nano /etc/docker/daemon.json
# dodanie wpisu "hosts":["unix:///var/run/docker.sock", "tcp://0.0.0.0:2375"]
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/docker.conf
#[Service]
#ExecStart=
#ExecStart=/usr/bin/dockerd
cat /etc/systemd/system/docker.service.d/docker.conf
sudo systemctl daemon-reload
sudo systemctl restart docker

sudo docker ps
docker -H tcp://0.0.0.0:2375 ps

sudo docker image pull nginx:latest
curl -X POST -H "Content-Type: application/json" \
    -d '{"Image": "nginx:latest", "PortBindings": {"80/tcp" : [{ "HostPort": "8080" }]}}' \
    localhost:2375/v1.40/containers/create?name=create-by-api4
```

### 10.5 Logowanie
```bash
docker info --format '{{.LoggingDriver}}'
docker container run --name redis-json redis
cd /var/lib/docker/containers
ls -lah
cd ./3b812d71f61e0ddb210b3c5bc5732cbf9bbf6d726ef02a3d57e736979afb2db2
ls -lah
cat 3b812d71f61e0ddb210b3c5bc5732cbf9bbf6d726ef02a3d57e736979afb2db2-json.log
cd /

nano /etc/docker/daemon.json
# dodanie wpisu "log-driver": "local"
sudo systemctl restart docker
docker info --format '{{.LoggingDriver}}'
docker container run --name redis-local redis
cd /var/lib/docker/containers
ls -lah
cd ./f1d2df27951bd4d2c20958b94dafac3b95d0687e050bf3ab594fcc417d1da789
ls -lah
cd local-logs
ls -lah
cat container.log
cd /

# nano /etc/docker/daemon.json
# zmiana sterownika na journald 
# "log-driver": "local"
# lub
docker container run --name redis-journald --log-driver=journald redis
docker container logs redis-journald
journalctl -xe | grep edis

journalctl -fu docker.service #logi całego Docker Engine
journalctl -u docker.service #logi całego Docker Engine
```