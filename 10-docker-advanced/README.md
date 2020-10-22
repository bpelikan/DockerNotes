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
