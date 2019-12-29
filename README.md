# docker 实践
Docker demos

### 网络

```shell
# 自建一个桥接网络，然后创建两个容器并通过该桥接网络连接，测试容器间是否可通信
$ docker pull ubuntu
$ docker network create --driver bridge net-brg
$ docker network ls
$ docker network inspect net-brg
$ docker container run -it --name net-test1 --network=net-brg ubuntu
$ docker container run -it --name net-test2 --network=net-brg ubuntu
$ docker exec -it CONTAINER_ID bash
root@CONTAINER_ID:/# apt-get update && apt-get install iputils-ping
root@CONTAINER_ID:/# ping ANOTHER_CONTAINER_NAME
```

### 数据卷

```shell
# 1. 新建容器 httpd，并把主机上指定文件挂载到容器的指定目录下
$ docker pull httpd
$ docker run -d -it -p 80:80 --name httpd-demo2 -v /Users/lirui/Documents/test/:/usr/local/apache2/htdocs httpd
# 修改主机 index.html 文件内容，访问 http://127.0.0.1/index.html

# 2. 容器分享数据卷给另一个容器
$ docker create -v /data/index.html --name datastore ubuntu
$ docker run --rm -it --volumes-from datastore ubuntu                                        
```

### docker swarm

```shell
# 通过 docker-machine 创建集群
# 在 ~/.docker/machine/cache/ 目录下安装 boot2docker.iso。再如下操作创建 管理节点 和 工作节点
$ docker-machine create --virtualbox-boot2docker-url ~/.docker/machine/cache/boot2docker.iso --engine-registry-mirror https://registry.docker-cn.com ManagerX

$ docker-machine create --virtualbox-boot2docker-url ~/.docker/machine/cache/boot2docker.iso --engine-registry-mirror https://registry.docker-cn.com WorkerA
```

