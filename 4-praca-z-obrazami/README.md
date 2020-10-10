# 4. Praca z obrazami

### 4.1 Docker Hub i repozytoria
```bash
docker image pull alpine:3.7
docker image ls
docker image pull alpine:3.9
```

### 4.2 Tagowanie i publikowanie obrazów na Docker Hub
```bash
docker image pull alpine:3.9
docker image tag alpine:3.9 bpelikan/alpine:3.9
docker image ls
docker login
docker image push bpelikan/alpine:3.9
docker image rm bpelikan/alpine:3.9
docker image pull bpelikan/alpine:3.9
docker container run --name myalpine1 bpelikan/alpine:3.9
docker container run --name myalpine2 -it bpelikan/alpine:3.9 sh
  exit
docker images ls
docker image pull alpine:3.7
docker image tag alpine:3.7 bpelikan/alpine:3.7
docker image push bpelikan/alpine:3.7
```
