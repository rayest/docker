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

