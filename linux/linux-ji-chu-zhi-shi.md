# Linux 基础知识

## Socket 端口号最大值

Linux socket使用16bit无符号整型表示端口号，最大值到65535。

## 复制粘贴

- 终端下
  - 复制：Ctrl + Shift + C 
  - 粘贴：Ctrl + Shift + V 
- 控制台下
  - 复制：Ctrl + Insert 或 用鼠标选中
  - 粘贴：Shift + Insert 或 单击鼠标滚轮

## 截图

1. 键盘printscreen，整个屏幕
2. 键盘Alt+printscreen，当前窗口
3. 自带截图gnome-screenshot
4. apt-get install ksnapshot
设置快捷键，想要按下Ctrl+Alt +A 来实现区域截图依次打开 系统设置 > 键盘 > 快捷键 > 自定义快捷键 > +，在【name】输入 screenshot , 【command】输入 gnome-screenshot -a ，点击【apply】确定后，再点击disable 禁用，接着就同时按下 Ctrl+Alt +A 就可以成功设置截图快捷键了

## 内网映射

[frp](https://github.com/fatedier/frp)；
[如何远程登录家里的Ubuntu电脑(命令行模式)？](https://www.zhihu.com/question/27771692)；
[怎样从外网访问内网服务器](http://www.cnblogs.com/devymex/p/4156378.html)；
[外网主机访问虚拟机下的web服务器](http://blog.csdn.net/ai_net/article/details/7723748)；

## 创建快捷方式

创建一个`*.desktop`文件
```
[Desktop Entry]
Name=Android Studio
Comment=Android Studio IDE
Icon=/opt/android-studio/bin/studio.png
Exec=/opt/android-studio/bin/studio.sh
Terminal=false
Type=Application
Categories=Application
Encoding=UTF-8
StartupNotify=true
```

常用分类
```
Categories=Application;
PackageManager;GTK;System;Settings;
Network;WebBrowser;
Development;Emulator;
Utility;Dictionary;
Office;Spreadsheet;Qt;
AudioVideo;Player;GTK;
AudioVideo;Player;
Graphics;GTK;

```

## 重新加载资源管理器
```
nautilus -q
```

## 常用命令

```bash
# 关机
shutdown -h now
# 重启
reboot
# 修改密码
passwd root
# 查看安装位置
which firefox
# 查看软连接真正位置
ls -l /usr/bin/firefox
# 已装软件列表
dpkg -l
# 安装.deb文件
sudo apt install gdebi
sudo apt install gdebi-core
```

### 文件管理

```bash
# 当前目录
pwd
# 显示列表
ls -a 全部  -l权限
# 创建文件夹
mkdir -p 递归创建
# 创建文件
touch
# 删除
rm -rf 文件(-r 删除目录 -f 删除前不需确认)
rmdir -p 递归删除空目录
# 移动/重命名
mv
# 复制
cp
# 修改权限
owner = rwx = 4+2+1 = 7
group = rwx = 4+2+1 = 7
others= --- = 0+0+0 = 0
chmod -R 递归修改
# 修改用户组/所有者
chgrp / chown  -R 递归修改
chown -R [username]  /opt
# 链接
ln 源文件 目标文件
ln -s /etc/php.ini php.soft 生成软链接文件
ln /etc/php.ini php.hard 生成硬链接文件
# 解压文件
sudo tar -zxvf jdk-7u60-linux-x64.gz -C /usr/lib/jvm
```

### 软件管理

** 右键添加命令窗口 **
```
sudo apt-get install nautilus-open-terminal
```

** 更新应用 **
```
# 源
sudo apt update
# 可更新列表
sudo apt list --upgradable
# 指定更新
sudo apt install openssl
# 已安装更新
sudo apt upgrade
# 系统更新
sudo apt-get dist-upgrade
```

** 安装应用 **
```
1.GDebi安装程序
sudo apt instal gedbi
sudo apt update

2.dpkg安装
sudo dpkg -i <application>.deb
sudo apt install -f

3.卸载重装应用商店16.04已废弃
sudo apt-get autoremove --purge software-center
sudo apt-get install -f software-center
```

** 卸载应用 **
```
1.Synaptic软件包管理器
sudo apt-get install synaptic

2.命令
查看已安装的软件包列表
dpkg --list
完全apt-get安装的软件的程序
sudo apt-get --purge remove <programname>
只卸载程序
sudo apt-get remove <programname>
卸载自己deb包安装的软件或者apt-get 安装的软件
$sudo dpkg -r <programname>

3.应用商店，16.04已废弃
```
** 新立德软件管理 **
```
sudo apt-get install synaptic
```

** 安装Window模拟环境 **
```
sudo apt-get install wine
```

** Google 拼音 **
`sudo apt-get install ibus-googlepinyin`
[ubuntu安装google 输入法](http://www.cnblogs.com/duanguyuan/p/3480162.html)

** Chrome浏览器 **

1). Ubuntu
```
sudo add-apt-repository ppa:a-v-shkop/chromium
sudo apt-get update
sudo apt-get install chromium-browser
```

2). 其他

```
# 下载源加入到系统的源列表
# https://repo.fdzh.org/chrome/google-chrome.list
# http://www.linuxidc.com/files/repo/google-chrome.list
sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
# 更新列表获取最新版
sudo apt-get update 
# 导入谷歌软件的公钥
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
# 安装Chrome 浏览器（稳定版）
sudo apt-get install google-chrome-stable 
```


** 安装JDK **

关于JDK，Linux 有OpenJDK 和 HotSpot，OpenJDK可直接命令安装，HotSpot 只能到oracle网站下载
[Ubuntu 安装 JDK 7 / JDK8 的两种方式](http://www.cnblogs.com/a2211009/p/4265225.html)
```
sudo apt-get install openjdk-7-jdk
sudo apt-get install openjdk-8-jdk

```

** JDK配置环境变量 **

1). 加入环境变量（修改/etc/profile）
```
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export JAVA_HOME
CLASSPATH=.:$JAVA_HOME/lib
export CLASSPATH
ANDROID_SDK=/opt/android-sdk-linux
export ANDROID_SDK
PATH=$PATH:$JAVA_HOME/bin:$ANDROID_SDK/tools:$ANDROID_SDK/platform-tools
export PATH
```
2). 立即生效
```
source /etc/profile  
```


3). 多个jdk版本 `alternatives` 更新
为不同的命令建立/替换链接
```
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/java/jdk_8u60/bin/java" 300
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/java/jdk_8u60/bin/javac" 300
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/java/jdk_8u60/bin/javaws" 300

```
选择链接，存在多个链接，根据需要选择不同选项
```
sudo update-alternatives --config java
sudo update-alternatives --config javac
sudo update-alternatives --config javaws
```

[Ubuntu 15.04 安装JDK并配置成为默认的JDK](http://www.linuxidc.com/Linux/2015-09/122689.htm)

** Genymotion 模拟器安装 **

```
sudo apt install virtualbox-qt
sudo chmod u+x genymotion-2.8.1_x64.bin
sudo ./genymotion-2.8.1_x64.bin
```

** SVN **

```
sudo apt-get install subversion
```
软件 [rabbitvcs](http://wiki.rabbitvcs.org/wiki/install/ubuntu)

**PHP XAMPP + Composer**

 [ubuntu16.04安装 composer 和 laravel](https://blog.csdn.net/yc1022/article/details/54580716 )


[How To Install and Use Composer on Ubuntu 14.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-14-04)

[简介| Composer 中文文档| Composer 中文网](https://docs.phpcomposer.com/00-intro.html)

[在Ubuntu 16.04 下配置Nginx + PHP 7.0 + MySQL 环境- ZGQ's Blog](https://blog.izgq.net/archives/763/)

