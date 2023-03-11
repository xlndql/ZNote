1、安装依赖和相关库：

```
[root@localhost ~]# yum -y install gcc-c++ zlib-devel openssl-devel libtool
```

2、下载nginx安装包并解压：

```
[root@localhost ~]# cd /usr/local
[root@localhost local]# wget http://nginx.org/download/nginx-1.14.0.tar.gz
[root@localhost local]# tar -zxvf nginx-1.14.0.tar.gz
```

3、配置和安装

```
[root@localhost local]# cd nginx-1.14.0
[root@localhost nginx-1.14.0]# ./configure --prefix=/usr/local/nginx
[root@localhost nginx-1.14.0]# make && make install
```

4、启动nginx：

```
[root@localhost nginx-1.14.0]# cd ../nginx/sbin
[root@localhost sbin]# ./nginx
```

5、查看nginx:

```
[root@localhost nginx]# ps -ef | grep nginx
root      13850      1  0 17:01 ?        00:00:00 nginx: master process ./nginx
nobody    13851  13850  0 17:01 ?        00:00:00 nginx: worker process
root      13879   1128  0 17:11 pts/0    00:00:00 grep --color=auto nginx
```

6、停止和重启nginx:

```
./nginx -s reload   #重启
./nginx -s stop #关闭
```