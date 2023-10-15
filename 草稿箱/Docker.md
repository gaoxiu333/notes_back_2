
### 安装

[官方安装文档](https://docs.docker.com/get-docker/)

在 Ubuntu 上安装，可以不需要 Desktop 版本，只安装 Docker Engine 版本就可以。

> 注意：
> 1. 卸载旧版的 docker或者第三方插件，具体参考官网。
> 2. docker 端口会绕过防火墙，如果有配置的话需要额外注意。

### 使用 apt-get 安装

需要先配置 apt 存储库，阿里的服务器好像已经配置过了？具体安装还是需要看[官方安装教程](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)


## 常用命令

```bash
# 启动docker
systemctl start docker
# 停止docker
systemctl stop docker
# 查看docker服务状态
systemctl status docker
# 设置docker开机自启动
systemctl enable docker
# 删除未运行的容器
docker rm `docker ps -aq`
# 删除所有镜像
docker rmi $(docker images -q)
```