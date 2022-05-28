---
title: 使用脚本安装ArchLinux(不一定成功)
date: 2022-01-08 10:55:15
tags:
---

# ArchLinux安装教程（不完全是）
---

![Linux的选择.png](https://huashijituan.coding.net/p/liuzhierzhong/d/liuzhierzhong/git/raw/pages/Linux.png?download=false)

学习ArchLinux`找不到教程，看不懂官方文档，嫌麻烦`是很大的问题

为了帮助便捷地安装ArchLinux，我写了一个[交互式安装脚本](https://github.com/LGY07/arch-install)(~~祸害~~)

优势在于可以通过以下几步快速的完成ArchLinux的安装（已经有别的安装脚本，但是个人认为比正常安装还麻烦

### 1.下载镜像
[清华大学镜像站](https://mirrors.tuna.tsinghua.edu.cn/archlinux/iso/latest/)
### 2.烧录镜像
可以使用[Rufus](https://rufus.ie/zh/)烧录（一定要FAT32而不是NTFS）

或者直接打开镜像，把里面的文件全部复制到一个格式为FAT32的U盘里
### 3.重启电脑进入镜像
（混完3个步骤的字数了
## 4.下载安装脚本
```
curl -O https://huashijituan.coding.net/p/liuzhierzhong/d/liuzhierzhong/git/raw/master/install.sh
```
~~这可能是最困难的步骤，需要视力以及打字速度，但是好在它不需要更改~~
## 5.运行脚本
```
bash ./install.sh
```
在脚本中，需要进行的步骤：

### 分区：使用cfdisk分区，选择gpt

使用⬆⬇键选择位置，选择空闲的空间

使用⬅➡键选择对当前位置的操作，选择New创建分区

输入引导分区大小为1G（可以很小，~~100M也行~~，但是不推荐）

输入根目录分区大小最好在10G以上（~~也许2G也行，足以体现ArchLinux的轻量~~）

选择Write，输入yes，选择Quit退出

### 选择分区

输入刚才的根目录分区位置(例如sdaX，Nvme盘为nvme0n1pX)

输入引导分区位置

### 选择内核

默认linux-zen

### 选择桌面环境

默认KDE Plasma

### 选择文本编辑器

默认Vim

### 选择AUR助手

默认Yay

### 接下来会自动pacstrap安装系统

完成后提示输入用户名，设置你的用户名，不要有空格

设置用户的密码，输入两次，不会显示出来，甚至输入后没变化，是正常现象（下同）

设置root的密码

## 完成安装

显示FINISH，10秒后自动重启

<br/>