下载安装包

首先去官网下载jdk安装包，后缀为-linux-x64.tar.gz

解压

```shell
tar -zxvf jdk-verson-linux-x64.tar.gz
```

移动

```shell
mv jdk /usr/local/
```

修改配置文件

```shell
vim /etc/profile
```

添加配置

```shell
export JAVA_HOME=/usr/local/jdk1.8 export CLASSPATH=$:CLASSPATH:$JAVA_HOME/lib/ export PATH=$PATH:$JAVA_HOME/bin
```

刷新配置

```shell
source /etc/profile
```