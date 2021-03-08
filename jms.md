#### 1  配置 yum 源(使用阿里云的yum仓库,要求云主机必须能够访问网络) 

```shell
[root@jump-server ~]# wget -qO /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo
[root@jump-server ~]# wget -qO /etc/yum.repos.d/epel.repo https://mirrors.aliyun.com/repo/epel-7.repo
[root@jump-server ~]# sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/CentOS-Base.repo
[root@jump-server ~]# sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/epel.repo
[root@jump-server ~]# vim /etc/yum.repos.d/CentOS-Base.repo
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#
#
 
[base]
name=CentOS-$releasever - Base - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
 
#released updates 
[updates]
name=CentOS-$releasever - Updates - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
 
#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
 
#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/centos/$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
 
#contrib - packages by Centos Users
[contrib]
name=CentOS-$releasever - Contrib - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/centos/$releasever/contrib/$basearch/
gpgcheck=1
enabled=0
gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7

[root@jump-server ~]# vim /etc/yum.repos.d/epel.repo 
[epel]
name=Extra Packages for Enterprise Linux 7 - $basearch
baseurl=http://mirrors.aliyun.com/epel/7/$basearch
failovermethod=priority
enabled=1
gpgcheck=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
 
[epel-debuginfo]
name=Extra Packages for Enterprise Linux 7 - $basearch - Debug
baseurl=http://mirrors.aliyun.com/epel/7/$basearch/debug
failovermethod=priority
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
gpgcheck=0
 
[epel-source]
name=Extra Packages for Enterprise Linux 7 - $basearch - Source
baseurl=http://mirrors.aliyun.com/epel/7/SRPMS
failovermethod=priority
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
gpgcheck=0
```

#### 2  下载软件开始安装

```shell
[root@jump-server ~]# curl -LO http://demo.jumpserver.org/download/setuptools.tar.gz
[root@jump-server ~]# tar zxf setuptools.tar.gz
[root@jump-server ~]# cd setuptools/
[root@jump-server setuptools]# cp config_example.conf  config.conf
[root@jump-server setuptools]# ./jmsctl.sh install
[root@jump-server setuptools]# ./jmsctl.sh start
[root@jump-server setuptools]# ./jmsctl.sh status
       __                     _____
      / /_  ______ ___  ____ / ___/___  ______   _____  _____
 __  / / / / / __ `__ \/ __ \\__ \/ _ \/ ___/ | / / _ \/ ___/
/ /_/ / /_/ / / / / / / /_/ /__/ /  __/ /   | |/ /  __/ /
\____/\__,_/_/ /_/ /_/ .___/____/\___/_/    |___/\___/_/
                    /_/

					 Version:  v2.5.3  

MySQL   Check 	........................ [ OK ]
Redis   Check 	........................ [ OK ]
Docke.  Check 	........................ [ OK ]
Nginx   Check 	........................ [ OK ]
Py3     Check 	........................ [ OK ]
Core    Check 	........................ [ OK ]
Koko    Check 	........................ [ OK ]
Guaca.  Check 	........................ [ OK ]
```