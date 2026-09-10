# Dockerfile

Dockerfile 中包含一系列构建指令，是自动化构建 Docker 镜像的蓝图。编辑 `Dockerfile` 文件内容如下。

```dockerfile
FROM redis:latest
WORKDIR /data
ENV DEMO_VARIABLE=233
RUN apt update && apt install iputils-ping -y
EXPOSE 6379
CMD ["redis-server","--appendonly","yes"]
```

执行下面的命令，使用 Dockerfile 构建镜像。

```
docker build -t radis:v1.0.1 .
```

还可以通过访问 [Dockerfile](https://docs.docker.com/reference/dockerfile) 来查看更多构建指令。
