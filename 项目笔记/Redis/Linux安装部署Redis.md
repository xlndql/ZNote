下载Redis

进入官网找到下载地址 [https://redis.io/download](https://redis.io/download)

右键Download按钮，选择复制链接。

进入到Xshell控制台(默认当前是root根目录)，输入wget 将上面复制的下载链接粘贴上，如下命令:

```
wget [复制下载链接]
```

 解压

下载完成后需要将压缩文件解压，输入以下命令解压到当前目录

```
tar -zvxf [压缩包名]
```

移动redis目录

一般都会将redis目录放置到 /usr/local/redis目录，所以这里输入下面命令将目前在/root目录下的redis-5.0.7文件夹更改目录，同时更改文件夹名称为redis。

```
mv /root/[解压后文件夹名称] /usr/local/redis
```

编译

cd到/usr/local/redis目录，输入命令make执行编译命令，接下来控制台会输出各种编译过程中输出的内容。

```
make
```

安装

输入以下命令

```
make PREFIX=/usr/local/redis install
```

启动redis

根据上面的操作已经将redis安装完成了。在目录/usr/local/redis 输入下面命令启动redis

```
./bin/redis-server ./redis.conf
```

配置远程连接且始终运行

进入配置文件

```
vim /usr/local/redis/redis.conf
```

设置以下属性

```
#bind 注释掉bind 
daemonize yes 
protected-mode no
```

查看Redis是否正在运行

```
ps -aux | grep redis
```

重启Redis

```
kill -9 [进程号]
```

进入Redis

```
./redis-cli
```