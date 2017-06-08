# MongoDB

## 安装
### 环境
CentOS Linux release 7.3.1611 (Core)   
MongoDB 3.4.4   

### 手动创建repo文件
```
vim /etc/yum.repos.d/mongodb-org-3.4.repo
```
在文本编辑器中输入如下配置：
```
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

### 使用yum安装mongodb
执行
```
yum install -y mongodb-org
```

## 启动和关闭
```
systemctl start mongod
systemctl status mongod
systemctl stop mongod
```

