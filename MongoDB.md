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

## 配置
### 配置文件
```
/etc/mongod.conf
```

### 为数据目录创建软连接
```
ln -s /var/lib/mongo /home/data/mongo
```

## 安全
MongoDB安装完成后，默认是不需要输入用户名密码即可登录的，
但是往往数据库方面我们会出于安全性的考虑而设置用户名密码，
以下内容介绍MongoDB添加管理员/普通用户的方法。

注：   
MongoDB是没有默认管理员账号，所以要先添加管理员账号，再开启权限认证。   
切换到admin数据库，添加的账号才是管理员账号。   
用户只能在用户所在数据库登录，包括管理员账号。   
管理员可以管理所有数据库，但是不能直接管理其他数据库，要先在admin数据库认证后才可以。

### 创建超级用户
执行
```
./mongo
> use admin
> db.createUser(
  user: "root",
  pwd: "root",   
  roles: [ { role: "root", db: "admin" } ]   
)
```
添加成功时显示：
```
Successfully added user: {
    "user" : "root",
    "roles" : [
        {
            "role" : "root",
            "db" : "admin"
        }
    ]
}
```
执行以下命令看看结果：
```
> show users
```

### 开启权限验证
在/etc/mongod.conf中添加：
```
security:
    authorization: enabled
```
重启mongodb服务，执行
```
systemctl restart mongod
```

验证权限是否生效：
```
./mongo
MongoDB shell version v3.4.4
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.4
> use admin
switched to db admin
> db.auth('root', 'root')
1
> show dbs
admin  0.000GB
local  0.000GB
```

### 创建普通用户
```
> use test
> db.createUser(
... {
... user:"test1",
... pwd: "test1",
... roles: [{ role: "dbOwner", db: "test"}]
... }
... )
Successfully added user: {
        "user" : "test1",
        "roles" : [
                {
                        "role" : "dbOwner",
                        "db" : "test"
                }
        ]
}
> exit
bye

./mongo
MongoDB shell version v3.4.4
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.4

> use test
switched to db test
> db.auth('test1','test1')
1
```

### MongoDB内置角色
自行百度
