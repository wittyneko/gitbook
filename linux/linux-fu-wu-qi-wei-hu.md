# Linux 服务器维护

## 常用软件

```bash
# 安装/卸载apache2
sudo apt-get install apache2
sudo apt-get --purge remove apache2
sudo apt-get autoremote
sudo rm -rf /var/www

# 安装/卸载nginx
sudo apt-get install nginx
sudo apt-get remove nginx
sudo apt-get autoremote
rm -rf /etc/nginx

# SSH客户端与服务器端的文件交互
sudo apt-get install lrzsz

# postgreSQL
sudo apt-get install libpq-dev python-dev
sudo apt-get install postgresql postgresql-contrib
```

## SSH远程访问

```bash
# 安装
apt-get install openssh-server
# 重启ssh
service ssh restart
/etc/init.d/sshd restart
/etc/init.d/ssh restart
# 编辑配置
vi /etc/ssh/sshd_config
```
/etc/ssh/sshd_config
```
# 允许root账号登入
PermitRootLogin yes
# 修改ssh端口 开启端口22和50000
Port 22　　Port 50000
```

## 搭建FTP服务器
```
apt-get install vsftpd
# 开启、停止、重启vsftpd服务也很简单
service vsftpd start | stop | restart
# 修改用户密码
passwd ftp
```
关键配置，修改vsftpd的配置文件` vi /etc/vsftpd.conf`

```
#禁止匿名访问
anonymous_enable=NO
#接受本地用户
local_enable=YES
#可以上传
write_enable=YES
#启用在chroot_list_file的用户只能访问根目录
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list
#设置固定目录，在结尾添加。如果不添加这一行，各用户对应自己的目录
local_root=/srv/ftp
```

### 访问权限

- chroot_list_file 例外文件路径，默认是/etc/vsftpd.chroot_list

- chroot_list_enable 是否启用chroot_list_file配置的文件
  - `YES` chroot_list_file配置的文件生效
  - `NO` chroot_list_file配置的文件无效

- chroot_local_user 禁止访问其他目录
  - `YES` chroot_list_file配置的文件外，用户不能切换到主目录之外其他目录
  - `NO` chroot_list_file配置的文件外，用户能够切换到

### 错误处理
**530 login incorrect**
两种处理方式
1). 修改文件` vi /etc/pam.d/vsftpd`，注释掉

```
#auth    required pam_shells.so
```

2). 在 `/etc/shells` 最后一行添加`/sbin/nologin`

**500 OOPS: vsftpd: refusing to run with writable root inside chroot()**
启用`chroot_local_user`必须把访问的根目录要设置为不可写
```
chmod a-w /home/user
```

## 搭建Git服务器

```
# 安装Git
apt-get update
apt-get install git
# 新建管理账号
adduser git
```

### 管理公钥

将所有公钥添加到`/home/git/.ssh/authorized_keys`文件，一行一个

```
mkdir -p /home/git/.ssh
touch /home/git/.ssh/authorized_keys
vi /home/git/.ssh/authorized_keys
```

### 禁用shell登录
编辑`/etc/passwd`文件完成。将：
```
git:x:1001:1001:,,,:/home/git:/bin/bash
```
改为：
```
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```
禁用`shell`采用`git-shell`的好处除了确保安全外，每次登入后会自动退出

### 创建空仓库
```
cd /home/git
git init --bare sample.git
chown -R git:git sample.git
```

### 访问

```
git clone git@server:sample.git
```
Git的访问是基于SSH的，SSH默认端口为22，服务器修改了默认端口会无法访问。
```
ssh: connect to host xxx port 22: Connection refused
fatal: Could not read from remote repository.
```
这时需要修改访问的默认端口，cd到用户目录下`.ssh`文件夹，配置`config`文件
`config`文件不存在就新建，添加如下内容
```
Host "服务器地址"
Port 2333
```

### 参考

[搭建Git服务器](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)
[Git配置SSH非默认端口(22)](http://blog.csdn.net/daiwood/article/details/50561306)

## GitLab

https://packages.gitlab.com/gitlab/gitlab-ce

http://www.cnblogs.com/xishuai/p/ubuntu-install-gitlab.html
HTTP端口修改
https://segmentfault.com/a/1190000011266124
SSH端口修改
https://www.linuxidc.com/Linux/2017-02/141043.htm

**配置Postfix**
https://www.liaoxuefeng.com/article/00137387674890099a71c0400504765b89a5fac65728976000


## 搭建 Maven 镜像服务器

### 下载解压
下载地址[https://www.sonatype.com/download-oss-sonatype](https://www.sonatype.com/download-oss-sonatype)
解压
```
sudo tar -zxvf nexus-2.14.4-03-bundle.tar.gz -C /usr/local
```

### 参考
[Ubuntu 14.04 搭建Nexus Maven 私服](https://www.tianmaying.com/tutorial/maven)