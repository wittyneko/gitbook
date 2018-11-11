# 后台运行

后台执行命令

```bash
# nohub
nohup ping www.ibm.com &
ping www.ibm.com > out.file 2>&1 &
# setid
setsid ping www.ibm.com
# subshell
(ping www.ibm.com &)
# screen
screen -dmS session name 创建
screen -r session name 连接
screen -list 全部列表
```

管理

```bash
# 查看后台列表
ps -ef |grep www.ibm.com
# 关闭
kill -9 pid
```

[Linux 技巧：让进程在后台可靠运行的几种方法](http://www.ibm.com/developerworks/cn/linux/l-cn-nohup/index.html)

