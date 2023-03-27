# 

<!--
 * @Author: huzi
 * @Date: 2023-03-26 22:51:40
 * @LastEditTime: 2023-03-28 00:10:52
 * @FilePath: /blog/content/posts/openwrt编译.md
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

### 添加自定义源

```bash
cat >> feeds.conf.default <<EOF
src-git kenzo https://github.com/kenzok8/openwrt-packages
src-git small https://github.com/kenzok8/small
src-git OpenClash https://github.com/vernesong/OpenClash.git
EOF
```

或

```
sed -i '$a src-git kenzo https://github.com/kenzok8/openwrt-packages' feeds.conf.default
sed -i '$a src-git small https://github.com/kenzok8/small' feeds.conf.default
sed -i '$a src-git OpenClash https://github.com/vernesong/OpenClash.git' feeds.conf.default
```

### 更新源/安装源

```
./scripts/feeds update -a && ./scripts/feeds install -a
```

### 配置环境环境 .config

```bash
make menuconfig
#  M  表示选中插件但不编译进固件
# （）不选择
#  *  选中并编译

Target System (x86)  --->   目标系统（x86）
Subtarget (x86_64)  --->   子目标（x86_64）
Target Profile (Generic)  --->目标配置文件（通用）
Target Images  ---> 保存目标镜像的格式
Global build settings  --->      全局构建设置
Advanced configuration options (for developers)  ---- 高级配置选项（适用于开发人员）
Build the OpenWrt Image Builder 构建OpenWrt图像生成器
Build the OpenWrt SDK  构建OpenWrt SDK
Package the OpenWrt-based Toolchain 打包基于OpenWrt的工具链
Image configuration  --->图像配置
Base system  --->     基本系统
Administration  --->     管理
Boot Loaders  ---> 引导加载程序
Development  --->   开发
Extra packages  --->  额外包
Firmware  --->固件
Fonts  --->字体
Kernel modules  --->  内核模块
Languages  --->语言
Libraries  --->  图书馆
LuCI  --->      LuCI
Mail  ---> 邮件
Multimedia  --->多媒体
Network  --->网络
Sound  ---> 声音
Utilities  --->实用程序
Xorg  --->Xorg
```

```bash
## 选择系统(以 x86_64 为例)
Target System -> x86
Subtarget -> x86_64

## 选择固件的文件系统
## https://openwrt.org/docs/techref/filesystems
Target Images -> squashfs

## 选择构建X86_X64的GRUB固件
Target Images -> Build GRUB images (Linux x86 or x86_64 host only)

## 选择更小的压缩格式固件，方便复制
Target Images -> GZip images

## 修改软件包可用空间，默认安装会占用100M左右，建议修改扩大，为后续安装其他软件打基础
Target Images -> Root filesystem partition size

## 添加web界面(y键选择n键排除)
LuCI > Collections -> Luci

## 添加兼容性依赖
LuCI > Modules -> luci-compat

## 添加中文
LuCI > Modules -> Translations -> Chinese Simplified

## 添加openclash
LuCI > Applications -> luci-app-openclash

## 添加主题
LuCI -> Themes

## 添加wget
Nerwork -> File Transfer -> wget-nossl
Nerwork -> File Transfer -> wget-ssl

## 添加kmod-tun，TUN模式必须
Kernel modules -> Network Support -> kmod-tun

## 排除dnsmasq，由于默认会安装dnsmasq-full，这里需要排除dnsmasq，否则会冲突报错。
Base system -> dnsmasq

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

## pve 导入镜像

```bash
## 转换成 PVE 磁盘格式，注意其中的112替换为你的VM ID
./img2kvm openwrt-x86-64-generic-squashfs-combined.img 112 vm-112-disk-1
```

