## 说明 
* Dockerfile 中每一个指令都会建立一层，RUN 也不例外
* 这里没有使用很多个 RUN 对一一对应不同的命令，而是仅仅使用一个 RUN 指令，并使用 && 将各个所需命令串联起来。只有 1 层
## 上下文
* docker build 命令最后有一个 ‘.’, 指定了上下文路径
* 使用 docker build 构建镜像，并非在本地构建，而是在 Docker 的服务端(Docker 也是客户端/服务端模式)即在 Docker 引擎中构建的
* docker build 时，会将路径下的所有内容进行打包，然后上传给 Docker 引擎
* Docker 引擎收到该上下文包之后，展开就会获得构建镜像所需要的一切文件
* 如果需要忽略某些文件进行构建，可以仿照 .gitignore 创建 .dockerignore 将其忽略
