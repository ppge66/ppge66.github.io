# 

<!--
 * @Author: huzi
 * @Date: 2023-03-26 22:51:40
 * @LastEditTime: 2023-03-27 00:42:09
 * @FilePath: /hugo/blog/content/posts/first_post.md
 * @Description:
-->
<!-- ---
title: 'openwrt 编译记录'
date: 2023-03-26T20:46:08+08:00
draft: true
--- -->

# openwrt 编译记录

## 编译

### 首先得搭一个环境

在 ubuntu-20.04 上运行命令，将环境搭建好：

```bash
apt-get update && apt-get install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync -y
```

### 新建用户

```
adduser openwrt
usermod -a -G sudo openwrt
su openwrt
```

```
./scripts/feeds update -a && ./scripts/feeds install -a
```

### 添加自定义源

```
cat >> feeds.conf.default <<EOF
src-git kenzo https://github.com/kenzok8/openwrt-packages
src-git small https://github.com/kenzok8/small
EOF
或
sed -i '$a src-git kenzo https://github.com/kenzok8/openwrt-packages' feeds.conf.default
sed -i '$a src-git small https://github.com/kenzok8/small' feeds.conf.default
```

### 配置环境环境 .config

```bash
make menuconfig
#  M  表示选中插件但不编译进固件
# （）不选择
#  *  选中并编译
```

### 导出.config 用于云端编译

./scripts/diffconfig.sh > yun.config

### 下载 dl 库（国内请尽量全局科学上网），8 线程，如需看详细日志加 V=s

`make download -j8`

## 其它命令

```bash
# 多线程编译
make -j $(($(nproc)+1)) || make -j1 || make -j1 V=s

# 仅清理编译结果（bin 目录）
make clean

# 清理所有编译文件（除了.config、dl 文件夹和 feeds 以外都清理）
make dirclean

# 清理所有编译文件以及相关依赖（完全清理干净，一键回到刚 git clone 下来的时候）
make distclean

# 更改配置编译
rm -rf ./tmp && rm -rf .config
make menuconfig
make -j$(($(nproc) + 1)) V=s
```

### 更改 LAN 口的默认 IP 地址

```bash
vim package/base-files/files/bin/config_generate
```

### 单独编译插件

```bash
git clone https://github.com/rosywrt/luci-theme-rosy.git
```

## pve 导入镜像

```bash
./img2kvm openwrt-x86-64-generic-squashfs-combined.img 112 vm-112-disk-1
```

