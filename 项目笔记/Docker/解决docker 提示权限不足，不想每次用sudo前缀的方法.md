可以不用执行，默认是安装完docker后，是有docker用户组的

```
sudo groupadd docker
```

根据自己的用户名加上权限

```
sudo gpasswd -a [username] docker
```

重启docker服务

```
sudo service docker restart
```

退出终端，重新进入，就可以直接使用docker 命令了