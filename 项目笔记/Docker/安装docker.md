菜鸟教程：[https://www.runoob.com/docker/centos-docker-install.html](https://www.runoob.com/docker/centos-docker-install.html)

使用官方安装脚本自动安装

```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

或者

```
curl -sSL https://get.daocloud.io/docker | sh
```

手动安装

1. 卸载旧版本依赖

```
yum remove docker \                   docker-client \                   docker-client-latest \                   docker-common \                   docker-latest \                   docker-latest-logrotate \                   docker-logrotate \                   docker-engine
```

2. 设置仓库

安装所需的软件包。yum-utils 提供了 yum-config-manager ，并且 device mapper 存储驱动程序需要 device-mapper-persistent-data 和 lvm2。

sudo yum install -y yum-utils \  device-mapper-persistent-data \  lvm2

使用以下命令来设置稳定的仓库。阿里云仓库

sudo yum-config-manager \    --add-repo \    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

3. 安装最新版本的 Docker Engine-Community 和 containerd

sudo yum install docker-ce docker-ce-cli containerd.io

启动 Docker

systemctl start docker 或 service docker start

5. 验证是否安装成功

docker version

Docker 需要用户具有 sudo 权限，为了避免每次命令都输入sudo，可以把用户加入 Docker 用户组（官方文档）。

sudo usermod -aG docker $USER

docker images：查看镜像文件

卸载docker

sudo yum remove docker-ce docker-ce-cli containerd.io

sudo rm -rf /var/lib/docker

开机自启

systemctl enable docker

阿里云镜像加速

sudo mkdir -p /etc/docker sudo tee /etc/docker/daemon.json <<-'EOF' { "registry-mirrors": ["https://3n4m4jry.mirror.aliyuncs.com"] } EOF sudo systemctl daemon-reload sudo systemctl restart docker