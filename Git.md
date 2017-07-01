# Git

## 安装
### 环境
CentOS Linux release 7.3.1611 (Core)
git version 1.8.3.1

### 安装
使用yum安装
```
yum install git
```

安装成功后，执行如下指令，如果正常显示git版本，说明安装成功
```
git --version
```

## 配置SSH
执行指令：
```
ssh-keygen -t rsa -C "214461193@qq.com"
```
输出如下：
```
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
```
括号中为默认路径和文件，直接回车即可。
之后会要求输入并确认密码：
```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
正确输入密码后输出如下：
```
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
4b:32:eb:21:97:da:0f:5b:47:a4:14:6d:9f:57:b4:e0 214461193@qq.com
The key's randomart image is:
+--[ RSA 2048]----+
|        ..   . ..|
|         .o . . o|
|        .... E o |
|       . o  o .  |
|      o S .  .   |
|       * o       |
|    . * o .      |
|     * = .       |
|    . +..        |
+-----------------+
```
此时ssh配置完成，/root/.ssh路径下可以看到生成的公钥和私钥

## 在github中配置公钥
执行命令：
```
cat ~/.ssh/id_rsa.pub
```
登陆github账号，复制公钥到用户设置相应位置。配置完成后即可在linux服务器上克隆git项目了。

## 指令
```
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:ShadowWatcher/WatcherLinux
git push -u origin master

git mv -f Mysql.md MySQL.md
git add -u MySQL.md
git commit -m "rename Mysql.md"

git rm -rf database/
```
