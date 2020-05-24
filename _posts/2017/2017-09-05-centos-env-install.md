---
categories:
- Linux
date: 2017-09-05 08:01:34
description: Centos Env Install
layout: post
tags:
- Linux
title: Centos Env Install
update_date: 2020/05/23 23:56:51

---

# python
## Centos7でのpython入れ替えメモ
```
# cat /etc/redhat-release
CentOS Linux release 7.3.1611 (Core)

# yum install -y https://centos7.iuscommunity.org/ius-release.rpm
# yum search python36
# yum install -y python36u python36u-libs python36u-devel python36u-pip

シンボリックリンク張り替え
# ls -l /bin/py*
# ln -s /bin/python3.6 /bin/python3
# unlink /bin/python
# ln -s /bin/python3.6 /bin/python
# vim $(which pip)
1行目  #!/usr/bin/python2   →　#!/usr/bin/python
# pip --version
pip 9.0.1 from /usr/lib/python3.6/site-packages (python 3.6)

```

# node
##

# redis

# mongodb

# ant 1.10 install
```shell
wget http://www.apache.org/dist/ant/binaries/apache-ant-1.10.1-bin.tar.gz
tar zxvf apache-ant-1.10.1-bin.tar.gz
mv apache-ant-1.10.1 /usr/share/ant
ln -s /usr/share/ant/bin/ant /usr/bin/ant
vi ~/.bash_profile
```

bash_profile
```
~/.bash_profile
export ANT_HOME=/usr/share/ant
```