# Shell Auto

## zenity 弹框输入密码

```bash
#!/bin/bash

export DIR=$(cd `dirname $0`; pwd)
export PASSWORD=$(zenity --password --title "password")
sudo -v -S <<EOF
$PASSWORD
EOF
nohup sudo $DIR/manager-linux-x64.run
```

## expect + zenity

检测 & 安装expect是否已经安装

```text
ls /usr/bin | grep expect
sudo apt-get install tcl tk expect
```

```bash
#!/bin/bash
export PASSWORD=$(zenity --password)
expect <<EOF
set timeout 5
spawn sudo -v
expect {
   "sudo" {send "${PASSWORD}\n"}
   "password" {send "${PASSWORD}\n"}
}
expect eof
interact
exit
EOF

nohup sudo /opt/lampp/manager-linux-x64.run
```

gnome-desktop-item-edit --create-new ~/Desktop

[https://segmentfault.com/a/1190000011438491](https://segmentfault.com/a/1190000011438491) [https://blog.csdn.net/chaolovejia/article/details/47311807](https://blog.csdn.net/chaolovejia/article/details/47311807) [https://blog.csdn.net/zilong00007/article/details/6681090](https://blog.csdn.net/zilong00007/article/details/6681090) [https://blog.csdn.net/wyl9527/article/details/72831567](https://blog.csdn.net/wyl9527/article/details/72831567)

## path

```bash
#!/bin/bash
echo '$0: '$0
echo "pwd: "`pwd`
echo "============================="
echo "scriptPath1: "$(cd `dirname $0`; pwd)
echo "scriptPath2: "$(pwd)
echo "scriptPath3: "$(dirname $(readlink -f $0))
echo "scriptPath4: "$(cd $(dirname ${BASH_SOURCE:-$0});pwd)
echo -n "scriptPath5: " && dirname $(readlink -f ${BASH_SOURCE[0]})
```

## http\_proxy.sh

```bash
export http_proxy="http://127.0.0.1:1087"
export https_proxy="http://127.0.0.1:1087"
```

## un\_http\_proxy.sh

```bash
export http_proxy=""
export https_proxy=""
```

## test

```bash
source http_proxy.sh
curl -I -m 1 -o /dev/null -s -w "%{http_code}\n" www.google.com
source un_http_proxy.sh
echo $(curl -I -m 1 -o /dev/null -s -w %{http_code} www.google.com)
```

## groovy

```text
println "ls".execute().text

def sout = new StringBuilder(), serr = new StringBuilder()
def proc = 'ls /badDir'.execute()
proc.consumeProcessOutput(sout, serr)
proc.waitForOrKill(1000)
println "out> $sout err> $serr"
```

## Link

[有哪些命令行的软件堪称神器？ - 知乎](https://www.zhihu.com/question/59227720)

