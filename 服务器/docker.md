## 卸载系统之前的doker 并安装新的docker

```
#卸载系统之前的docker 
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
                  
                  
sudo yum install -y yum-utils

# 配置镜像
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
    
sudo yum install docker-ce docker-ce-cli containerd.io

sudo systemctl start docker
# 设置开机自启动
sudo systemctl enable docker

docker -v
sudo docker images

# 配置镜像加速
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://chqac97z.mirror.aliyuncs.com"]
}
EOF


sudo systemctl daemon-reload
sudo systemctl restart docker
```

## mysql部署

```
sudo docker pull mysql:5.7



#centos
# --name指定容器名字 -v目录挂载 -p指定端口映射  -e设置mysql参数 -d后台运行
sudo docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7
	
#ubuntu	
sudo docker run --name mysql-container -v /mydata/mysql/conf:/etc/mysql/conf.  d -v /mydata/mysql/data:/var/lib/mysql -v /mydata/mysql/logs:/var/log/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7	

ubuntu配置my.cnf
	
```

```
# 进入已启动的容器
docker exec -it mysql bin/bash
# 退出进入的容器
exit;

因为有目录映射，所以我们可以直接在镜像外执行
vi /mydata/mysql/conf/my.conf 

[client]
default-character-set=utf8
[mysql]
default-character-set=utf8
[mysqld]
init_connect='SET collation_connection = utf8_unicode_ci'
init_connect='SET NAMES utf8'
character-set-server=utf8
collation-server=utf8_unicode_ci
skip-character-set-client-handshake
skip-name-resolve

保存(注意评论区该配置不对，不是collection而是collation)

docker restart mysql

```

## redis部署

拉取镜像

```
docker pull redis
```

创建配置文件

```
mkdir -p /mydata/redis/conf
touch /mydata/redis/conf/redis.conf
```

创建容器

```bash
docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf
```

启动容器

```bash
docker exec -it redis redis-cli
```









## 基础命令

|                             操作                             |                          描述                          |
| :----------------------------------------------------------: | :----------------------------------------------------: |
|                    docker search [镜像名]                    |                        查找镜像                        |
|                 docker pull [镜像名]:[版本]                  |                拉取镜像(默认为最新版本)                |
|                        docker images                         |                  查看已拉取的镜像列表                  |
|                     docker rmi [镜像id]                      |                     根据id删除镜像                     |
|        docker run -id --name=[容器名] [镜像名]:[版本]        |                  创建容器并在后台运行                  |
|        docker run -it --name=[容器名] [镜像名]:[版本]        |        创建容器并在容器中运行命令(不在后台运行)        |
|                docker start [容器名或容器id]                 |                        启动容器                        |
|                 docker stop [容器名或容器id]                 |                        关闭容器                        |
|          docker exec -it [容器名或容器id] /bin/bash          |                 在运行的容器中运行命令                 |
|                 docker rm  [容器名或容器id]                  |                   删除停止运行的容器                   |
|                docker inspect[容器名或容器id]                |                返回docker对象的底层信息                |
| docker run -it --name=[容器名] -v [宿主机数据目录]:[容器目录] [镜像名]:[版本] /bin/bash | 创建一个容器并将其指定目录与宿主机进行绑定从而数据共享 |







