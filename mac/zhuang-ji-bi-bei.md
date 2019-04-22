# 装机必备

## ohmyzsh

```text
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## 终端 App Store

```text
brew install mas
```

## site

[cleanmymac-3](https://macpaw.com/cleanmymac-3)、 [synergy2](https://symless.com/synergy/downloads/list/s2)、 [eudic](https://www.eudic.net/eudic/mac_dictionary.aspx)

## 环境变量设置

### 加载顺序

bash

`/etc/profile`,`/etc/bashrc`,`/etc/paths`,`/etc/paths.d/`,`~/.bash_profile`

zsh

`/etc/profile`,`/etc/zshrc`,`/etc/paths`,`/etc/paths.d/`,`~/.zshrc`

### 添加

```bash
# profile
export PATH="$PATH:<PATH 1>:<PATH 2>:<PATH 3>:...:<PATH N>"
# paths
sudo -s 'echo "/usr/local/sbin/mypath" > /etc/paths.d/mypath'
export PATH="$PATH:<PATH 1>:<PATH 2>:<PATH 3>:...:<PATH N>"
```

### 查看

PATH `echo $PATH`

内置SHELL `cat shells`

### 我的配置

```bash
# Go
export GOROOT=/usr/local/Cellar/go/1.12/libexec
export GOPATH=/Users/wittyneko/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOBIN:$GOROOT/bin

# Android
export ANDROID_HOME=~/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

# Flutter
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
export FLUTTER_HOME=~/Library/flutter
export PATH=$PATH:$FLUTTER_HOME/bin
```

[macOS/Linux 环境变量设置- 知乎](https://zhuanlan.zhihu.com/p/25976099)

## Dnsmasq

```text
brew install dnsmasq
vim /usr/local/etc/resolv.dnsmasq.conf
vim /usr/local/etc/dnsmasq.conf
# /usr/local/etc/dnsmasq.d/*
# 清除DNS缓存
sudo killall -HUP mDNSResponder
# 重启
sudo brew services stop dnsmasq
sudo brew services start dnsmasq
sudo launchctl stop homebrew.mxcl.dnsmasq
sudo launchctl start homebrew.mxcl.dnsmasq
```

### 自定义解析

`/usr/local/etc/dnsmasq.d/my.address.conf`

```text
# 加速GitHub访问
address=/github.com/192.30.253.112
address=/github.com/192.30.253.113
```

[ipaddress ip-lookup](https://www.ipaddress.com/ip-lookup)  
[dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)   
[利用Dnsmasq 部署DNS 服务- 运维之美](https://www.hi-linux.com/posts/30947.html)  
[Mac上用dnsmasq配置DNS服务器](https://blog.csdn.net/lovenjoe/article/details/51210937)

## 预览增强

[增强 Mac「预览」功能（QuickLook）的教程](https://sspai.com/31927)

[QuickLookPlugins.com](http://www.quicklookplugins.com/)

```bash
# markdown
brew cask install qlmarkdown
# code
brew cask install qlcolorcode
brew cask install scriptql
# webp
brew cask install webpquicklook
# zip 
# or http://macitbetter.com/BetterZipQL.zip
brew cask install hetimazipql
```

## 压缩

[Mac 压缩 / 解压缩工具解决方案](https://sspai.com/post/46943)

* The Unarchiver `brew cask install the-unarchiver`
* Keka `brew cask install keka kekadefaultapp`
* WinRAR `brew cask install rar`

## NTFS

```bash
brew cask install mounty
```
[Mounty for NTFS](https://mounty.app)

## 文件备份

[文件备份还能怎么玩？试试这条命令](https://sspai.com/post/41967)

```bash
# rsync -av [源文件夹路径] [备份路径]
# rsync -av [源文件夹路径] [备份路径] --delete
```

[ 添加Mac的Time Machine备份到smb网络硬盘（windows 共享文件夹）](https://www.douban.com/note/614980869/)

```bash
sudo tmutil setdestination -p /Volumes/backup/
```

## 下载

[除了会员，别无选择？6 款 Mac 下载工具帮你加速](https://sspai.com/post/41174)

`Folx 5`、`FDM`、`Leech 3`、`uTorrent`、`Transmission`、`Aria2`

## Markdown

[Typora 主题](https://sspai.com/post/43873)

## 数据库

[SequelPro](http://www.sequelpro.com/) [DBeaver](https://dbeaver.jkiss.org)

