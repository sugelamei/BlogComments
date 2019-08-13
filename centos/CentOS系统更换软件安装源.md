---
title: CentOS系统更换软件安装源
date: 2019-08-13 09:57:06 
tags: Centos
---

第一步：安装wget
 

    yum install -y wget 

第二步：备份你的原镜像文件，以免出错后可以恢复。


    mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup

第三步：下载新的CentOS-Base.repo 到/etc/yum.repos.d/


    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo


第四步：运行yum makecache生成缓存

    yum clean all
    yum makecache

