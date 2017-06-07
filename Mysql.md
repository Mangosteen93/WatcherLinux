# Mysql

## 安装
### 环境

### 依赖
MySQL 依赖 libaio，所以先要安装 libaio   
`yum search libaio  # 检索相关信息   
yum install libaio # 安装依赖包`   

### 下载 MySQL Yum Repository
地址为http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm

执行   
`wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm`

### 添加 MySQL Yum Repository
添加 MySQL Yum Repository 到你的系统 repository 列表中，执行   
`yum localinstall mysql-community-release-el7-5.noarch.rpm`

验证下是否添加成功   
`yum repolist enabled | grep "mysql.*-community.*"`   
可以看到下面内:   
```
[root@bogon software]# yum repolist enabled | grep "mysql.*-community.*"   
mysql-connectors-community/x86_64        MySQL Connectors Community           1   
mysql-tools-community/x86_64             MySQL Tools Community                1   
mysql56-community/x86_64                 MySQL 5.6 Community Server          13   
```

选择要启用 MySQL 版本   
查看 MySQL 版本，执行   
`yum repolist all | grep mysql`   
可以看到 5.5， 5.7 版本是默认禁用的，因为现在最新的稳定版是 5.6

可以通过类似下面的语句来启动某些版本   
`yum-config-manager --disable mysql56-community`   
`yum-config-manager --enable mysql57-community-dmr`   
或者通过修改 /etc/yum.repos.d/mysql-community.repo 文件

``\# Enable to use MySQL 5.6   
[mysql56-community]   
name=MySQL 5.6 Community Server   
baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/7/$basearch/   
enabled=1   
gpgcheck=1   
gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql``   
其中 enabled=0 是指禁用，enabled=1 指启用。   
注意： 任何时候，只能启用一个版本。

执行   
`yum repolist enabled | grep mysql`
查看当前的启动的 MySQL 版本   
`[root@bogon software]# yum repolist enabled | grep mysql   
mysql-connectors-community/x86_64        MySQL Connectors Community           14   
mysql-tools-community/x86_64             MySQL Tools Community                17   
mysql56-community/x86_64                 MySQL 5.6 Community Server          139`   
本例，我们启用的是 5.6 版本。
