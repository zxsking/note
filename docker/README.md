## Windows

### 安装

安装windows版的docker [docker-desktop](https://www.docker.com/products/docker-desktop/)

可直接在powershell中使用docker命令





### mysql

拉取镜像

```
docker pull mysql5.7         //5.7版本
```

创建容器

```
docker run -p 3306:3306 --privileged=true  --name mysql -v /d/dev/docker/mydata/mysql/log:/var/log/mysql -v /d/dev/docker/mydata/mysql/data:/var/lib/mysql -v /d/dev/docker/mydata/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD="root" -d mysql:5.7
```

