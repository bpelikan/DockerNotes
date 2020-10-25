# 11. Bezpieczeństwo

### 11.3 Least privileged - czyli jak pozbyć się roota z kontenera
```bash
docker run -itd --name ubuntu-defaultuser ubuntu /bin/bash
docker container top ubuntu-defaultuser #PID: 5169
ps -aux | grep bash
# root      5169  0.0  0.0   4112  3388 pts/0    Ss+  14:34   0:00 /bin/bash

cd ../home/bartoszpelikan/
touch /home/bartoszpelikan/most-wanted-file
ls
docker run -itd --name ubuntu-defaultuser1 -v /:/hacking ubuntu /bin/bash
docker exec -it ubuntu-defaultuser1 bash
    ls -l
    cd hacking 
    ls
    rm ./home/bartoszpelikan/most-wanted-file
    exit

docker run -itd --user 998 --name ubuntu-customuser -v /:/hacking ubuntu /bin/bash
docker container top ubuntu-customuser #PID: 5596
ps -aux | grep bash
# 998       5596  0.1  0.0   4112  3184 pts/0    Ss+  14:40   0:00 /bin/bash
docker exec -it ubuntu-customuser bash
    cd hacking/home/bartoszpelikan/
    touch test-file # odmowa dostępu
    exit
```