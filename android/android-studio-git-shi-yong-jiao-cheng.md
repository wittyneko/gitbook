# Android Studio Git使用教程

## 创建仓库

在GitHub上创建一个新工程，这里选择了初始化一个README文件作为测试

![create repostory.png](http://upload-images.jianshu.io/upload_images/1845254-8b2a663ad9605ec6.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

Git的安装配置就不说明了，参考[http://git.oschina.net/oschina/git-osc/wikis/帮助](http://git.oschina.net/oschina/git-osc/wikis/帮助)，记得把`id_rsa.pub`公钥添加到GitHub

![add ssh keys.png](http://upload-images.jianshu.io/upload_images/1845254-813f99433440e003.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

选择一个存放工程的目录右键，`Git Bash Here` ![git bash.png](http://upload-images.jianshu.io/upload_images/1845254-0a9212d3d17ef9e0.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

输入`git clone 仓库地址`克隆远程仓库，`Shift+Insert`可以粘贴文本 ![git clone.png](http://upload-images.jianshu.io/upload_images/1845254-53d7b042a66fabe2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 添加忽略文件ignore

忽略文件可以在创建仓库时生成，不过最好自己创建了解下，系统创建可能有些编译文件没有给过滤忽略

安装`.ignore`插件`Setting > Plugins > Browser respositories` 搜索ignore，点击`Install`安装重启

![ignore.png](http://upload-images.jianshu.io/upload_images/1845254-e056bd3066952f27.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

切换为Project方式浏览，右键项目添加`igonre`，这里有很多种版本管理可选择，选择Git版本文件，接着选择项目语言，可以多选或不选自己编辑

![add gitignore file.png](http://upload-images.jianshu.io/upload_images/1845254-28879902889bedb0.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

![choose language.png](http://upload-images.jianshu.io/upload_images/1845254-5d21e2c644afadf4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

ignore文件的整理说明

```text
# 忽略IDEA工程信息文件
# IntelliJ project files
.idea/
*.iml

gen### Android template
# 忽略编译生成文件
# Generated files
bin/
gen/
out/

# 忽略Gradle编译文件
# Gradle files
.gradle/
build/

# 忽略Android编译生成文件
# Built application files
*.apk
*.ap_

# Files for the ART/Dalvik VM
*.dex

# Java class files
*.class

# Android Studio Navigation editor temp files
.navigation/

# Android Studio captures folder
captures/

# 忽略SDK配置信息文件
# Local configuration file (sdk path, etc)
local.properties

# Proguard folder generated by Eclipse
proguard/

# 忽略错误日志
# Log Files
*.log

# 忽略编译密钥
# Keystore files
*.jks
```

## 冲突文件处理

所谓冲突文件就是，两个人同时修改了同一个文件，在合并时Git不能自动处理需要用户自己来合并。以README文件为例，这里直接在GitHub上编辑加入一句`origin add message`

![origin add.png](http://upload-images.jianshu.io/upload_images/1845254-fc8ceed34cb012fc.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

本地编辑加入`local add message`

![local add message.png](http://upload-images.jianshu.io/upload_images/1845254-606d577eefb5e8da.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

选择底部`Version Control`，`Local Changes`为当前修改的文件，`Log`为历史提交记录

![Version Control.png](http://upload-images.jianshu.io/upload_images/1845254-65c82164ab5c5135.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

单击`VCS`选择提交文件，填写提交信息，`commit`提交到本地

![local update.png](http://upload-images.jianshu.io/upload_images/1845254-164635e3132b833b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

菜单`VCS > Git > Pull`，选择pull远程服务器和分支，这里只有origin/master分支，由于冲突文件会自动弹出合并提示框，也可以通过`VCS > Git > Marge Changes`自己选择合并。

![git pull.png](http://upload-images.jianshu.io/upload_images/1845254-2561e3e110dd87b0.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

![pull changes.png](http://upload-images.jianshu.io/upload_images/1845254-75151b4db96f3212.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

![Merged Dialog.png](http://upload-images.jianshu.io/upload_images/1845254-865c07e39d576345.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

弹出合并提示如果确定不要远程或本地版本可直接选择，否则选择Merge手动合并

![merge revisions.png](http://upload-images.jianshu.io/upload_images/1845254-ffe285eb7b964d46.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

这里在结果文件加入一句`merge message`，合并本地， 删除远程，选错了可以`Abort`返回重新选择

![merge change.gif](http://upload-images.jianshu.io/upload_images/1845254-2372c55442ee6aa9.gif?imageMogr2/auto-orient/strip)

修改完需要再次提交修改的文件，系统会自动生成提交信息，不喜欢可以自己修改，这次可以选择`Commit and Push`提交并推送到服务器

![Commit and Push.png](http://upload-images.jianshu.io/upload_images/1845254-d064f1fd0314ec56.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

查看下记入我们合并完成了，合并本地分支和远程原理相同，自行探索吧啊

![Log.png](http://upload-images.jianshu.io/upload_images/1845254-e7a4cee143203895.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 版本回退

首先很重要的一点，回退前记得要提交到远程以免丢失修改内容。

选择要回退的版本，右键`Reset Current Branch`，选择回退方式

![Git Reset.png](http://upload-images.jianshu.io/upload_images/1845254-fb5f4a07289db355.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

![Git Reset Mode.png](http://upload-images.jianshu.io/upload_images/1845254-0e35f57da7c5d833.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

对应的git 命令操作参考[git reset soft,hard,mixed之区别深解](http://www.cnblogs.com/kidsitcn/p/4513297.html)，引用评论的总结

> 简单总结一下，其实就是--soft 、--mixed以及--hard是三个恢复等级。使用--soft就仅仅将头指针恢复，已经add的缓存以及工作空间的所有东西都不变。如果使用--mixed，就将头恢复掉，已经add的缓存也会丢失掉，工作空间的代码什么的是不变的。如果使用--hard，那么一切就全都恢复了，头变，aad的缓存消失，代码什么的也恢复到以前状态

