# 10. Docker Advanced

### 10.2 Konfiguracja Docker Engine

Konfiguracja:
* Linux: /etc/docker/daemon.json
* Windows: Settings -> Docker Engine
* MacOS: Preferences -> Daemon -> Advanced

### 10.3 Komunikacja z Docker Daemon po HTTP

* Domyślnie komunikacja Docker Daemona z DockerCLI odbywa się przez Unix Sockets (/var/run/docker.sock) i wymaga uprawnień dla grupy ,,docker"
* Istnieje możliwośc komunikacji po TCP: Domyślnie komunikacja nie jest szyfrowana oraz nie posiada uwierzytelniania

