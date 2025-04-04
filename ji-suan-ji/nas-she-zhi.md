---
description: nas 设置
---
## win10 当 nas

1. [win10LTSC64bit](magnet:?xt=urn:btih:366ADAA52FB3639B17D73718DD5F9E3EE9477B40&dn=SW_DVD9_WIN_ENT_LTSC_2021_64BIT_ChnSimp_MLF_X22-84402.ISO&xl=5044211712) [win11LTSC64bit](magnet:?xt=urn:btih:b84e74c1dbcc88a02c5b24a6f84383f353a2e1dd&dn=zh-cn_windows_11_enterprise_ltsc_2024_x64_dvd_cff9cd2d.iso&xl=5287520256)
2. 开启远程协助:windows设置 ---》安全设置---》本地策略---》安全选项---》账号：使用空密码的本地帐户只允许进行控制台登录---》禁用
3. 更改注册表
```
Windows Registry Editor Version 5.00

［HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print］

“RpcAuthnLevelPrivacyEnabled”=dword:00000000
```
4. 打开 控制面板-管理工具-任务计划程序---》 创建基本任务---》输入名称、描述---》选择执行的操作，选择启动程序---》执行命令 `shutdown -r -f` 命令---》勾选，打开任务属性对话框---》选择不管用户是否登录都要运行，不选不存储密码
5. 安装 [qBittorrent-Enhanced-Edition](https://github.com/c0re100/qBittorrent-Enhanced-Edition/releases) ，设置下载位置为E盘，改 [tracker](https://cf.trackerslist.com/all.txt)
6. 电脑访问 `\\10.10.10.11`
7. win10 用 cmd 查看系启动时间 `systeminfo | find "系统启动时间"`


## 解决 Win11 无法访问 samba：

1. 打开组策略，在“本地计算机策略 > 计算机配置 > 管理模板 > 网络 > Lanman 工作站”中启用“启用不安全的来宾登录”。
2. 打开组策略，在”本地计算机策略 > 计算机配置 > Windows 设置 > 安全设置 > 本地策略>安全选项”中禁用“Microsoft 网络客户端：对通信进行数字签名（始终）”。
3. 立即生效。



## nas 设置

1. [下载地址](https://fw.koolcenter.com/iStoreNAS/x86_64_efi/)
2. [文档教程](https://doc.linkease.com/zh/guide/istoreos/)
3. 默认密码：`password`
4. cups 打印机地址 `http://10.10.10.11:631/printers/Pantum_P2200_series` 添加ppd文件 `/usr/lib/cups/filter/pt2500Filter`
5. 挂载点要用uuid，不然重启后会变 `UUID: ef6909e4-45e8-4c92-9d3c-cd840ab7b8cb (/dev/sdb1, 698.62 GiB)	/hdd	auto (ext4)	defaults	是	`，samba 添加挂载点 share 路径 `/mnt/sata2-1/`
6. qb enhance下载设置  `/mnt/sata2-1/down1` `/mnt/sata2-1/qb` nas里和qb网页设置里都设置一次 内网白名单
```text
WebUI\AuthSubnetWhitelist=10.10.10.0/24
WebUI\AuthSubnetWhitelistEnabled=true
```
7. samba 路径 `/hdd` `share` 添加 `\\10.10.10.11`
8. 安装 [passwall2](https://github.com/xiaorouji/openwrt-passwall2/releases) ，下载后上传到 nas ，安装命令 `opkg install *.ipk --force-reinstall` ，`添加socks代理 ，1081 端口`
