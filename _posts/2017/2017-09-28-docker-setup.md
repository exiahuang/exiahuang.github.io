---
categories:
- Docker
date: 2017-09-28 08:02:34
description: Docker Setup
layout: post
tags:
- Docker
title: Docker Setup
update_date: 2020/05/23 23:56:51

---

# Docker的安装和卸载


# Docker的version
```
hellodocker>docker version
Client:
 Version:      17.06.2-ce
 API version:  1.30
 Go version:   go1.8.3
 Git commit:   cec0b72
 Built:        Tue Sep  5 19:57:19 2017
 OS/Arch:      windows/amd64

Server:
 Version:      17.06.2-ce
 API version:  1.30 (minimum version 1.12)
 Go version:   go1.8.3
 Git commit:   cec0b72
 Built:        Tue Sep  5 19:59:19 2017
 OS/Arch:      linux/amd64
 Experimental: true
```

# Docker中关于镜像的基本操作
```
[root@xxx ~]# docker search centos    # 查看centos镜像是否存在
[root@xxx ~]# docker pull centos    # 利用pull命令获取镜像
Using default tag: latest
latest: Pulling from library/centos
08d48e6f1cff: Pull complete
Digest: sha256:b2f9d1c0ff5f87a4743104d099a3d561002ac500db1b9bfa02a783a46e0d366c
Status: Downloaded newer image for centos:latest

[root@xxx ~]# docker images    # 查看当前系统中的images信息
REPOSITORY      TAG            IMAGE ID       CREATED        SIZE
centos          latest         0584b3d2cf6d   9 days ago     196.5 MB
```

# Docker中关于镜像的基本操作利用镜像启动一个容器后进行修改 ==> 利用commit提交更新后的副本
```
[root@xxx ~]# docker run -it centos:latest /bin/bash    # 启动一个容器
[root@72f1a8a0e394 /]#    # 这里命令行形式变了，表示已经进入了一个新环境
[root@72f1a8a0e394 /]# git --version    # 此时的容器中没有git
bash: git: command not found
[root@72f1a8a0e394 /]# yum install git    # 利用yum安装git
......
[root@72f1a8a0e394 /]# git --version   # 此时的容器中已经装有git了
git version 1.8.3.1
```

此时利用exit退出该容器，然后查看docker中运行的程序（容器）：
```
[root@xxx ~]# docker ps -a
CONTAINER ID  IMAGE    COMMAND      CREATED   STATUS   PORTS    NAMES
72f1a8a0e394  centos:latest "/bin/bash"  9 minutes ago   Exited (0) 3 minutes ago      angry_hodgkin
```

这里将容器转化为一个镜像，即执行commit操作，完成后可使用docker images查看：
```
[root@xxx ~]# docker commit -m "centos with git" -a "qixianhu" 72f1a8a0e394 xianhu/centos:git

[root@xxx ~]# docker images
REPOSITORY       TAG    IMAGE ID         CREATED             SIZE
xianhu/centos    git    52166e4475ed     5 seconds ago       358.1 MB
centos           latest 0584b3d2cf6d     9 days ago          196.5 MB
```

其中，-m指定说明信息；-a指定用户信息；72f1a8a0e394代表容器的id；xianhu/centos:git指定目标镜像的用户名、仓库名和 tag 信息。注意这里的用户名xianhu，后边会用到。

此时Docker引擎中就有了我们新建的镜像xianhu/centos:git，此镜像和原有的CentOS镜像区别在于多了个Git工具。此时我们利用新镜像创建的容器，本身就自带git了。

```
[root@xxx ~]# docker run -it xianhu/centos:git /bin/bash
[root@520afc596c51 /]# git --version
git version 1.8.3.1
```

利用exit退出容器。注意此时Docker引擎中就有了两个容器，可使用docker ps -a查看。

# 利用Dockerfile创建镜像
Dockerfile可以理解为一种配置文件，用来告诉docker build命令应该执行哪些操作。一个简易的Dockerfile文件如下所示，
```
# 说明该镜像以哪个镜像为基础
FROM centos:latest

# 构建者的基本信息
MAINTAINER xianhu

# 在build这个镜像时执行的操作
RUN yum update
RUN yum install -y git

# 拷贝本地文件到镜像中
COPY ./* /usr/share/gitdir/
```

有了Dockerfile之后，就可以利用build命令构建镜像了：
```
[root@xxx ~]# docker build -t="xianhu/centos:gitdir" .
```

构建完成之后，同样可以使用docker images命令查看：

```
[root@xxx ~]# docker images
REPOSITORY        TAG       IMAGE ID      CREATED            SIZE
xianhu/centos     gitdir    0749ecbca587  34 minutes ago     359.7 MB
xianhu/centos     git       52166e4475ed  About an hour ago  358.1 MB
centos            latest    0584b3d2cf6d  9 days ago         196.5 MB
```

# 删除容器或者镜像
以上就是构建自己镜像的两种方法。其中也涉及到了容器的一些操作。如果想删除容器或者镜像，可以使用rm命令，注意：删除镜像前必须先删除以此镜像为基础的容器。
```
[root@xxx ~]# docker rm container_name/container_id
[root@xxx ~]# docker rmi image_name/image_id
```

# 基本命令
启动、停止、重启容器命令：
```
[root@xxx ~]# docker start container_name/container_id
[root@xxx ~]# docker stop container_name/container_id
[root@xxx ~]# docker restart container_name/container_id
```

后台启动一个容器后，如果想进入到这个容器，可以使用attach命令：
```
[root@xxx ~]# docker attach container_name/container_id
```

删除容器的命令前边已经提到过了：
```
[root@xxx ~]# docker rm container_name/container_id
```

用exec进入容器：
```
docker exec -it 6858df85647a /bin/bash
```


指定端口：
```
docker run --name=nginx -d -v ~/nginxlogs:/var/log/nginx -p 5000:80 nginx
```

绑定卷：
```
docker run --name xjava -v .:/work -it java:8 /bin/bash
docker run -d -P --name xjava2 -v .:/work -it java:8 /bin/bash
```

# Dockerfile构建Python开发环境，框架Django, bottle, Flask

## Dockerfile
```
# OSはCentOS
FROM centos:latest

# 各パッケージをインストール
# pipやvirtualenvインストールも想定しています。
RUN yum -y update
RUN yum -y groupinstall "Development Tools"
RUN yum -y install \ 
           kernel-devel \
           kernel-headers \
           gcc-c++ \
           patch \
           libyaml-devel \
           libffi-devel \
           autoconf \
           automake \
           make \
           libtool \
           bison \
           tk-devel \
           zip \
           wget \
           tar \
           gcc \
           zlib \
           zlib-devel \
           bzip2 \
           bzip2-devel \
           readline \
           readline-devel \
           sqlite \
           sqlite-devel \
           openssl \
           openssl-devel \
           git \
           gdbm-devel \
           python-devel 

# Python3.5.2をインストール
# Python3.5.2をダウンロード
WORKDIR /root
RUN wget https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tgz
RUN tar xzvf Python-3.5.2.tgz

# makeでインストール
WORKDIR ./Python-3.5.2
RUN ./configure --with-threads
RUN make install

# pipインストール(最新版)
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py

# readlineインストール
RUN pip install readline

# virtualenvインストール
RUN pip install virtualenv

# Djangoインストール
RUN pip install django

# おまけ
# Django以外のフレームワークインストール
# bottleインストール
# RUN pip install bottle

# Flaskインストール
# RUN pip install Flask

WORKDIR /root
CMD ["/bin/bash"]
```

## Centos镜像生成
```
$ docker build -t {任意のイメージ名} .
# 例
$ docker build -t exia/pycentos .
```

## 制作容器
作成したPython入りのCentOSイメージからコンテナ作成
```
$ docker run -it --name {任意のコンテナ名} {作成したイメージ名} /bin/bash
# 例
$ docker run -it --name exia/pycentos_c exia/pycentos /bin/bash
```

## pyenvインストール
pyenvをクローン
```
# git clone https://github.com/yyuu/pyenv.git /root/.pyenv
```

bash_profileに環境変数を記述するためにviを起動
```
# vi /etc/skel/.bash_profile
```

.bash_profile
```
# pyenv
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

bash_profileを反映。
```
# source /etc/skel/.bash_profile
```

設定を確認
```
# pyenv version
system (set by /root/.pyenv/version)
```

Pythonのリスト
```
# pyenv install --list
Available versions:
  2.1.3
  2.2.3
  2.3.7
...
  3.5.1
  3.5.2
  3.6.0a1
  3.6.0a3
  3.6-dev
...
```