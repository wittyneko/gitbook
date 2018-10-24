# Linux系统安装

## UEFI启动管理

```bash
# 修复启动引导，--efi-directory指定efi安装目录，--boot-directory指定efi分区目录
sudo grub-install /dev/sda --efi-directory=/mnt/boot/efi --boot-directory=/mnt/boot
# 查看启动项
efibootmgr
# 添加启动项：-c创建，-L名称，-d磁盘，-p分区号，-l有效的efi启动文件
efibootmgr -c -w -L "BootOptionName" -d /dev/sda -p 1 -l /EFI/Boot/bootx64.efi
# 删除启动项
efibootmgr -B -b 编号
# 禁用启动项
efibootmgr -A -b 编号
# 启用启动项
efibootmgr -a -b 编号
# 修改顺序编号x在y前
efibootmgr -o x,y
```

[用efibootmgr管理UEFI启动项，添加丢失的启动项](https://blog.csdn.net/Pipcie/article/details/79971337)  
[Ubuntu 16.04引导错误修复- EFI - Linux公社](http://www.linuxidc.com/Linux/2016-09/135486.htm)  
[在linux环境中利用efibootmgr管理efi启动项](https://kelvin.mbioq.com/using-efibootmgr-to-manage-efi-startup-items-in-an-linux-environment.html)

## Windows的Linux子系统

[Windows10内置Linux子系统初体验](https://www.jianshu.com/p/bc38ed12da1d)  
[Windows10安装Linux子系统Ubuntu](https://blog.csdn.net/zhouzme/article/details/78780479)

## GRUB安装ubuntu

```text
title Install Ubuntu
root (hd0,4)
kernel (hd0,4)/linux/ubuntu/vmlinuz.efi boot=casper iso-scan/filename=/linux/ubuntu/ubuntu-16.04-desktop-amd64.iso ro quiet splash
initrd (hd0,4)/linux/ubuntu/initrd.lz
boot
```

## GRUB安装deepin

```text
title install  deepin-15
find --set-root /deepin.iso
kernel /vmlinuz  findiso=/deepin.iso  noprompt quiet splash  boot=live ro deepin-installer/locale=zh_CN.UTF-8 keyboard-configuration/layoutcode=us keyboard-configuration/variantcode= --  rootflags=sync auto-deepin-installer
initrd /initrd.lz
boot
```

GRUB2

```text
if  search --file /bootiso/deepin-15-alpha2-amd64.iso; then
menuentry "install deepin-15-alpha2-amd64.iso" {
set isofile="/bootiso/deepin-15-alpha2-amd64.iso"
search --set  -f $isofile
loopback loop $isofile
linux (loop)/live/vmlinuz.efi  boot=live union=overlay username=user quiet  live-config noprompt noeject findiso=$isofile locales=zh_CN.UTF-8
initrd (loop)/live/initrd.lz
}
fi

----------

set root=(hd0,msdos6)  #按自己的情况改
set isofile="/deepin-15-alpha2-amd64.iso"
search --set  -f $isofile
loopback loop $isofile
linux (loop)/live/vmlinuz.efi  boot=live union=overlay username=user quiet  live-config findiso=$isofile locales=zh_CN.UTF-8
initrd (loop)/live/initrd.lz
boot
```

[其它linux发行版完美运行deepin上的wine软件包\(ubuntu QQ也完美\)](http://blog.csdn.net/xuelongqy/article/details/51258754)

## ubuntu更新grub2

[修改ubuntu下grub2系统启动项](http://blog.chinaunix.net/uid-26438352-id-3418184.html)  
**Grub 2结构** Grub 2包含下面几个部分：  
/boot/grub/grub.cfg 文件  
/etc/grub.d/ 文件夹  
/etc/default/grub 文件  
sudo gedit /etc/default/grub  
sudo update-grub2

