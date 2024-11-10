---
description: nas 设置
---

## nas 设置

1. [下载地址](https://fw.koolcenter.com/iStoreNAS/x86_64_efi/)
2. [文档教程](https://doc.linkease.com/zh/guide/istoreos/)
3. 默认密码：`password`
4. cups 打印机地址 `http://10.10.10.11:631/printers/Pantum_P2200_series`
5. 挂载点要用uuid，不然重启后会变 `UUID: ef6909e4-45e8-4c92-9d3c-cd840ab7b8cb (/dev/sdb1, 698.62 GiB)	/hdd	auto (ext4)	defaults	是	`
6. qb enhance下载设置 `/hdd/down1` `/hdd/qb` 内网白名单 `10.10.10.12`
7. samba 路径 `/hdd` `share` 添加 `\\10.10.10.11`

## 解决 Win11 无法访问 samba：

1. 打开组策略，在“本地计算机策略 > 计算机配置 > 管理模板 > 网络 > Lanman 工作站”中启用“启用不安全的来宾登录”。
2. 打开组策略，在”本地计算机策略 > 计算机配置 > Windows 设置 > 安全设置 > 本地策略>安全选项”中禁用“Microsoft 网络客户端：对通信进行数字签名（始终）”。
3. 立即生效。