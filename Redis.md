# Redis

## 安装
### 环境
CentOS Linux release 7.3.1611 (Core)···
Redis 3.2.3-1.el7

### 使用yum安装redis
执行
```
yum install redis
```

## 启动和关闭
```
systemctl start redis.service
systemctl enable redis.service
```

## 配置
### 配置文件
```
/etc/redis.conf
```

### 设置密码
打开redis.conf配置文件，找到requirepass，然后修改如下:  
requirepass yourpassword  
yourpassword就是redis验证密码，设置密码以后发现可以登陆，但是无法执行命令了。

命令如下:  
```
redis-cli -h yourIp -p yourPort //启动redis客户端，并连接服务器
keys *                          //输出服务器中的所有key
```
报错如下:  
```
(error) NOAUTH Authentication required.
```
这时候你可以用授权命令进行授权，就不报错了  
命令如下:  
```
auth youpassword
```
另外，在连接服务器的时候就可以指定登录密码，避免单独输入上面授权命令  
命令如下:  
```
redis-cli -h yourIp -p yourPort  -a youPassword
```

###配置IP
在redis.conf文件中把# bind 127.0.0.1前面的#去掉， 用要配置的IP替换127.0.0.1

### 为数据目录创建软连接
```
ln -s /var/lib/redis /home/data/redis
```
