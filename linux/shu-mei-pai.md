# 树莓派

## 多个WiFi配置

修改配置 `vim /etc/wpa_supplicant/wpa_supplicant.conf`

```text
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=CN

network={
    ssid="wifi1"
    key_mgmt=WPA-PSK
    psk="password1"
    priority=1
}

network={
    ssid="wifi2"
    key_mgmt=WPA-PSK
    psk="password2"
    priority=2
}

network={
    ssid="wifi3"
    key_mgmt=NONE
    wep_key0="passowrd3"
    priority=3
}

network={
    ssid="wifi4"
    key_mgmt=NONE
    priority=4
}
```

## 创建热点

安装 [create\_ap](https://github.com/oblique/create_ap.git)

```bash
# 安装依赖
apt-get install util-linux procps hostapd iproute2 iw haveged dnsmasq
git clone https://github.com/oblique/create_ap.git
cd create_ap
make install
```

修改配置 `vim /etc/create_ap.conf`

```text
SSID=wifi名称
PASSPHRASE=密码
```

重启服务 `service create_ap restart`

