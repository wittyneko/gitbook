# Linux系统GRUB硬盘安装

## ubuntu

```text
title Install Ubuntu
root (hd0,4)
kernel (hd0,4)/linux/ubuntu/vmlinuz.efi boot=casper iso-scan/filename=/linux/ubuntu/ubuntu-16.04-desktop-amd64.iso ro quiet splash
initrd (hd0,4)/linux/ubuntu/initrd.lz
boot
```

## deepin

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
sudo update-grub  
sudo gedit /boot/grub/grub.cfg

