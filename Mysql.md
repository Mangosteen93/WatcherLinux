# Mysql

## 安装
### 环境

### 依赖
MySQL 依赖 libaio，所以先要安装 libaio
`yum search libaio  # 检索相关信息   
yum install libaio # 安装依赖包`   

成功安装，提示如下:   
`[root@bogon /]# yum install libaio   
已加载插件：fastestmirror   
Loading mirror speeds from cached hostfile   
 * base: mirrors.yun-idc.com   
 * extras: mirrors.163.com   
 * updates: mirrors.163.com   
软件包 libaio-0.3.109-12.el7.x86_64 已安装并且是最新版本   
无须任何处理`
