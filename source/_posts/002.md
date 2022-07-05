---
title: 在任意Linux发行版安装pacman软件包管理器
date: 2022-01-06 10:52:31
tags:
---

# 在任意的Linux发行版使用pacman软件包管理器
---

##### 作为Arch~~母亲~~的忠实用户，你是否为其他的Linux发行版没有pacman感到烦恼
#### 用优秀的[灵格丁](https://github.com/lingrottin)先生写的[pacman-installer](https://github.com/LGY07/pacman-installer)脚本！


dnf用户可以使用`$sudo dnf install pacman`来安装，但是需要更改`/etc/pacman.conf`的配置文件，改变根目录,需要更改的部分：
```
RootDir     = /你希望用来安装软件的目录/
DBPath      = /你希望用来安装软件的目录/var/lib/pacman/
CacheDir    = /你希望用来安装软件的目录/var/cache/pacman/pkg/
LogFile     = /你希望用来安装软件的目录/var/log/pacman.log
```
然后创建目录，确保以上目录存在：
```
$sudo mkdir /你希望用来安装软件的目录/
$sudo mkdir /你希望用来安装软件的目录/var/
$sudo mkdir /你希望用来安装软件的目录/var/lib/
$sudo mkdir /你希望用来安装软件的目录/var/lib/pacman/
$sudo mkdir /你希望用来安装软件的目录/var/cache/
$sudo mkdir /你希望用来安装软件的目录/var/cache/pacman/
$sudo mkdir /你希望用来安装软件的目录/var/cache/pacman/
$sudo mkdir /你希望用来安装软件的目录/var/log/
```

<br/>

如果是其他用户，请使用[pacman-installer](https://github.com/LGY07/pacman-installer)安装脚本,你可以按照READEME的标准安装方式，也可以使用以下命令快捷安装：

wget下载器：
```
$su - -c 'bash <(wget -O- https://github.com/LGY07/pacman-installer/raw/main/pacman-installer.sh)'
```
curl下载器：
```
$su - -c 'bash <(curl https://github.com/LGY07/pacman-installer/raw/main/pacman-installer.sh)'
```