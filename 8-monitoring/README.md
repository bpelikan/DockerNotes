# 8. Monitoring

### 8.1 Wstęp do monitoringu
```bash
docker stats

#
docker container run -d --name apache1 httpd
docker container run -d --name apache2 httpd
docker container run -d --name redis1 redis
docker container run -d --name redis2 redis
docker container ls
docker container stats
docker container stats --no-stream
```

### 8.2 Limitowanie zasobów poszczególnym kontenerom
```bash
docker run -d -p 6370:6379 --memory="600M" --cpus="0.6" --name redis redis

#
docker container run -d -p 8081:80 --memory="256M" --cpus="0.6" nginx
docker container run  --memory="50M" --rm busybox free -m
docker run --memory 50m --rm -it progrium/stress --vm 1 --vm-bytes 62914560 --timeout 3s
docker container run -it --cpus=".5" ubuntu bash
```