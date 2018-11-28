# 酸酸乳好喝

虽然好喝没事少喝点。

## 一键配置

```text
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
```

## 终端代理

```text
export ALL_PROXY=socks5://127.0.0.1:1080
export http_proxy="socks5://127.0.0.1:1080"
export https_proxy="socks5://127.0.0.1:1080"
```

## Git代理

`git config --global http.proxy "socks5://127.0.0.1:1080"` /User/.ssh/config

```text
# 这里必须是 github.com，因为这个跟我们 clone 代码时的链接有关
Host github.com
   HostName github.com
   User git
   # 如果是 HTTP 代理，把 proxyport 改成自己的 http 代理的端口
   # ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8123
   # 如果是 socks5 代理，把 6666 改成自己 socks5 代理的端口
   # ProxyCommand nc -v -x 127.0.0.1:1080 %h %p
```

## 登入服务器

Window如果安装了Git客户端，可以直接命令使用ssh登入

```text
ssh 用户@服务器IP
ssh -p 端口 用户@服务器IP
ssh root@192.168.68.1
```

或者下载putty客户端 [http://www.chiark.greenend.org.uk/~sgtatham/putty/](http://www.chiark.greenend.org.uk/~sgtatham/putty/)

## 安装pip和git

centos：

```bash
yum install -y python-setuptools && easy_install pip
yum install -y git
```

ubuntu/debian：

```bash
apt-get install python-pip
apt-get install git
```

## 克隆仓库的manyuser分支

```text
git clone -b manyuser https://github.com/shadowsocksrr/shadowsocksr.git
# or 
git clone -b manyuser https://github.com/shadowsocksr-backup/shadowsocksr.git
```

![clone.png](http://upload-images.jianshu.io/upload_images/1845254-74743e19a147d66b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 初始化&生成随机账号

```text
cd shadowsocksr
bash initmudbjson.sh
```

## 初始化手动配置

```text
cd shadowsocksr
bash initcfg.sh
```

执行完会多出3个user开头文件

![initcfg.png](http://upload-images.jianshu.io/upload_images/1845254-3e9e2e46fe46096f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 创建用户

这里介绍json多用户配置方式，更多方式查看源文档

```text
//查看帮助
python mujson_mgr.py -h
//添加账号(端口、秘密是必须参数，更多参考帮助)
python mujson_mgr.py -a -p 端口 -k 秘密 -m 加密方式 -O 协议 -o 混淆
```

![create user.png](http://upload-images.jianshu.io/upload_images/1845254-0fc10985d96a33d2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

eg. 添加

```text
python mujson_mgr.py -a -u tutu -p 6000 -k 123456 -m a2 -O +as -o +1
```

eg. 修改

```text
python mujson_mgr.py -e -u tutu -m r -O as -o +1
```

参数前带`+`表示兼容`shadowsock`，建议不设置兼容更安全。 参数可查看源码

```text
    fast_set_obfs = {'0': 'plain',
            '+1': 'http_simple_compatible',
            '1': 'http_simple',
            '+2': 'tls1.2_ticket_auth_compatible',
            '2': 'tls1.2_ticket_auth'}
    fast_set_protocol = {'0': 'origin',
            's4': 'auth_sha1_v4',
            '+s4': 'auth_sha1_v4_compatible',
            'am': 'auth_aes128_md5',
            'as': 'auth_aes128_sha1',
            'ca': 'auth_chain_a',
            }
    fast_set_method = {'0': 'none',
            'a1c': 'aes-128-cfb',
            'a2c': 'aes-192-cfb',
            'a3c': 'aes-256-cfb',
            'r': 'rc4-md5',
            'r6': 'rc4-md5-6',
            'c': 'chacha20',
            'ci': 'chacha20-ietf',
            's': 'salsa20',
            'a1': 'aes-128-ctr',
            'a2': 'aes-192-ctr',
            'a3': 'aes-256-ctr'}
```

## 更改默认配置

默认采用数据多用户版本，`vi userapiconfig.py`修改配置

```text
API_INTERFACE = 'sspanelv2'
```

改为

```text
API_INTERFACE = 'mudbjson'
```

![update config](http://upload-images.jianshu.io/upload_images/1845254-b09d722c5118f290.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 运行与停止

后台运行（无log，ssh窗口关闭后也继续运行）

```text
./run.sh
```

后台运行（输出log，ssh窗口关闭后也继续运行）

```text
./logrun.sh
```

后台运行时查看运行情况

```text
./tail.sh
```

停止运行

```text
./stop.sh
```

#### 客户端使用

Windows有客户端软件，以下是Linux系统的使用，在配合genpac生成个自动代理

创建配置文件

```text
mkdir /etc/shadowsocksr
vi /etc/shadowsocksr/config
```

内容模板

```text
{
    "server":"服务器IP",
    "server_ipv6": "::",
    "server_port":服务器端口,
    "password":"密码",
    "local_address": "127.0.0.1",
    "local_port":1080,
    "timeout":350,
    "method":"rc4-md5",
    "protocol":"auth_aes128_sha1",
    "obfs":"http_simple",
    "fast_open": false,
    "workers": 1
}
```

后台启动

```text
sudo /opt/shadowsocksr/shadowsocks/local.py -c /etc/shadowsocksr/config -d start
```

注：通过脚本运行默认日志会保存在根目录的ssserver.log，可手动查看。

附：更多操作 [https://github.com/breakwa11/shadowsocks-rss/wiki](https://github.com/breakwa11/shadowsocks-rss/wiki)



---

## 代理配置

### PAC代理
- **[genpac](https://github.com/JinnLynn/genpac)**

```
# 从github安装开发版本
$ pip install https://github.com/JinnLynn/genpac/archive/master.zip  # sudo
```
没加入`sudo`可在pip安装后在`/home/wittyneko/.local/bin`查看python执行genpac
1). 生成配置
```
# 创建目录
sudo mkdir /etc/genpac
# 修改权限
sudo chmod a+w -R /etc/genpac
# 生成配置文件
genpac --init /etc/genpac
vim /etc/genpac/config.init
```
2). 修改配置文件`config.init`
```
[config]
pac-proxy = "SOCKS5 127.0.0.1:1080; PROXY 127.0.0.1:8123; DIRECT"
gfwlist-proxy = SOCKS5 127.0.0.1:1080
gfwlist-local = /etc/genpac/gfwlist.txt
update-gfwlist-local = true
user-rule-from = /etc/genpac/user-rules.txt
output = /etc/genpac/autoproxy.pac
```
3). 生成代理文件
```
# 1. 配置文件生成
genpac -c /etc/genpac/config.init
# 2. 禁用gfwlist，自定义路径
genpac -c /etc/genpac/config.ini --gfwlist-disabled -o /etc/genpac/userproxy.pac
# 3. 直接生成
genpac -p "SOCKS5 127.0.0.1:1080" --gfwlist-proxy "SOCKS5 127.0.0.1:1080" -o /etc/genpac/autoproxy.pac"
```
**[gfwlist](https://github.com/gfwlist/gfwlist)**
部分系统全局代理不需要file://前缀，跟网上说的不一样
gfwlist2Pac
http://blog.csdn.net/weiqiangsu/article/details/46956977
https://github.com/JinnLynn/genpac


### Polipo 设置全局代理
https://jingsam.github.io/2016/05/08/setup-shadowsocks-http-proxy-on-ubuntu-server.html

1. 安装Polipo
`sudo apt-get install polipo`

2. 修改polipo的配置文件/etc/polipo/config

```
logSyslog = true
logFile = /var/log/polipo/polipo.log

proxyAddress = "0.0.0.0"

socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5

chunkHighMark = 50331648
objectHighMark = 16384

serverMaxSlots = 64
serverSlots = 16
serverSlots1 = 32

```
重启polipo服务
`sudo /etc/init.d/polipo restart`

终端配置http代理
`export http_proxy="http://127.0.0.1:8123/"`


