---
title: 在NVMe硬盘安装ArchLinux+Windows11
date: 2021-12-19 10:40:13
tags:
---

# 如何安装ArchLinux和Windows11在NVMe硬盘：
---

（第一次写博客，可能很烂（

##### 本文主要解决以下问题：

`1.ArchLinux无法识别较新的NVMe（我的是金士顿A2000）`

`2.os-prober无法识别Windows11`

##### 需要准备：

`一台正常装有Windows11的电脑`

`一个耐用的U盘（最好是移动硬盘，也可以是热插拔的SATA盘），以下简称“U盘1”`

`一个烧录了ArchLive的U盘，以下简称“U盘2”`

`一个烧录了wepe的U盘，以下简称“U盘3”`[WePE-下载](https://www.wepe.com.cn/download.html)

~~`一个没有坏掉的大脑（（（`~~

## ——ArchLinux在NVMe如何安装：

进入U盘2的Arch Live，并插上U盘1

在U盘1上安装Arch，更改以下步骤：
```
pacstrap /mnt base linux-zen linux-firmware
```
进入chroot环境后，安装arch安装脚本：
```
pacman -S arch-install-scritps
```
不必安装图形界面，重启后fdisk -l，就能看到NVMe硬盘了

按照在SATA盘安装Arch的步骤，在NVMe盘安装ArchLinux，引导分区使用Windows11的ESP分区（建议先把ESP分区删了，重新创建，因为它太小了）

重启后，就可以进入ArchLinux了（好耶！

## ——Grub2引导ArchLinux和Windows11：
（上面的ArchLinux请使用Grub2引导

进入U盘3的wepe

打开dism++（启动时的东西都不用管）

选择Windows11

点击“工具箱”，点击引导修复，选择ArchLinux的引导分区

修复完成后重启系统，会正常进入Windows11，但是并没有破坏掉Grub2，启动按F12（我的是F12，请自己看主板说明，或者F*全部按一遍）进入引导菜单，找到ArchLinux（具体的名称是你安装Grub2时设置的）
```
#grub-install --target=x86_64 --efi-directory=/boot --bootloader-
id=ArchLinux

#pacman -S vim

#vim /etc/grub.d/40_custom
```
编辑40_custom脚本：
```
### BEGIN /etc/grub.d/40_custom_proxy ###

menuentry "Windows11"  {

insmod part_gpt

insmod fat

insmod chain

root=uuid= 【引导分区的文件系统UUID】

search --no-floppy --fs-uuid --set=root 【引导分区的文件系统UUID】 --hint-
bios=hd0,gpt0 --hint-efi=hd0,gpt0 --hint-baremetal=NVMe0,gpt0
【Windows11的系统分区文件系统UUID】

chainloader /EFI/Microsoft/Boot/bootmgfw.efi

}

### END /etc/grub.d/40_custom_proxy ###
```
确保你的Windows11位于硬盘第一个分区（/dev/NVMe0n1p1）

如果不是，请将上面的两个hd0改为hd*，/dev/NVMe0n1pX


*应为X-1
```
#grub-makecfg -o /boot/grub/grub.cfg
```
（如果你之前装的grub配置文件为”grub.conf”，请将以上命令的”grub.cfg”改为”grub.conf”）

##### 引导部分可以自己看看ArchWiki：
[GRUB (简体中文) - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%A4%9A%E7%B3%BB%E7%BB%9F%E5%90%AF%E5%8A%A8)