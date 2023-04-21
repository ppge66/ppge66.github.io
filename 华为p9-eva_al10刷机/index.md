# 

<!--
 * @Author: huzi
 * @Date: 2023-04-20 17:45:02
 * @LastEditTime: 2023-04-21 18:13:44
 * @FilePath: /blog/content/posts/华为P9-EVA_AL10刷机.md
 * @Description:
-->
<!-- ---
title: '华为P9-EVA_AL10刷机'
date: 2023-04-20T20:46:08+08:00
draft: true
--- -->

# 华为 P9-EVA_AL10 刷机

## adb 常用命令

```bash
adb devices
adb push
adb pull
adb install

adb shell
adb shell su

adb reboot bootloader

adb connect ${ip地址}

# 华为冻结更新命令
adb shell pm disable-user com.huawei.android.hwouc
adb shell pm enable com.huawei.android.hwouc
```

## 刷机常用命令

```bash
fastboot flash boot boot.img
fastboot flash reboot

# lock重装上锁
fastboot oem unlock ${解锁码}

# emui5 boot.img
fastboot flash boot magisk_patched-xxx.img
# emui7、8 提取 RAMDISK.img
fastboot flash ramdisk magisk_patched-xxx.img
# emui9+ 鸿蒙 提取 RECOVERY_RAMDISK.img - 使用命令
fastboot flash recovery_ramdisk magisk_patched-xxx.img

```

## 手机工程模式

```bash
*#*#2846579#*#*
```

## 工具下载

```bash
# idm绿色版
https://www.123pan.com/s/A6cA-XD9Jh
https://423down.lanzouo.com/b0f3ahu0b
https://pan.baidu.com/s/1Xg9wvVePXgh4s1I3RLSriA?pwd=2023

# room下载
https://www.huaweirom.com

https://www.rom100.com
https://firmwarefile.com/huawei-p9-eva-al10
https://androidmtk.com/download-huawei-stock-rom-for-all-models


# 升级降级
https://github.com/ProfessorJTJ/HISuite-Proxy
# 固件搜索
https://professorjtj.github.io
```

## magisk

```bash
https://github.com/topjohnwu/Magisk
# delta面具
https://github.com/HuskyDG/magisk-files

# 模块
# lsposed
https://github.com/LSPosed/LSPosed
# Shamiko

# move certificates
# JustTrustMe
# TrustMEalready
# Inspeckage

# WebViewDebugHook
https://github.com/feix760/WebViewDebugHook

# lamda
https://github.com/rev1si0n/lamda/releases
```

