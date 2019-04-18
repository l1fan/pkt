# Aria2c Dockerfile  

docker compose config
```yml
services:
    aria2c:
        build: https://l1fan.github.io/pkt/aria2/docker/Dockerfile
        image: l1fan/aria2
        restart: always
        ports:
            - "6800:6800"
        volumes:
            - /download/path:/dl
```
