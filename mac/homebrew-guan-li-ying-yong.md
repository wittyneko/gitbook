# Homebrew 管理应用

## 安装

[HomeBrew常规使用教程](https://link.juejin.im/?target=https%3A%2F%2Fjuejin.im%2Fpost%2F5a559b9f6fb9a01cba42772f)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 常用命令

#### 安装卸载软件

* `brew --version` 或者 `brew -v` 显示brew版本信息
* `brew install <formula>` 安装指定软件
* `brew unistall <formula>` 卸载指定软件
* `brew list`  显示所有的已安装的软件
* `brew search text` 搜索本地远程仓库的软件，已安装会显示绿色的勾
* `brew search /text/` 使用正则表达式搜软件

#### 升级

* `brew update` 自动升级homebrew（从github下载最新版本）
* `brew outdated` 检测已经过时的软件
* `brew upgrade`  升级所有已过时的软件，即列出的以过时软件
* `brew upgrade <formula>` 升级指定的软件
* `brew pin <formula>` 禁止指定软件升级
* `brew unpin <formula>` 解锁禁止升级
* `brew upgrade --all` 升级所有的软件包，包括未清理干净的旧版本的包

#### 清理

homebrew再升级软件时候不会清理相关的旧版本

* `brew cleanup -n` 列出需要清理的内容
* `brew cleanup <formula>` 清理指定的软件过时包
* `brew cleanup` 清理所有的过时软件
* `brew unistall <formula>` 卸载指定软件
* `brew unistall <fromula> --force` 彻底卸载指定软件，包括旧版本

## Homebrew Cask

* `brew search <app>` 搜索
* `brew cask install <app>` 安装软件
* `brew cask uninstall <app>` 卸载 软件
* `brew cask info <app>` 相关信息
* `brew cask list` 已安装列表
* `brew cask update` 更新

### 常用软件

```bash
brew cask install google-chrome
thunder
baidunetdisk
sogouinput
neteasemusic
wechat
qq

keka
jietu
skitch
mplayerx
eudic
evernote
gitbook
typora


iterm2
alfred
synergy
vnc-viewer

atom
sublime-text
visual-studio-code
android-studio
sourcetree

v2rayx
shadowsocksx-ng-r

obs
soundflower
```

