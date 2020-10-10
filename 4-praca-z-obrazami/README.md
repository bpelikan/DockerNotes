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

### 4.4 Dockerfile
```dockerfile
FROM alpine:3.9

COPY text.txt .

CMD ["cat", "text.txt"]
```

```bash
cd 4.4
ls -l
docker image build -t myalpine . 
docker container run --name alpine1 myalpine:latest
```

### 4.5 Rozszerzenie oficjalnych obrazów
```bash
cd 4.5
docker container run -d --name nginx11 nginx:latest
docker container cp nginx11:/usr/share/nginx/html/index.html index.html
ls
docker image build -t mynginx:latest .
docker container run -d --name mynginx11 mynginx:latest
docker container run --name mynginx12 -d -p 8081:80 mynginx:latest 
curl http://localhost:8081/
```