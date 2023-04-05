# 

<!--
 * @Author: huzi
 * @Date: 2023-04-05 17:42:49
 * @LastEditTime: 2023-04-05 18:32:26
 * @FilePath: /blog/content/posts/google-one.md
 * @Description:
-->
<!-- ---
title: 'google one 连接记录'
date: 2023-04-5T20:46:08+08:00
draft: true
--- -->

# google one 连接记录

## openclash 设置

### 插件设置

关闭 quic：插件设置-流量控制-禁用 quic 勾去掉
关闭 UDP 流量转发

### 覆写设置

```code
# 此条必须的，连接认证，地区检查
- DOMAIN-SUFFIX,cloud.cupronickel.goog,🇺🇲 美国节点
```

```code
# 此处自行删减
- DOMAIN-SUFFIX,scone-pa.googleapis.com,🇺🇲 美国节点
- DOMAIN-SUFFIX,quake-pa.googleapis.com,🇺🇲 美国节点
- DOMAIN-SUFFIX,phosphor-pa.googleapis.com,🇺🇲 美国节点
- DOMAIN-SUFFIX,subscriptionsmanagement-pa.googleapis.com,🇺🇲 美国节点
- DOMAIN-SUFFIX,subscriptionsmobile-pa.googleapis.com,🇺🇲 美国节点
- DOMAIN-SUFFIX,federatedml-pa.googleapis.com,🇺🇲 美国节点
```

```code
# 创建隧道用
- DOMAIN-SUFFIX,na.b.g-tun.com,🇺🇲 美国节点
```

```code
# 1g流量时验证
- DOMAIN-SUFFIX,userlocation.googleapis.com,🇺🇲 美国节点


# 下面好像也是
- DOMAIN-SUFFIX,connectivitycheck.gstatic.com,🇺🇲 美国节点
- DOMAIN-KEYWORD,subscriptions,🇺🇲 美国节点
- DOMAIN-SUFFIX,clientservices.googleapis,🇺🇲 美国节点
- DOMAIN-SUFFIX,firebaseremoteconfig.googleapis.com,🇺🇲 美国节点
```

```code
script:
   shortcuts:
     google_vpn: match_provider('google_vpn') and dst_port == 443 and network == 'udp'
```

```code
rules:
  - SCRIPT,google_vpn,🎯 全球直连
```

DNS 设置

```code
# Fake-IP-Filter

# google one
na.b.g-tun.com
# +.g-tun.com  #ios连接必须要
```

### 新建规则集文件

配置管理-规则集文件列表-新建文件- google_vpn.yaml

```code
payload:
  - '136.22.64.0/24'
  - '136.22.65.0/24'
  - '136.22.67.0/24'
  - '136.22.76.0/24'
  - '136.22.83.0/24'
  - '136.22.85.0/24'
  - '136.22.86.0/24'
  - '136.22.87.0/24'
  - '136.22.92.0/24'
  - '136.22.93.0/24'
  - '136.22.94.0/24'
  - '136.22.95.0/24'
  - '136.22.96.0/24'
  - '136.22.97.0/24'
  - '136.22.98.0/24'
  - '136.22.99.0/24'
  - '136.22.100.0/24'
  - '136.22.101.0/24'
  - '136.22.102.0/24'
  - '136.22.103.0/24'
  - '136.22.104.0/24'
  - '136.22.105.0/24'
  - '136.22.106.0/24'
  - '136.22.107.0/24'
  - '136.22.108.0/24'
  - '136.22.109.0/24'
  - '136.22.110.0/24'
  - '136.23.1.0/24'
  - '136.23.2.0/24'
  - '136.23.3.0/24'
  - '136.23.4.0/24'
  - '136.23.5.0/24'
  - '136.23.6.0/24'
  - '136.23.7.0/24'
  - '136.23.8.0/24'
  - '136.23.9.0/24'
  - '136.23.10.0/24'
  - '136.23.11.0/24'
  - '136.23.12.0/24'
  - '136.23.13.0/24'
  - '136.23.14.0/24'
  - '136.23.15.0/24'
  - '136.23.16.0/24'
  - '136.23.17.0/24'
  - '136.23.18.0/24'
  - '136.23.19.0/24'
  - '136.23.20.0/24'
  - '136.23.21.0/24'
  - '136.23.22.0/24'
  - '136.23.23.0/24'
  - '136.23.24.0/24'
  - '136.23.25.0/24'
  - '136.23.26.0/24'
  - '136.23.27.0/24'
  - '136.23.28.0/24'
  - '136.23.29.0/24'
  - '136.23.30.0/24'
  - '136.23.31.0/24'
  - '136.23.32.0/24'
  - '136.23.33.0/24'
  - '136.23.34.0/24'
  - '136.23.35.0/24'
  - '209.107.176.0/24'
  - '209.107.177.0/24'
  - '209.107.178.0/24'
  - '209.107.179.0/24'
  - '209.107.180.0/24'
  - '209.107.181.0/24'
  - '209.107.182.0/24'
  - '209.107.183.0/24'
  - '209.107.184.0/24'
  - '209.107.185.0/24'
  - '209.107.186.0/24'
  - '209.107.187.0/24'
  - '209.107.188.0/24'
  - '209.107.189.0/24'
  - '209.107.190.0/24'
  - '209.107.191.0/24'
```

### 自定义规则集附加

规则附加 - 自定义规则集附加 - 添加

```
rule-providers:
   google_vpn:
    type: file
    behavior: ipcidr
    path: ./rule_provider/google_vpn.yaml
```

