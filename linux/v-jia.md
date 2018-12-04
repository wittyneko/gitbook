# V+

### BBR
 [开启TCP BBR拥塞控制算法](https://github.com/iMeiji/shadowsocks_install/wiki/%E5%BC%80%E5%90%AFTCP-BBR%E6%8B%A5%E5%A1%9E%E6%8E%A7%E5%88%B6%E7%AE%97%E6%B3%95)
```sh
# 安装更新内核Ubuntu16.04
apt install --install-recommends linux-generic-hwe-16.04
apt autoremove
# 14.04
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.16/linux-image-4.16.0-041600-generic_4.16.0-041600.201804012230_amd64.deb
dpkg -i linux-image-4.*.deb
dpkg -l | grep linux-image 
apt-get purge <old core>
# 重启查看内核
update-grub
reboot
uname -r
# 检测是否启用bbr
uname -r
lsmod | grep bbr
# 启用bbr
modprobe tcp_bbr
echo "tcp_bbr" | sudo tee --append /etc/modules-load.d/modules.conf
echo "net.core.default_qdisc=fq" | sudo tee --append /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" | sudo tee --append /etc/sysctl.conf
sysctl -p
# 检测
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
```

[OpenVZ 平台 Google BBR 加速 TCP 之 Rinetd 方式](https://blog.kuoruan.com/119.html)
```bash
curl https://raw.githubusercontent.com/linhua55/lkl_study/master/get-rinetd.sh | bash
iptables -t raw -nL

vi /etc/rinetd-bbr.conf
ip addr
/usr/bin/rinetd-bbr -f -c /etc/rinetd-bbr.conf raw venet0:0 &

```
/etc/rinetd-bbr.conf

```
# bindadress bindport connectaddress connectport
 
0.0.0.0 443 0.0.0.0 443
```

[OpenVZ 平台 Google BBR 一键安装脚本](https://blog.kuoruan.com/116.html)
```bash
wget https://raw.githubusercontent.com/kuoruan/shell-scripts/master/ovz-bbr/ovz-bbr-installer.sh
chmod +x ovz-bbr-installer.sh
./ovz-bbr-installer.sh

systemctl {start|stop|restart} haproxy-lkl
service haproxy-lkl {start|stop|restart}

# 检查
iptables -t nat -nL
# 修改
vi /usr/local/haproxy-lkl/etc/port-rules
# 卸载
./ovz-bbr-installer.sh uninstall
```


### 锐速

https://www.moerats.com/archives/387/

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

https://xpsss.com/859.html
```
wget http://ftp.al/appex.sh
chmod +x appex.sh
bash appex.sh install
```

### 安装v2

```sh
bash <(curl -L -s https://install.direct/go.sh)
bash <(wget https://install.direct/go.sh -O -)

# 指定版本
wget https://install.direct/go.sh
chmod a+x go.sh
./go.sh --version 4.5.0
```

### WS-TLS
`${}` 替换为你的配置

```sh
# acme需要
apt install socat curl
# 安装acme
curl  https://get.acme.sh | sh
source ~/.bashrc
# 生成证书
~/.acme.sh/acme.sh --issue -d ${my.com} --standalone -k ec-256
# 安装证书
~/.acme.sh/acme.sh --installcert -d ${my.com} --fullchainpath /etc/v2ray/v2ray.crt --keypath /etc/v2ray/v2ray.key --ecc
# 删除
acme.sh --remove -d ${my.com} --ecc
# 吊销
acme.sh --revoke -d ${my.com} --ecc
```

vim `gg` + `dG` 清空内容，`i` 插入编辑，`esc` + `:wq` 保存退出

v2ray config `vim /etc/v2ray/config.json`
```json
{
  "inbounds": [
    {
      "port": 10000,
      "listen": "127.0.0.1",
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "${uuid}",
            "level": 1,
            "alterId": 6
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
          "path": "/path"
        }
      }
    }
  ],
  "outbounds": [
    {
      "tag": "directout",
      "protocol": "freedom",
      "settings": {}
    },
    {
      "tag": "blockout",
      "protocol": "blackhole",
      "settings": {}
    }
  ],
  "routing": {
    "rules": [
      {
        "type": "field",
        "ip": [
          "geoip:private"
        ],
        "outboundTag": "blockout"
      }
    ]
  }
}
```
`systemctl restart v2ray`
### Nginx

[Debian 8 安装Nginx最新版本](https://www.cnblogs.com/geons/p/install_nginx.html)
[Ubuntu 16.04系统中Nginx上配置HTTP/2简明教程](https://ywnz.com/linuxyffq/2103.html)
```bash
apt install nginx

apt remove  nginx nginx-common nginx-full


```

http://nginx.org/en/linux_packages.html

https://www.binss.me/blog/install-lastest-nginx-on-ubuntu/

https://blog.csdn.net/yjk13703623757/article/details/78945576

```bash
wget http://nginx.org/keys/nginx_signing.key
apt-key add nginx_signing.key
apt-cache policy nginx
apt install nginx=1.10.3-1~trusty
```
```
root   /usr/share/nginx/html;
/etc/nginx/nginx.conf
/etc/nginx/conf.d
```
`vim /etc/nginx/sites-enabled/v2ray`
```cfg
server {
    listen 443 ssl default_server;
    listen [::]:443 ssl default_server;

    # Add index.php to the list if you are using PHP
    index index.html index.htm index.nginx-debian.html;

    #server_name _;
    server_name ${my.com};

    ssl on;
    ssl_certificate       /etc/v2ray/v2ray.crt;
    ssl_certificate_key   /etc/v2ray/v2ray.key;
    ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers           HIGH:!aNULL:!MD5;


    location /path {
        proxy_redirect off;
        proxy_pass http://127.0.0.1:10000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;
    }

    location / {
        try_files $uri $uri/ =404;
    }
}
```

service nginx restart

### 客户端
```json
{
    "inbounds": [
        {
            "tag": "socksin",
            "port": 1080,
            "listen": "0.0.0.0",
            "protocol": "socks",
            "settings": {
                "auth": "noauth",
                "udp": true
            },
            "snifffing": {
                "enabled": false,
                "destOverride": [
                    "tls",
                    "http"
                ]
            }
        },
        {
            "tag": "httpin",
            "port": 1087,
            "listen": "0.0.0.0",
            "protocol": "http",
            "settings": {
                "timeout": 0
            },
            "snifffing": {
                "enabled": false,
                "destOverride": [
                    "tls",
                    "http"
                ]
            }
        }
    ],
    "outbounds": [
        {
            "tag": "proxyout",
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "${my.com}",
                        "port": 443,
                        "users": [
                            {
                                "id": "${uuid}",
                                "alterId": 64,
                                "security": "auto"
                            }
                        ]
                    }
                ]
            },
            "streamSettings": {
                "network": "ws",
                "security": "tls",
                "wsSettings": {
                    "path": "/path",
                    "headers": {
                        "Host": "${my.com}"
                    }
                },
                "httpSettings": {
                    "path": "/path"
                },
                "tlsSettings": {
                    "serverName": "${my.com}",
                    "allowInsecure": false
                },
                "sockopt": {
                    "tcpFastOpen": true
                }
            }
        },
        {
            "tag": "directout",
            "protocol": "freedom",
            "settings": {}
        },
        {
            "tag": "blockout",
            "protocol": "blackhole",
            "settings": {}
        }
    ],
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "outboundTag": "directout",
                "domain": [
                    "geosite:cn"
                ],
                "ip": [
                    "0.0.0.0/8",
                    "10.0.0.0/8",
                    "100.64.0.0/10",
                    "127.0.0.0/8",
                    "169.254.0.0/16",
                    "172.16.0.0/12",
                    "192.0.0.0/24",
                    "192.0.2.0/24",
                    "192.168.0.0/16",
                    "198.18.0.0/15",
                    "198.51.100.0/24",
                    "203.0.113.0/24",
                    "::1/128",
                    "fc00::/7",
                    "fe80::/10",
                    "geoip:private",
                    "geoip:cn"
                ]
            }
        ]
    }
}
```
[官网](https://www.v2ray.com)
[V2Ray 配置指南](https://toutyrater.github.io)