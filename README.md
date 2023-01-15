### 安装
```
官网
如果有旧的docker版本，需要先卸载旧的版本，在安装新的版本
```

### 开启docker服务
```shell
systemctl start docker
```

### 判断docker是否启动成功/查看docker版本
```shell
docker version
```

### 测试docker
```shell
docker run hello-world
```

### 镜像相关
```shell
# 查询本地的镜像
docker images

# 删除本地的镜像(单个)
docker rmi -f <image-id|image-name>

# 删除本地所有的镜像(多个)
docker rmi -f $(docker images -aq)

# 搜索DockerHub中的镜像
docker search <image-name>

# 从DockerHub中下载镜像
docker pull <image-name>:<version>
```

### 容器相关
```shell
# 新建一个容器并运行
docker run [可选参数] <image-name|image-id>

# 可选参数说明

# 容器的名称
--name=<name>

# 后台的方式运行，linux会自动停止没有前台的
-d

# 使用交互方式运行，进入容器查看内容
-it

# 手动指定端口运行
-p 主机端口:容器内部端口

# 随机指定端口运行
-P

# 卷挂载
-v

# 环境配置
-e

# 进入容器
/bin/bash

# 推出容器
exit



# 所有正在运行的容器
docker ps

# 查看曾经运行的容器
docker ps -a

# 删除单个容器(不能删除正在运行的容器)
docker rm <容器ID>

# 删除全部容器
docker rm -f $(docker ps -aq)

# 启动停止掉的容器
docker start 容器ID

# 重启容器
docker restart 容器ID

# 停止容器
docker stop 容器ID

# 强制停止容器
docker kill 容器ID

# 查看日志
docker logs -f -t --tail 日志数量 容器ID

# 查看容器的元数据
docker inspect 容器ID

# 进入当前正在运行的容器(打开一个新的命令窗口)
docker exec -it 容器ID /bin/bash

# 进入当前正在运行的容器(打开第一次运行的命令窗口)
docker attach 容器ID

# 容器内拷贝文件拷贝到外部
docker cp 容器ID:容器内路径 目前的主机路径

# 查看容器运行的内存
docker stats
```


### 镜像技术
```shell
# 将容器为一个新的镜像
docker commit -m="描述信息"  容器ID 新镜像名称:版本号
```


### 数据卷技术
```shell
# 查看所有卷
docker volume ls

# 主从同步
--volumes-from
```

### Dockerfile
```
FROM centos
VOLUME ["volume01"，"volume02"]
CMD echo "----end----"
CMD /bin/bash



FROM                 #基础镜像
LABEL                #镜像是谁写的，作者是谁
RUN                  #镜像构建的时候需要运行的命令
ADD                  #添加内容
WORKDIR              #镜像的工作目录
VOLUME               #挂载卷
EXPOSE               #暴露端口
CMD                  #容器启动后要运行的命令，只有最后一个会生效
ENTRYPOINT           #容器启动后要运行的命令，追加
COPY                 #将文件拷贝到镜像中
ENV                  #环境变量
```



### 案例
```
docker run -d -it --name nginx01 -v /home/nginx01:/home -p 3355:80 /bin/bash
```