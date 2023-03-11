[Redis的安装和配置说明 - 简书 (jianshu.com)](https://www.jianshu.com/p/e90317668ae2)

---

# 1. 在Linux系统上安装Redis

首先想到的安装方法是使用 apt-get install redis-server命令来安装Redis，不过在《Redis实战》中并不推荐这么做。

因为根据Debian或者Ubuntu版本的不同，这种安装方法有可能会让读者安装到旧版本的Redis。

故而可以选择直接使用源码来编译并安装Redis。

首先要确保系统具有make、gcc等一系列构建工具。

安装过程如下：

（1）从[http://redis.io/download](https://links.jianshu.com/go?to=http%3A%2F%2Fredis.io%2Fdownload)下载最新的stable版本的Redis源码。

（2）使用tar命令解压源代码。

（3）使用make命令来编译、安装。

此外，官方也给出了Linux系统下的安装教程（[https://redis.io/download](https://links.jianshu.com/go?to=https%3A%2F%2Fredis.io%2Fdownload)）

2. 在Windows系统上安装Redis

虽然在Windows系统上Redis的功能稍稍受限，但是由于本人并不太能驾驭Linux系统，所以暂时还以Windows为主。。。

1.  Redis官网并没有提供Windows的下载，不过我们可以使用微软官方的移植版本（[https://github.com/MicrosoftArchive/redis/releases](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FMicrosoftArchive%2Fredis%2Freleases)）。

![0](https://note.youdao.com/yws/res/2/WEBRESOURCE29f763ee533a6f9c22b47f51b9dd67e2)

这里我们可以选择自己所需的版本zip或msi下载

1.  下载解压后，可得如下目录结构：

![0](https://note.youdao.com/yws/res/d/WEBRESOURCE67a0e8b0fa56faa2ea270cddcea05f9d)

1.  这里双击Redis服务器即可启动Redis

![0](https://note.youdao.com/yws/res/e/WEBRESOURCEddb10421b4821ad0395377bb85c2393e)

Redis-Server

1.  Server启动之后，我们就可以双击标注为Redis客户端的文件来操作Redis数据库了。

![0](https://note.youdao.com/yws/res/0/WEBRESOURCEcd777de3a5460d55fc2ad8f7318533b0)

Redis客户端

到此，基本操作就完成了，就可以通过命令行来访问Redis了。不过我们也可以看一下Redis 的配置文件，以便对Redis的配置有进一步了解。

3. Redis的配置文件

我们在安装目录下找到redis.windows-service.conf这个文件，使用文本编辑器打开。

![0](https://note.youdao.com/yws/res/1/WEBRESOURCEa178696cff33b09f7dae81d74e531ce1)

Redis配置文件

这里对Redis数据库的配置进行了详细说明，部分配置选项如下：

daemonize：是否以后台进程运行，默认为no。Windows下不支持修改 。Linux平台下可以改为yes，这样就不用为了启动Redis而单独保留一个shell窗口。

pidfile：如以后台进程运行，则需指定一个pid，默认为/var/run/redis.pid。Windows下不支持修改。

bind：绑定主机IP，默认值为127.0.0.1（注释）

protected-mode：以保护模式运行，默认yes

port： 监听端口，默认为6379

timeout： 超时时间，默认为300（秒）

loglevel： 日志记录等级，有4个可选值，debug，verbose（默认值），notice，warning

logfile： 日志记录方式，默认值为stdout

databases： 可用数据库数，默认值为16，默认数据库为0

save ： 指出在多长时间内，有多少次更新操作，就将数据同步到数据文件。这个可以多个条件配合，比如默认配置文件中的设置，就设置了三个条件。

save 900 1 900秒（15分钟）内至少有1个key被改变

save 300 10 300秒（5分钟）内至少有10个key被改变

save 60 10000 60秒内至少有10000个key被改变

rdbcompression： 存储至本地数据库时是否压缩数据，默认为yes

dbfilename： 本地数据库文件名，默认值为dump.rdb

dir： 本地数据库存放路径，默认值为 ./

slaveof： 当本机为从服务时，设置主服务的IP及端口（注释）

masterauth： 当本机为从服务时，设置主服务的连接密码（注释）

requirepass 连接密码（注释）

maxclients： 最大客户端连接数，默认不限制（注释）

maxmemory ： 设置最大内存，达到最大内存设置后，Redis会先尝试清除已到期或即将到期的Key，当此方法处理后，任到达最大内存设置，将无法再进行写入操作。（注释）

appendonly： 是否在每次更新操作后进行日志记录，如果不开启，可能会在断电时导致一段时间内的数据丢失。因为redis本身同步数据文件是按上面save条件来同步的，所以有的数据会在一段时间内只存在于内存中。默认值为no

appendfilename： 更新日志文件名，默认值为appendonly.aof（注释）

appendfsync： 更新日志条件，共有3个可选值。no表示等操作系统进行数据缓存同步到磁盘，always表示每次更新操作后手动调用fsync()将数据写到磁盘，everysec表示每秒同步一次（默认值）。

vm-enabled： 是否使用虚拟内存，默认值为no

vm-swap-file： 虚拟内存文件路径，默认值为/tmp/redis.swap，不可多个Redis实例共享

vm-max-memory： 将所有大于vm-max-memory的数据存入虚拟内存,无论vm-max-memory设置多小,所有索引数据都是内存存储的(Redis的索引数据就是keys),也就是说,当vm-max-memory设置为0的时候,其实是所有value都存在于磁盘。默认值为0。