# FRP

## 简单SSH配置

### 服务端frps

配置文件`/frp/frps.ini`

```text
[common]
bind_port = 7000
token = 12345678
```

自动启动`/lib/systemd/system/frps.service`

```text
[Unit]
Description=fraps service
After=network.target network-online.target syslog.target
Wants=network.target network-online.target

[Service]
Type=simple
Restart=on-failure
RestartSec=300s

ExecStart=/frp/frps -c /frp/frps.ini

[Install]
WantedBy=multi-user.target
```

管理命令

```text
# 允许开机启动
systemctl enable frps
# 启动
systemctl start frps
# 重启
systemctl restart frps
# 停止
systemctl stop frps
# 状态
systemctl status frps
```

### 客户端frpc

配置文件`/frp/frpc.ini`

```text
[common]
server_addr = xxxx.xx
server_port = 7000
token = 12345678

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
```

自动启动`/lib/systemd/system/frpc.service`

```text
[Unit]
Description=fraps service
After=network.target network-online.target syslog.target
Wants=network.target network-online.target

[Service]
Type=simple
Restart=on-failure
RestartSec=300s

ExecStart=/frp/frpc -c /frp/frpc.ini

[Install]
WantedBy=multi-user.target
```

管理命令

```text
# 允许开机启动
systemctl enable frpc
# 启动
systemctl start frpc
# 重启
systemctl restart frpc
# 停止
systemctl stop frpc
# 状态
systemctl status frpc
```

## 参考

[Systemd 入门教程：实战篇](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html) [为 Syncer 选用守护进程工具](https://www.tidb.cc/Docs/180323-Systemd-Syncer.html)

