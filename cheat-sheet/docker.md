# Git

#### Everyday tasks

fetch latest image
```shell
docker compose pull
```

start, restart all services defined in docker-compose.yaml in background
```shell
docker compose up -d
```

for a specific container
```shell
docker compose up -d immich
```

start, restart all services defined in docker-compose.yaml in foreground
```shell
docker compose up 
```


stop running containers and remove stopped containers and networks
```shell
docker compose down
```

same but removes volumes too.
```shell
docker compose down -v
```


restart previously stopped containers
```shell
docker compose start
```

restart all stopped and running containers
```shell
docker compose restart
```

stop running containers but will not remove them
```shell
docker compose stop
```


remove unsused images
```shell
docker image prune -f
```

show container CPU [usage](https://docs.docker.com/reference/cli/docker/container/stats/)  
```shell
docker stats
docker cointainer stats
```


https://docs.docker.com/compose/faq/#whats-the-difference-between-up-run-and-start