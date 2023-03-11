列举镜像

```
docker images // 列举镜像
```

安装java

搜索镜像

```
docker search jdk
```
![[Pasted image 20230311181531.png]]
![0](https://note.youdao.com/yws/res/38/884AF489363F47AAA8B87F707EB14C16)

下载镜像：

```
docker pull docker.io/lwieske/java-8
```

查看镜像：

```
docker images
```

启动镜像：

```
docker run -it --name jdk1.8 -d java:latest /bin/bash
```

查看容器：

```
docker ps
```

查看所有容器：

```
docker ps -l
```

停止容器：

```
docker stop [容器id]
```

启动容器：

```
docker start [容器id]
```

删除容器：

```
docker rm [容器id]
```

删除镜像：

```
docker rmi [镜像id] docker rmi [镜像名称]:[tag]
```

进入容器：

```
docker attach [容器id]
```

Mysql

安装mysql

```
docker pull mysql:8.0
```

启动mysql

```
docker run -p 3308:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:8.0 

// 若存在mysql重名情况则需要先删除容器 docker ps -a //查看容器 
docker rm [镜像id] // 删除容器
```

快捷运行

```
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:8.0
```

参数解释：

-   --name 容器名字
-   -p 3308:3306 物理机端口：容器内部端口
-   -e 运行参数 初始化 root 用户的密码
-   -d 后台运行 mysq5.7 镜像名字加标签

-v 目录挂载，
-v /mydata/mysql/log:/var/log/mysql 表示将 docker里面mysql容器的/var/log/mysql目录挂载到宿主linux系统的 /mydata/mysql/log 目录下，方便查看。

然后修改权限：

```
// 进入mysql容器： 
docker exec -it 934e3c005153 /bin/bash // 登录mysql： 
mysql -uroot -proot 
// 修改权限： 
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root'; 
或者：
ALTER USER 'root'@'%' IDENTIFIED BY '123456'; flush privileges;
```

mysql配置文件: vim /mydata/mysql/conf/my.cnf

``` js
[client] 
default-character-set=utf8 
[mysql] 
default-character-set=utf8 
[mysqld] 
init_connect='SET collation_ connection = utf8_ unicode_ci' 
init_connect='SET NAMES utf8' 
character-set-server=utf8 
collation-server=utf8_unicode_ci 
skip-character-set-client-handshake 
skip-name-resolve
```

安装Oracle

```
# 安装oracle https://hub.docker.com/r/oracleinanutshell/oracle-xe-11g 
docker pull oracleinanutshell/oracle-xe-11g 

# 运行镜像 
-p: 是容器内部端口绑定到指定的主机端口 docker run --name oracle -d -p 1521:1521 -e ORACLE_ALLOW_REMOTE=true oracleinanutshell/oracle-xe-11g

# 进入容器 
docker exec -it 容器id /bin/bash 

# 连接 oracle 
su oracle 
cd $ORACLE_HOME 
bin/sqlplus / as sysdba 

# 创建账号 
create user qingxi identified by 123456;
grant connect,resource to qingxi; 

# 修改密码 
alter user 用户名 identified by 新密码; 

# 删除用户 
drop user 用户名;
```

安装Postgresql

```
# 拉取镜像 
docker pull postgres 

# 启动镜像 
docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=pass123 postgres 

# 进入容器 docker exec -it 容器id /bin/bash 

# 连接pg 
psql -U postgres -h 127.0.0.1 -p 5432
```

安装redis

```
docker pull redis
```

启动

```
// 创建配置文件 
mkdir -p /mydata/redis/conf 
touch /mydata/redis/conf/redis.conf
```

```
docker run -p 6379:6379 --name redis \ 
-v /mydata/redis/data:/data \ 
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \ 
-d redis redis-server/etc/redis/redis.conf
```

redis-cli控制台:

```
docker exec -it redis redis-cli
```

redis开启持久化，修改配置文件redis.conf，启动aof持久化，输入：

```
appendonly yes
```

docker启动mysqsl、redis自动启动：

docker update mysql --restart=always docker update redis --restart=always