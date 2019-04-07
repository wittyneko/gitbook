# CDLinux

## 关于CDLinux

CDLinux是什么？如果在Windows上用过WinPE，那么CDLinux相当于Linux版的WinPE了。本文适合有一定的Linux基础知识读者，当前系统是Linux发行版并已经安装GRUB，Ubuntu等系统都有默认装了GRUB。没有Linux基础的参考相关链接。

## 安装GRUB引导和CDLinux

要知道自己的移动硬盘的设备，可以通过`ls -al /dev`查看，这里是`sdc`，并安装到第一个分区，需要注意CDlinux不支持Ext4格式分区

```text
sudo mkdir -p /mnt/usb
# 挂着GRUB引导分区
sudo mount /dev/sdc1 /mnt/usb
# 安装GRUB引导到sdc
sudo grub-install --target=i386-pc --debug --boot-directory=/mnt/usb/cdl_boot /dev/sdc
# 生成启动引导文件
sudo grub-mkconfig -o /mnt/usb/cdl_boot/grub/grub.cfg
```

之后将下载的CDLinux解压到第一分区,即`/mnt/usb/`目录下。

## GRUB2配置

通过以上描述方法安装的是GRUB2引导启动方式，修改启动配置`sudo vi /mnt/usb/boot/grub/grub.cfg`.  
参考`/CDlinux/cdl_boot/grub.cfg`

```text
set default=1

set fallback=0
set timeout=5

set gfxmode=640x480
insmod gfxterm
insmod vbe
insmod vga

if loadfont /cdl_boot/grub/fonts/unicode.pf2; then
  terminal_output gfxterm
  insmod png
  background_image /CDlinux/boot/splash.png
fi

#################################################################

menuentry 'CDlinux' {
  search --set -f /CDlinux/initrd
  linux /CDlinux/bzImage quiet CDL_SAFEG=yes
  initrd /CDlinux/initrd
}

menuentry 'CDlinux (zh_CN) Chinese 中国大陆' {
  search --set -f /CDlinux/initrd
  linux /CDlinux/bzImage quiet CDL_LANG=zh_CN.UTF-8 vga=788
  initrd /CDlinux/initrd
}

menuentry 'CDlinux (zh_TW) Chinese 中國臺灣' {
  search --set -f /CDlinux/initrd
  linux /CDlinux/bzImage quiet CDL_LANG=zh_TW.UTF-8 vga=788
  initrd /CDlinux/initrd
}

menuentry 'CDlinux (en_GB) English Great Britain' {
  search --set -f /CDlinux/initrd
  linux /CDlinux/bzImage quiet CDL_LANG=en_GB.UTF-8 vga=788
  initrd /CDlinux/initrd
}

menuentry 'CDlinux (en_US) English United States' {
  search --set -f /CDlinux/initrd
  linux /CDlinux/bzImage quiet CDL_LANG=en_US.UTF-8 vga=788
  initrd /CDlinux/initrd
}


if search --file /8888/8PE_MGR; then
menuentry 'Win8 PE ' {
  insmod ntldr
  search --set -f /8888/8PE_MGR
  ntldr /8888/8PE_MGR
}

fi

menuentry 'MemTest86+:  a thorough, stand alone memory tester for x86' {
  linux16 /CDlinux/boot/memtest.bin.gz
}
```

附件参数

```text
# 语言编码
CDL_LANG=zh_CN.UTF-8
# 保存文件分区
CDL_DEV=sdc1
```

## GRUB配置

如果使用的是GRUB，Windows系统采用GRUB4DOS安装的就是GRUB，与GRUB2语法不同。  
menu.lst参考

```text
default 4
fallback 0
timeout 5

find --set-root /CDlinux/bzImage
splashimage (cd)/CDlinux/boot/splash.xpm.gz

title Safe Graphics Mode
    find --set-root /CDlinux/bzImage
    kernel /CDlinux/bzImage quiet CDL_SAFEG=yes
    initrd /CDlinux/initrd
title Normal, please select a language:
    root
title >
    root

title CDlinux English
    find --set-root /CDlinux/bzImage
    kernel /CDlinux/bzImage quiet CDL_LANG=en_US.UTF-8
    initrd /CDlinux/initrd
title CDlinux Chinese
    find --set-root /CDlinux/bzImage
    kernel /CDlinux/bzImage quiet CDL_LANG=zh_CN.UTF-8
    initrd /CDlinux/initrd
title >
    root

title MemTest86+:  a thorough, stand alone memory tester for x86
    find --set-root /CDlinux/bzImage
    kernel /CDlinux/boot/memtest.bin.gz
```

## 下载地址

1. CDlinux-0.9.7.1

   [ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/CDlinux-0.9.7.1.iso](ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/CDlinux-0.9.7.1.iso)

   [https://sourceforge.net/projects/cd-linux/files/CDlinux-ISO/0.9.7.1/CDlinux-0.9.7.1.iso/download](https://sourceforge.net/projects/cd-linux/files/CDlinux-ISO/0.9.7.1/CDlinux-0.9.7.1.iso/download)

2. CDlinux-0.9.7.1S社区版

   [ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/CDlinux\_CE-0.9.7.1.iso](ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/CDlinux_CE-0.9.7.1.iso)

3. CDlinux-0.9.7.1迷你版

   [ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/CDlinux\_mini-0.9.7.1.iso](ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/CDlinux_mini-0.9.7.1.iso)

4. 内核定制下载

   [ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/extra/devel-cdl.md](ftp://distro.ibiblio.org/pub/linux/distributions/cdlinux/releases/0.9.7.1/extra/devel-cdl.md)

## 相关链接

[CDlinux HOWTOs 文档](http://cd-linux.sourceforge.net/archive/0.4/howto-cn.html) [GRUB \(简体中文\)](https://wiki.archlinux.org/index.php/GRUB_%28简体中文%29) [目前国内最完整详细的 CDlinux 硬盘安装手册](http://cdlinux.net/cdlinux-10-1-1.html)  
[CDlinux-0.9.7.1iso版下载地址](http://cdlinux.net/cdlinux-2-1-1.html)  
[终于成功从U盘启动CDlinux系统，而且能够保存设置](http://blog.sina.com.cn/s/blog_6751e16f01012d4q.html)

