
**不同领域的主流操作系统**

* 桌面操作系统
  * Windows（用户数量最多）
  * Mac OS（操作体验好，办公人士首选）
  * Linux（用户数量少）
* 服务器操作系统
  * UNIX（安全、稳定、付费）
  * Linux（安全、稳定、免费、占有率高）
  * Windows Server（付费、占有率低）
* 移动设备操作系统
  * Android（基于 Linux、开源，主要用于智能手机、平板电脑和智能电视）
  * iOS（苹果公式开发、不开源，用于苹果公司的产品，例如：iPhone、iPad）
* 嵌入式操作系统
  * Linux（机顶盒、路由器、交换机）

**Linux 系统历史**

* 时间：1991年
* 地点：芬兰赫尔基辛大学
* 人物：Linus Torvalds（21岁）
* 语言：C语言、汇编语言
* logo：企鹅
* 特点：免费、开源、多用户、多任务

**Linux 系统版本**

Linux 系统分为**内核版**和**发行版**

* 内核版
  * 由 Linus Torvalds 及其团队开发、维护
  * 免费、开源
  * 负责控制硬件
* 发行版
  * 基于 Linux 内核版进行扩展
  * 由各个 Linux 厂商开发、维护
  * 有收费版本和免费版本

**Linux 系统版本 - 发行版**

Linux 系统发行版：

* Ubuntu：以桌面应用为主
* RedHat：应用最广泛、收费
* CentOS：RedHat 的社区版、免费
* openSUSE：对个人完全免费、图形界面华丽
* Fedora：功能完备、快速更新、免费
* 红旗 Linux：北京中科红旗软件技术有限公司开发



![[1673426786692.png]]

## 目录

* 系统安装
* 使用 SSH 连接工具
* 目录结构
  * Linux 和 Windows 目录结构对比
  * Linux 目录介绍
* 环境变量
* 文件管理
* 用户管理
* 内存管理
* 磁盘管理
* 进程管理
* 网络管理
* 软件包管理
* 服务管理
* 日志管理
* Linux 内核
* 常用命令
  * 基础常用命令
  * 命令使用技巧
  * 文件目录操作命令
    * ls
    * cd
    * cat
    * more
    * tail
    * mkdir
    * rmdir
    * rm
  * 拷贝移动命令
    * cp
    * mv
  * 打包压缩命令
    * tar
  * 文本编辑命令
    * vi/vim
    * vim
  * 查找命令
    * find
    * grep
* 防火墙命令
* 常用环境搭建
  * 软件安装方式
  * yum 安装
  * 安装 jdk
  * 安装 Tomcat
  * 安装 MySQL
  * 安装 lrzsz
* Shell 脚本编程

---

## 系统安装

1. 安装 VMWare
2. 下载 Linux 的镜像（CentOS 或 Ubuntu）
3. 在 VMWare中配置新虚拟机
4. 安装镜像

## 使用 SSH 连接工具

SSH（Secure Shell），建立在应用层基础上的安全协议

常用的 SSH 连接工具

* putty
* secureCRT
* xshell
* finalshell

通过 SSH 连接工具就可以实现从本地连接到远程的 Linux 服务器

## 目录结构

### Linux 和 Windows 目录结构对比

Linux 系统中的目录

* /是所有目录的顶点
* 目录结构像一颗倒挂的树

![[1673451882588.png]]

### Linux 目录介绍

![[1673451947945.png]]

* bin 存放二进制可执行文件
* boot 存放系统引导时使用的各种文件
* dev 存放设备文件
* etc 存放系统配置文件
* home 存放系统用户文件
* lib 存放程序运行所需要的共享库和内核模块
* opt 存放额外安装的可选应用程序包
* root 超级用户目录
* sbin 存放二进制可执行文件，只有 root 用户才能访问
* tmp 存放临时文件
* usr 存放系统应用程序
* var 存放运行时需要改变数据的文件，例如日志文件

## 常用命令

### 基础常用命令

| 序号 | 命令           | 对应英文             | 作用                     |
| ---- | -------------- | -------------------- | ------------------------ |
| 1    | ls             | list                 | 查看当前目录下的内容     |
| 2    | pwd            | print work directory | 查看当前所在目录         |
| 3    | cd [目录名]    | change directory     | 切换目录                 |
| 4    | touch [文件名] | touch                | 如果文件不存在，新建文件 |
| 5    | mkdir [目录名] | make directory       | 创建目录                 |
| 6    | rm [文件名]    | remove               | 删除指定文件             |

如果产生中文乱码情况，需要更改 Linux 的编码：

```powershell
echo 'LANG="en_US.UTF-8"' >> /etc/profile # 修改为英文
echo 'LANG="zh_CN.UTF-8"' >> /etc/profile # 修改为中文

source /etc/profile
```

### 命令使用技巧

* Tab键自动补全
* 连续两次 Tab 键，给出操作提示
* 使用上下箭头快速调出曾经使用过的命令
* 使用 clear 或者 Ctrl + l 快捷键实现清屏

### Linux 命令格式

command [-options] [parameter]

说明

* command：命令名
* [-options]：选项，可以对命令进行控制，也可以省略
* [parameter]：传给命令的参数，可以是零个、一个或多个

### 文件目录操作命令

#### ls

作用：显示指定目录下的内容

语法：ls [ -a、-l、-al] [dir]

说明：

* **-a** 显示所有文件及目录（.开头的隐藏文件也会列出）
* **-l** 除文件名称外，同时将文件形态（d表示目录，-表示文件）、权限、拥有者、文件大小等信息详细列出
* **-al** 表示 -a 和 -l

注意：

由于我们使用 ls 命令时经常需要加入 -l 选项，所以 Linux 为 ls -l 命令提供了一种简写方式，即 ll

#### cd

作用：用于切换当前工作目录，即进入指定目录

语法：cd [dirName]

特殊说明：

* ~ 表示用户的 home 目录
* . 表示目前所在目录
* .. 表示目前目录位置的上级目录

举例：

* cd ..			切换当前目录的上级目录
* cd ~			切换到用户的 home 目录
* cd /usr/local	切换到 /usr/local 目录

#### cat

作用：用于显示文件内容

语法：cat [-n] fileName

说明：

* -n：由 1 开始对所有输出的行数编号

举例：

* cat/etc/profile		查看 /etc 目录下的 profile 文件内容

#### more

作用：以分页的形式显示文件内容

语法：more fileName

操作说明：

* 回车键			向下滚动一行
* 空格键			向下滚动一屏
* b				返回上一屏
* q 或者 Ctrl + C		退出 more

举例：

more /etc/profile		以分页形式 /etc 目录下的 profile 文件内容

#### tail

作用：查看文件末尾的内容

语法：tail [-f] fileName

说明：

* -f：动态读取文件末尾内容并显示，通常用于日志文件的内容输出

举例：

tail /etc/profile		显示 /etc 目录下的 profile 文件末尾 10 行的内容

tail -20 /etc/profile		显示 /etc 目录下的 profile 文件末尾 20 行的内容

tail -f /xxx/xxx.log		动态读取 /xxx 目录下的 xxx.log 文件末尾内容并显示

#### mkdir

作用：创建目录

语法：mkdir [-p] dirName

说明：

* -p：确保目录名称存在，不存在就创建一个。通过此选项，可以实现多层目录同时创建

举例：

* mkdir xxx 在当前目录下，建立一个名为 xxx 的子目录
* mkdir -p xx/xxx 在工作目录的 xx 下建立一个 xxx 目录，如果不存在，则新建一个 xx 目录

#### rmdir

作用：删除空目录

语法：rmdir [-p] dirName

说明：

* -p：当子目录被删除后使父目录为空目录的话，则一并删除

举例：

* rmdir xxx 删除名为 xxx 的空目录
* rmdir -p xx/xxx 删除 xx 目录中的名为 xxx 的子目录，若删除完 xx 目录为空目录的话，也一并删除
* rmdir xx* 删除名称以 xx 开头的空目录

#### rm

作用：删除文件或者目录

语法：rm [-rf] name

说明：

* -r：将目录及目录中所有文件（目录）逐一删除，即递归删除
* -f：无需确认，直接删除

举例：

* rm -r xxx 删除名为 xxx 的目录和目录中的所有文件，删除前需要确认
* rm -rf xxx 无需确认，直接删除名为 xxx 的目录和目录中的所有文件
* rm -f xxx.txt 无需确认，直接删除 xxx.txt 文件

### 拷贝移动命令

#### cp

作用：用于复制文件或目录

语法：cp [-r] source dest

说明：

* -r：如果复制的是目录需要使用此选项，此时将复制该目录下的所有子目录和文件

举例：

* cp xxx.txt xxx/		将 xxx.txt 复制到 xxx 目录下
* cp xxx.txt /xx.txt	将 xxx.txt 复制到当前目录下并改名为 xx.txt
* cp -r xxx/ ./xx/		将 xxx 目录和目录下的所有文件复制到 xx 目录下
* cp -r xxx/* ./xx/	将 xxx 目录下的所有文件复制到 xx 目录下

#### mv

作用：为文件或目录改名，或将文件或目录移动到其它位置

语法：mv source dest

举例：

* mv xxx.txt xx.txt	将 xxx.txt 更改为 xx.txt
* mv xxx.txt xx/		将 xxx.txt 移动到 xx/ 目录下
* mv xxx.txt xx/xx.txt	将 xxx.txt 移动到 xx/ 目录下并改名为 xx.txt
* mv xxx/ xx/		将 xxx 目录移动到 xx 目录下，如果 xx 目录不存在，则将 xxx 目录名称更改为 xx

### 打包压缩命令

#### tar

作用：对文件进行打包、解包、压缩、解压

语法：tar [-zcxvf] fileName [files]

包文件后缀为 .tar 表示只是完成了打包，并没有压缩

包文件后缀为 .tar.gz 表示打包的同时还进行了压缩

说明：

* -z：z 代表的是 gzip，通过 gzip 命令处理文件，gzip 可以对文件压缩或者解压
* -c：c 代表的是 create，即创建新的包文件
* -x：x 代表的是 extract，实现从包文件中还原文件
* -v：v 代表的是 verbose，显示命令的执行过程
* -f：f 代表的是 file，用于指定包文件的名称

举例：

打包

* tar -cvf xxx.tar ./*		将当前目录下的所有文件打包，打包后的文件名为 xxx.tar
* tar -zcvf xxx.tar.gz ./*	将当前目录下的所有文件打包并压缩，打包后的文件名为 xxx.tar.gz

解包：

* tar -xvf xxx.tar					将 xxx.tar 文件解包并放在当前目录
* tar -zxvf xxx.tar.gz				将 xxx.tar.gz 文件解压并放在当前目录
* tar -zxvf xxx.tar.gz -C /usr/local	将 xxx.tar.gz 文件解压并放在 /usr/local 目录

### 文本编辑命令

#### vi/vim

作用：vi 命令是 Linux 系统提供的一个文本编辑工具，可以对文件内容进行编辑，类似于 Windows 的笔记本

语法：vi fileName

说明：

* vim 是从 vi 发展而来的一个功能更加强大的文本编辑工具，在编辑文件时可以对文本内容进行着色，方便我们对文件进行编辑处理
* 要使用 vim 命令，需要自行安装：

```powershell
  yum install vim
```

#### vim

作用：对文件内容进行编辑，vim 其实就是一个文本编辑器

语法：vim fileName

说明：

* 在使用 vim 编辑文件的时候，如果指定的文件存在，则直接打开文件，如果不存在则新建文件。
* vim 在进行文本编辑的时候共分为三个模式，分别是命令模式（Command mode）、插入模式（Insert mode）和底行模式（Last line mode）。这三种模式可以相互切换。

1. 命令模式：
   * 命令模式下可以查看文件内容、移动光标（上下左右箭头、gg 光标移动到开头、G 光标移动到结尾）
   * 通过 vim 命令打开文件后，默认进入命令模式
   * 另外两种模式需要首先进入命令模式才能进入
2. 插入模式
   * 插入模式下可以对文件内容进行编辑
   * 在命令模式下按下[i，a，o] 任意一个，可以进入插入模式。进入插入模式后，下方会出现 [insert] 字样
   * 在插入模式下按下 ESC，回到命令模式
3. 底行模式
   * 底行模式下可以通过命令对文件内容进行查找、显示行号、退出等操作
   * 在命令模式下按下 [:，/] 任意一个，可以进入底行模式
   * 通过 / 方式进入底行模式后，可以对文件内容进行查找
   * 通过 : 方式进入底行模式后，可以输入 wq（保存并退出）、q!（不保存退出）、set nu（显示行号）

### 查找命令

#### find

作用：在指定目录下查找文件

语法：find dirName -option fileName

举例：

* find . -name "*.java"	在当前目录及其子目录下查找 .java 结尾的文件
* find /xxx -name "*.java"	在 /xxx 目录及其子目录下查找 .java 结尾的文件

#### grep

作用：从指定文件中查找指定的文本内容

语法：grep word fileName

举例：

* grep xxx xxxx.java	查找 HelloWord.java 文件中出现 Hello 字符串的位置
* grep xxx *.java		查找当前目录中所有以 .java 结尾的文件中包含 hello 字符串的位置

## 防火墙命令

**防火墙操作：**

* 查看防火墙状态	systemctl status firewalld、firewall-cmd-state
* 暂时关闭防火墙	systemctl stop firewalld
* 永久关闭防火墙	systemctl disable firewalld
* 开启防火墙		systemctl start firewalld
* 开放指定端口		firewall-cmd --zone=public --add-port=8080/tcp --permanent
* 关闭指定端口		firewall-cmd --zone=public --remove-port=8080/tcp --permanent
* 立即生效			firewall-cmd --reload
* 查看开放的端口	firewall-cmd --zone=public --list-ports



注意：

1. systemctl 是管理 Linux 中服务的命令，可以对服务进行启动、停止、重启、查看状态等操作。
2. firewall-cmd 是 Linux 中专门用于控制防火墙的命令
3. 为了保证系统安全，服务器的防火墙不建议关闭


## 常用环境安装

### 软件安装方式

* 二进制发布包安装
  * 软件已经针对具体平台编译打包发布，只要解压修改配置即可。
* rpm 安装
  * 软件已经按照 redhat 的包管理规范进行打包，使用 rmp 命令进行安装，不能自行解决库依赖问题
* yum 安装
  * 一种在线软件安装方式，本质上还是 rpm 安装，自动下载安装包并安装，安装过程中自动解决库依赖问题
* 源码编译安装
  * 软件以源码工程的形式发布，需要自己编译打包


### yum 安装

来自 [yum更换国内镜像源_依赖](https://blog.csdn.net/qq_45887180/article/details/115796389)

**查看 yum 源信息：**

* yum repolist


**更换国内镜像源：**

```powershell
cd /etc/yum.repos.d				# 定位到 base repo 源位置
mv CentOS-Base.reop CentOS-Base.repo.bak	# 备份旧的配置文件
wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo	# 下载阿里源的文件
yum clean all		# 清理缓存
yum makecache		# 重新生成缓存
yum repolist		# 查看 yum 源信息
```


**yum 常用命令**

```powershell
yum常用命令
删除软件：yum remove AAA-x.x.x.rpm或者yum erase foo-x.x.x.rpm
升级软件：yum upgrade AAA或者yum update AAA
查询信息：yum info AAA
搜索软件（以包含foo字段为例）：yum search AAA
显示软件包依赖关系：yum deplist AAA
 
　　 -q 静默执行 
　　 -t 忽略错误
　　-R[分钟] 设置等待时间
　　-y 自动应答yes
　　--skip-broken 忽略依赖问题
　　--nogpgcheck 忽略GPG验证
 
　　check-update 检查可更新的包
　　clean all    清除全部[缓存]
　　clean packages 清除临时包文件（/var/cache/yum 下文件）
　　clean headers  清除rpm头文件
　　clean oldheaders 清除旧的rpm头文件
　　deplist 列出包的依赖
　　list 可安装和可更新的RPM包
　　list installed 已安装的包
　　list extras 已安装且不在资源库的包
　　info 可安装和可更新的RPM包 信息
　　info installed 已安装包的信息(-qa 参数相似)
　　install[RPM包] 安装包
　　localinstall 安装本地的 RPM包
　　update[RPM包] 更新包
　　upgrade 升级系统
　　search[关键词] 搜索包
　　provides[关键词] 搜索特定包文件名
　　reinstall[RPM包] 重新安装包
　　repolist 显示资源库的配置
　　resolvedep 指定依赖
　　remove[RPM包] 卸载包
    makecache  生成缓存

```


### 安装 jdk

操作步骤：

1. 使用 xshell 自带的上传工具将 jdk 的二进制发布包上传到 Linux
2. 解压安装包 tar -zxvf [文件名] -C /usr/local
3. 配置环境变量，使用 vim 命令修改 /etc/profile 文件，在文件末尾加入如下配置
   * JAVA_HOME=/usr/local/[jdk文件夹名称]
   * PATH=$JAVA_HOME/bin:\$PATH
4. 重新加载 profile 文件，使更改的配置立即生效，命令为 source /etc/profile
5. 检查安装是否成功，命令为 java -version


### 安装 Tomcat

**操作步骤：**

1. 使用 xshell 自带的上传工具将 Tomcat 的二进制发布包上传到 Linux
2. 解压安装包 tar -zxvf [文件名] -C /usr/local
3. 进入 Tomcat 的 bin 目录启动服务，命令为 sh startup.sh 或者 ./startup.sh


**验证 Tomcat 是否启动成功**

* 查看启动日志
  * more /usr/local/[Tomcat 目录名称]/logs/catalina.out
  * tail -50 /usr/local/[Tomcat 目录名称]/logs/catalina.out
* 查看进程
  * ps -ef | grep tomcat

注意：

* ps命令是 Linux 下非常强大的进程查看命令，通过 ps -ef 可以查看当前运行的所有进程的详细信息
* "|" 在 Linux 中称为管道符，可以将前一个命令的输出结果给后一个命令作为输入
* 使用 ps 命令查看进程时，经常配合管道符和查找命令 grep 一起使用来查看特定进程


**停止 Tomcat 服务的方式：**

* 运行 Tomcat 的 bin 目录中提供的停止服务的脚本文件
  * sh shutdown.sh
  * ./shutdown.sh
* 结束 Tomcat 进程
  * 先查看 Tomcat 进程获取 id
  * 输入命令 kill -9 [进程 id]

注意：

* kill 是 Linux 提供的用于结束进程的命令，-9 表示强制结束


### 安装 MySQL

**检测当前系统是否安装了 MySQL：**

* rpm -qa				查询当前系统中安装的所有软件
* rpm -qa | grep mysql	查询当前系统中安装的名称带 mysql 的软件
* rpm -qa | grep mariadb	查询当前系统中安装的名称带 mariadb 的软件

RMP（Red-Hat Package Manager）RPM 软件包管理器，是红帽 Linux 用于管理和安装软件的工具

注意：

* 如果当前系统已经安装了 MySQL 数据库，安装会失败
* CentOS 7 中自带的 mariadb 与 MySQL 数据库冲突


**卸载已安装的冲突软件软件：**

* rpm -e --nodeps 软件名称


**安装 MySQL：**

* mkdir /usr/local/mysql
* tar -zxvf [压缩包名称] -C /usr/local/mysql


按照顺序安装 rpm 软件包：

* 说明1：安装过程中提示缺少 net-tools 依赖，使用 yum 安装
* 说明2：可以通过指令升级现有软件及系统内核 yum update


**使用 yum 安装 MySQL**
