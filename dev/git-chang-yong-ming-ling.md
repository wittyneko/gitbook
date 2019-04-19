# Git 常用命令

## 初始全局配置

```text
git config --global user.name "wittyneko"
git config --global user.email "wittytutu@gmail.com"
```

## 生成SSH key并测试连接

```text
ssh-keygen -t rsa -C "wittytutu@gmail.com"
# 测试链接
ssh -T git@github.com
ssh -T git@git.oschina.net
```

## 断点续传

`git clone`不支持断点续传，可以使用支持断点续传的`git fetch`

```text
mkdir linux && cd linux
git init
git fetch git://mirrors.ustc.edu.cn/linux.git
git checkout FETCH_HEAD
```

## 远程

推送`master`分支到`origin`远程仓库

```text
# git push [远程名] [本地分支]:[远程分支]
git push origin master
```

`-u`推送关联远程仓库，第一次提交到远程仓库

```text
git push -u origin master
```

`-f`使用本地内容覆盖远程仓库

```text
git push -f origin master
git push origin HEAD --force
git push origin HEAD:master --force
```

### 同时push多个远程仓库

[终端下如何配置 git 使其可以同时 push 到两个远程仓库？](https://segmentfault.com/q/1010000000764992)

## 代理配置

### http.proxy

```bash
# 当前项目
git config http.proxy socks5://127.0.0.1:10808
git config http.proxy http://127.0.0.1:8088
git config http.proxy http://username:password@127.0.0.1:8088
# 全局
git config --global http.proxy socks5://127.0.0.1:10808
git config --global http.proxy http://127.0.0.1:8088
# 删除代理
git config --global --unset http.proxy
#只对github.com代理
git config --global http.https://github.com.proxy socks5://127.0.0.1:10808
git config --global --unset http.https://github.com.proxy)

# 关闭证书验证
git config --global http.sslVerify false
```

### core.gitProxy

创建`socks5_proxy_wrapper`

{% tabs %}
{% tab title="connect " %}
```bash
#!/bin/sh
connect -S 127.0.0.1:8088 "$@"
```
{% endtab %}

{% tab title="ncat" %}
```bash
#!/bin/sh
/usr/bin/ncat --proxy 127.0.0.1:1081 --proxy-type socks5 "$@"
```
{% endtab %}
{% endtabs %}

```bash
# 配置 gitProxy 
git config --global core.gitProxy '/opt/bin/socks5_proxy_wrapper'
git config --global core.gitProxy '/opt/bin/socks5_proxy_wrapper for git.kernel.org'
或 export GIT_PROXY_COMMAND
export GIT_PROXY_COMMAND="/opt/bin/socks5_proxy_wrapper"
```

### ssh

{% tabs %}
{% tab title="~/.ssh/config" %}
Mac & Linux `~/.ssh/config`  
1, https.proxy设置是无用的, 只需要设置http.proxy  
2, socks5h://更好, 远端DNS

```bash
ost github.com
    User git
    ProxyCommand nc -v -x 127.0.0.1:1086 %h %p
    # ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=6667
```

Windows

```bash
Host github.com
    User git
    ProxyCommand connect -S 127.0.0.1:1086 %h %p
```
{% endtab %}

{% tab title="GIT\_SSH" %}
创建 `socks5_proxy_ssh`

```text
#!/bin/sh
ssh -o ProxyCommand="/path/to/socks5_proxy_wrapper %h %p" "$@"
```

```text
export GIT_SSH="/path/to/socks5_proxy_ssh"
```
{% endtab %}
{% endtabs %}

[git 设置和取消代理](https://gist.github.com/laispace/666dd7b27e9116faece6)  
[Windows下git使用代理服务器的设置方法](http://blog.useasp.net/archive/2015/08/26/config-git-proxy-settings-on-windows.aspx)  
[\[整理\]为git 和ssh 设置socks5 协议的代理](https://blog.systemctl.top/2017/2017-09-28_set-proxy-for-git-and-ssh-with-socks5/)

## 分支

查看分支

```text
git branch -a
```

切换分支\(切换前先提交更改\)

```text
git checkout master
```

查看比较远程分支和本地分支

```text
git remote show origin
```

删除本地不存在的远程分支

```text
git remote prune origin
```

## 记录

git rm --cached logs/xx.log 删除已提交文件记录  
git log -v

## 其他

//添加gradle项目结构  
git init  
git remote add gradle git@github.com:brady9308/gradle-frame.git  
git pull gradle master  
//不添加gradle项目结构  
git init  
git remote add gradle git@github.com:brady9308/gradle-frame.git  
git pull gradle gradle  
//删除文件夹.git，清空版本管理信息  
rm -rf .git  
//新建项目版本管理  
git init  
git remote add origin git@github.com:brady9308/android-sample.git  
git push -u origin master

/////git command/////  
//\(HEAD, HEAD^, HEAD~1\)  
//HEAD 最近一个提交， HEAD^ 上一次  
git push -u origin master //推送关联远程仓库  
git push -f origin master //推送覆盖远程仓库  
git push origin HEAD --force //推送覆盖远程仓库  
git push origin HEAD:master --force //推送覆盖远程仓库

git branch gradle //创建分支  
git checkout gradle //检出\(切换\)分支  
git checkout -b gradle //创建并检出分支  
git commit -a -m "create new branch" //创建新分支指针  
git merge gradle //合并分支\(回到主分支\)  
git branch -d gradle //删除分支

git fetch origin //获取远程更新内容  
git checkout --track origin/gradle //创建检出远程分支  
git checkout -b gd origin/gradle //创建检出远程分支  
git merge origin/gradle //合并远程分支  
git push \[远程名\] \[本地分支\]:\[远程分支\]  
git push origin :gradle //删除远程分支  
git push origin --delete gradle //删除远程分支  
\`  
git reset &lt;tag \| commit\_id \| HEAD&gt; //重置提交，commit和index  
git reset -soft //重置提交，commit  
git reset -head //重置提交，内容、commit和index  
git reset &lt;文件名&gt; //重置单个文件提交  
git checkout -- &lt;file name&gt; //检出head指向版本的文件

git log --pretty=oneline 文件名 //查看commit历史  
git log filename //查看commit历史  
git log -p filename //提交的diff信息  
git show commit\_id filename //文件变化

