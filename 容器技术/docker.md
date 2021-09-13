
* [docker](#docker)
    * [Docker简介](#docker简介)
        * [是什么](#是什么)
        * [能干嘛](#能干嘛)
    * [Docker常用命令](#docker常用命令)
        * [帮助命令](#帮助命令)
        * [镜像命令](#镜像命令)
        * [容器命令](#容器命令)


# docker
## Docker简介
### 是什么
解决了运行环境和配置问题软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术。
### 能干嘛
容器虚拟化技术

一次构建、随处运行
- 更快速的应用交付和部署
- 更便捷的升级和扩缩容
- 更简单的系统运维
- 更高效的计算资源利用
## Docker常用命令
### 帮助命令
- docker version
- docker info
- docker --help
### 镜像命令
- docker images 列出本地主机上的镜像
  - OPTIONS说明：
    - -a :列出本地所有的镜像（含中间映像层）
    - -q :只显示镜像ID。
    - --digests :显示镜像的摘要信息
    - --no-trunc :显示完整的镜像信息
- docker search 某个XXX镜像名字
  - 网站 https://hub.docker.com
  - 命令 docker search [OPTIONS] 镜像名字
    - OPTIONS说明：
      - --no-trunc : 显示完整的镜像描述
      - -s : 列出收藏数不小于指定值的镜像。
      - --automated : 只列出 automated build类型的镜像；
- docker pull 某个XXX镜像名字 下载镜像
  - docker pull 镜像名字[:TAG]
- docker rmi 某个XXX镜像名字ID 删除镜像
  - 删除单个 docker rmi  -f 镜像ID
  - 删除多个 docker rmi -f 镜像名1:TAG 镜像名2:TAG
  - 删除全部 docker rmi -f $(docker images -qa)
### 容器命令
有镜像才能创建容器，这是根本前提(下载一个CentOS镜像演示)
- docker pull centos

新建并启动容器
- docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

列出当前所有正在运行的容器
- docker ps [OPTIONS]

退出容器
- exit 容器停止退出
- ctrl+P+Q 容器不停止退出

启动容器
- docker start 容器ID或者容器名

重启容器
- docker restart 容器ID或者容器名

停止容器
- docker stop 容器ID或者容器名

强制停止容器
- docker kill 容器ID或者容器名

删除已停止的容器
- docker rm 容器ID

一次性删除多个容器
- docker rm -f $(docker ps -a -q)
- docker ps -a -q | xargs docker rm

重要

启动守护式容器
- docker run -d 容器名 

查看容器日志
- docker logs -f -t --tail 容器ID
  -  -t 是加入时间戳
  -  -f 跟随最新的日志打印
  -  --tail 数字 显示最后多少条

查看容器内运行的进程
- docker top 容器ID

查看容器内部细节
- docker inspect 容器ID

进入正在运行的容器并以命令行交互
- docker exec -it 容器ID bashShell
- 重新进入docker attach 容器ID
- 上述两个区别
  - attach 直接进入容器启动命令的终端，不会启动新的进程
  - exec 是在容器中打开新的终端，并且可以启动新的进程

从容器内拷贝文件到主机上
- docker cp  容器ID:容器内路径 目的主机路径