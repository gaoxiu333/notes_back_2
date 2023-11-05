
`镜像短 ID`、`镜像长 ID`、`镜像名`、`镜像摘要`  ？？
## 使用镜像

Docker 运行容器前需要本地存在对应的镜像，如果本地不存在该镜像，Docker 会从镜像仓库拉取该镜像；

- 获取镜像
- 使用镜像
> 镜像分为获取和使用，因为国内网络的原因，获取镜像需要学会使用国内源，使用镜像就更重要了。

### 获取镜像

```bash
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
# 相当于
docker pull pull docker.io:80/library/ubuntu:18.04
```

- `<域名/IP>[:端口号]` - 默认 Docker Hub(`docker.io`)
- `仓库名` -  仓库名为两段式，即`<用户名>/<软件名>` 用户名默认为`Library`

```bash
# 从 Docker Hub 获取官方镜像 library/unbuntu 仓库中标签为 18.4 的镜像
docker pull ubuntu:18.04
```

### 查看镜像

```bash
docker image ls --help
# 查看顶层镜像
docker image ls
# 查看 docker 占用内存情况
docker system　df
```

#### 虚悬镜像

一种特殊镜像，镜像既没有仓库名，也没有标签，均为`none`；是由于发布的新镜像名字取代了旧的镜像，旧的镜像变成了`none`。

删除虚悬镜像

```bash
docker image prune
```

#### 中间层镜像

```bash
docker image ls -a
```

#### 查看特定镜像

```bash
# 查看镜像名字包含 ubuntu 的所有镜像
docker image ls ubuntu
```

#### 格式化

```bash
# 列出顶层镜像，并且只包含镜像ID和仓库名
docker image ls --format "{{.ID}}: {{.Repository}}"
```


#### 删除镜像

```bash
docker image rm --help
```

- `<IMAGE>` - 可以是`镜像短 ID`、`镜像长 ID`、`镜像名`、`镜像摘要`
	- `镜像短 ID` - 一般取三个字符以上，用于区分
	- `镜像名` - `<仓库名>:<标签>`
> 注意：rm 不仅可以删除镜像，也有可能是取消标签的命令，在执行删除时要注意甄别。

```bash
# 删除仓库名为 redis 的镜像
docker image rm $(docker image ls -q redis)
# 删除 mongo:3.2 之前的镜像
docker image rm $(docker image ls -q -f before=mongo:3.2)
docker exec -it webserver bash
```
### 制作镜像

docker commit - 简单理解为保存容器当前状态的快照

将容器的存储层保存下来成为镜像，换句话说就是在原有镜像的基础上，再叠加上容器的存储层，并构成新的镜像，新的镜像会拥有容器最后的文件变化。

```bash
docker commit [选项] <容器ID或容器名> [<仓库名>[:<标签>]]
```

#### Dockerfile

Dockerfile 是一个文件，包含了制定镜像的命令

```bash
# 指定基础镜像
FROM nginx
# 执行命令行命令
RUN echo "<h1>Hello World</h1>" > /usr/share/nginx/html/index.html
```

> 注意：每一个docker命令都将是一层镜像，所以尽量将多条docker命令合并成一个命令

#### Dockerfile 最佳实践

示例：编译、安装 redis 可执行文件

```bash
FROM debian:stretch

RUN buildDeps='gcc libc6-dev make wget' \
    && apt-get update \
    && apt-get install -y $buildDeps \
    && wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz" \
    && mkdir -p /usr/src/redis \
    && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
    && make -C /usr/src/redis \
    && make -C /usr/src/redis install \
    && rm -rf /var/lib/apt/lists/* \
    && rm redis.tar.gz \
    && rm -r /usr/src/redis \
    && apt-get purge -y --auto-remove $buildDeps```

常规操作解释：
- 行尾添加 `\` 的命令换行方式
- 删除编译构建所需要的软件
- 清理所有下载、展开的文件
- 清理 `apt` 缓存文件
#### 空白镜像

如果不希望以任何镜像为基础构建镜像那么可以使用`scratch`

```bash
FROM scratch
```

#### 参考
- [`Dockerfile` 官方文档](https://docs.docker.com/engine/reference/builder/)
- [`Dockerfile` 最佳实践文档](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [`Docker` 官方镜像 `Dockerfile`](https://github.com/docker-library/docs)

#### 构建镜像

```bash
docker build --help
docker build [选项] <上下文路径/URL/->
# 构建镜像命为 nginx:v3 的镜像 . 为当前目录
docker build -t nginx:v3 .
# 直接用 git repo
docker build https://github.com/twang2218/gitlab-ce-zh.git#:11.1
# 指定镜像文件
docker build -f Dockerfile -t containerName .
```

TODO: build 还有很多其他用法
## 操作容器

### 启动容器

新建并启动

```bash
docker run --help
# 后台运行一个容器
docker run -d <IMAGE>
# 查看容器日志
docker logs <container-id>
# 进入容器，并打开一个交互式终端
docker exec -it <container-id> /bin/bash
```

启动已终止的容器

```bash
docker start <container-id>
```

### 终止容器

```bash
docker stop <container>
```
### 进入容器

```bash
docker attach
# 常用
docker exec -it
```


### 导入导出容器

导出

```bash
# 将正在运行的容器导出为一个tar存档文件
docker export --help
# 将docker镜像打包为一个tar
docker save --help
# 示例
docker save -o my_image.tar my_image:tag
```

导入

```bash
docker import --help
docker load --help
# 示例
docker load -i my_image.tar
```
> docker import 和 docker load 的区别：前者是导入一个容器快照，快照文件将丢弃所有的历史记录和元数据信息（即仅保存容器当时的快照状态）

### 删除容器

```bash
docker container rm --help
docker container rm <container>
# 删除所有停止的容器
docker container prune
```

## 数据管理

docker 容器中有可写层，但是容器不再运行时，数据会随着容器的终止而结束。

将数据挂载在 docker 之外，有三种挂载方式
- Volumes - 存储在 Docker Host 文件系统的一个路径下，只能通过docker进行修改
- Bind mounts - 任何 进程都可以修改
- Tmpfs - 只存在docker中，不能持久存储


## 使用网络

## Dockerfile

```bash
FROM
RUN
COYP # 复制文件
ADD # 更高级的复制文件
CMD # 容器启动命令
ENTRYPOINT #入口点
ENV #设置环境变量
ARG # 构建参数
VOLUME # 定义匿名卷
EXPOSE # 暴露端口
WORKDIR # 指定工作目录
USER # 指定当前用户
HEALTHCHECK # 健康检查
ONBUILD # ...

```

## Docker Compose

定义和运行多个 Docker 容器的应用，前身是开源项目 Fig

`Compose` 两个重要的概念：
- 服务(service)：一个应用的容器，实际上可以包括若干运行相同镜像的容器实例；
- 项目(project)：由一组关联的应用容器组成的一个完整业务单元，在 docker-compose.yml 文件中定义。

### 安装

通过 `pip` 安装

```bash
pip install -U docker-compose
```

模版

```bash
# docker-compose.yml

version: "3"

services:
  webapp:
    image: examples/web
    ports:
      - "80:80"
    volumes:
      - "/data"```
## 私有仓库

## TODO

实战：
- node 开发环境
- python 多版本开发环境
- web 服务器 最佳
	- 增加https支持
