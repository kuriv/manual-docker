# Compose

Docker Compose 是用来一次编排、启动多个容器的工具。编辑 `compose.yaml` 文件内容如下。

```yaml
services:
  redis-master:
    image: redis:latest
    container_name: redis-master
    ports:
      - "6379:6379"
    environment:
      - DEMO_VARIABLE=233
    volumes:
      - redis-master-vol:/data
    networks:
      redis-net:
    restart: unless-stopped
    cpus: '1'
    mem_limit: 512M
    command: redis-server --appendonly yes

  redis-slave:
    image: redis:latest
    container_name: redis-slave
    ports:
      - "6380:6379"
    environment:
      - DEMO_VARIABLE=666
    volumes:
      - redis-slave-vol:/data
    networks:
      redis-net:
    restart: unless-stopped
    cpus: '0.5'
    mem_limit: 256M
    command: redis-server --replicaof redis-master 6379

volumes:
  redis-master-vol:
  redis-slave-vol:

networks:
  redis-net:
```

执行下面的命令，查看 Docker Compose 管理的容器状态。

```
docker compose ps -a
```

执行下面的命令，使用 Docker Compose 后台启动所有容器。

```
docker compose up -d
```

执行下面的命令，使用 Docker Compose 停止并删除所有的容器、网络以及数据卷。

```
docker compose down -v
```

执行下面的命令，使用 Docker Compose 启动指定的容器。

```
docker compose start redis-master redis-slave
```

执行下面的命令，使用 Docker Compose 停止指定的容器。

```
docker compose stop redis-master redis-slave
```

执行下面的命令，使用 Docker Compose 重新启动所有容器。

```
docker compose restart
```

还可以通过访问 [Docker Compose](https://docs.docker.com/reference/compose-file/) 来查看更多配置字段。
