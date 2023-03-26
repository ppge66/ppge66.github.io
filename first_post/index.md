# 

<!-- ---
title: 'openwrt 编译记录'
date: 2023-03-26T20:46:08+08:00
draft: true
--- -->

# openwrt 编译记录

## 首先得搭一个环境

在 ubuntu-20.04 上运行命令，将环境搭建好：

```bash
#!/bin/bash
apt-get update && apt-get install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync -y
```

