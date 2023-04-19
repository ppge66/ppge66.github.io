# 

<!--
 * @Author: huzi
 * @Date: 2023-03-26 22:51:40
 * @LastEditTime: 2023-04-19 19:58:45
 * @FilePath: /blog/content/posts/mac-u盘恢复.md
 * @Description:
-->
<!-- ---
title: 'mac上的u盘恢复'
date: 2023-03-26T20:46:08+08:00
draft: true
--- -->

# mac 上的 u 盘恢复

##

```bash
diskutil list
```

## 命令行格式化：

```bash
# uu 为u盘名称
sudo diskutil eraseDisk FAT32 uu MBRFormat /dev/disk5
```

