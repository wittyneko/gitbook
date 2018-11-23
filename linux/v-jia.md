# V 家

### BBR
 [开启TCP BBR拥塞控制算法](https://github.com/iMeiji/shadowsocks_install/wiki/%E5%BC%80%E5%90%AFTCP-BBR%E6%8B%A5%E5%A1%9E%E6%8E%A7%E5%88%B6%E7%AE%97%E6%B3%95)
```sh
# 安装更新内核Ubuntu16.04
apt install --install-recommends linux-generic-hwe-16.04
apt autoremove
# 重启查看内核
update-grub
reboot
uname -r
# 检测是否启用bbr
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
```

### WS-TLS
```sh
# acme需要
apt install socat
# 安装acme
curl  https://get.acme.sh | sh
source ~/.bashrc
# 生成证书
~/.acme.sh/acme.sh --issue -d my.xyz --standalone -k ec-256
# 安装证书
~/.acme.sh/acme.sh --installcert -d my.xyz --fullchainpath /etc/v2ray/v2ray.crt --keypath /etc/v2ray/v2ray.key --ecc
```
v2ray config `vim /etc/v2ray/config.json`
```json
{
  "inbound": {
    "port": 10000,
    "listen":"127.0.0.1",
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "uuid",
          "level": 1,
          "alterId": 64
        }
      ]
    },
    "streamSettings": {
      "network": "ws",
      "wsSettings": {
      "path": "/about"
      }
    }
  },
  "outbound": {
    "protocol": "freedom",
    "settings": {}
  },
  "outboundDetour": [
    {
      "protocol": "blackhole",
      "settings": {},
      "tag": "blocked"
    }
  ],
  "routing": {
    "strategy": "rules",
    "settings": {
      "rules": [
        {
          "type": "field",
          "ip": ["geoip:private"],
          "outboundTag": "blocked"
        }
      ]
    }
  }
}
```
`systemctl restart v2ray`
### nginx

```
apt install nginx
```
`vim /etc/nginx/sites-available/default`
```cfg
server {
	listen 443 ssl default_server;
	listen [::]:443 ssl default_server;

	# Add index.php to the list if you are using PHP
	index index.html index.htm index.nginx-debian.html;

	#server_name _;
	server_name my.xyz;

	ssl on;
	#ssl_certificate       /etc/v2ray/v2ray.crt;
	#ssl_certificate_key   /etc/v2ray/v2ray.key;
	#ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;
	#ssl_ciphers           HIGH:!aNULL:!MD5;


	location /about {
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
```
{
  "inbound": {
    "port": 1080,
    "listen": "127.0.0.1",
    "protocol": "socks",
    "domainOverride": ["tls","http"],
    "settings": {
      "auth": "noauth",
      "udp": false
    }
  },
  "outbound": {
    "protocol": "vmess",
    "settings": {
      "vnext": [
        {
          "address": "my.xyz",
          "port": 443,
          "users": [
            {
              "id": "uuid",
              "alterId": 64
            }
          ]
        }
      ]
    },
    "streamSettings": {
      "network": "ws",
      "security": "tls",
      "wsSettings": {
        "path": "/about"
      }
    }
  }
}
```
[官网](https://www.v2ray.com)
[V2Ray 配置指南](https://toutyrater.github.io)