---
description: Windows 安装介绍
---

# Windows 安装

1. 下载 Windows 系统 [假的MSDN](https://next.itellyou.cn/Original/)  win11
   中文版 [23H2 (Jan 2024)](magnet:?xt=urn:btih:57831e3ad5e74a319c5b85f239794fca3aeb5159&dn=zh-cn_windows_11_business_editions_version_23h2_updated_jan_2024_x64_dvd_fee59269.iso&xl=6725859328)
2. 下载 [AtlasOS](https://atlasos.net/) 精简 windows 系统;
3. 准备 winpe 优选 [firpe](https://firpe.cn/page-247);
4. winpe 安装正版系统，接着安装 AtlasOS
5. 激活 windows ，[HEU_KMS_Activator](https://github.com/zbezj/HEU_KMS_Activator/releases)
6. EasyRC [https://firpe.cn/page-196](https://firpe.cn/page-196) 重装系统软件
7. Bitwarden 密码管理器 [https://vault.bitwarden.com/#/vault](https://vault.bitwarden.com/#/vault)
8. iTab 浏览器网页标签 [https://www.itab.link/install/chrome.html](https://www.itab.link/install/chrome.html)
9. 桌面增强 [itop](https://www.itopvpn.com/user-manual/ied/?name=ied&ver=2.4.0.8&lan=&insur=other&to=wc_learn#Download-&-Installation)
10. [手心输入法](https://www.xinshuru.com/index.html?p=win)
11. 单文件软件 [https://www.cmdpe.com/category-10.html](https://www.cmdpe.com/category-10.html)
12. Filecr [https://filecr.com/en/](https://filecr.com/en/) 破解软件下载
13. FreeCommander [https://freecommander.com/en/downloads-portable/](https://freecommander.com/en/downloads-portable/)
    windows 文件管理软件
14. Moba shell [https://mobaxterm.mobatek.net/](https://mobaxterm.mobatek.net/) Windows shell 窗口 moba2023
15. Office 下载 [https://otp.landian.vip/zh-cn/download.html](https://otp.landian.vip/zh-cn/download.html)
16. W 压缩软件 WinRAR [https://www.rarlab.com/download.htm](https://www.rarlab.com/download.htm)
17. http 下载软件 [IDM ](https://filecr.com/windows/internet-download-manager/?id=187919616000)
18. OCR 软件 [ABBYY FineReader](https://filecr.com/windows/finereader/?id=202552448000)
19. 显示帧率 两个软件一起工作 [CapFrameX](https://www.capframex.com/download) [RTSS](https://www.guru3d.com/download/rtss-rivatuner-statistics-server-download/)
20. 看图软件 [Honeyview](https://www.bandisoft.com/honeyview/)
21. 文本编辑器 [Kate](https://kate-editor.org/zh-cn/get-it/) [UltraEdit](https://filecr.com/windows/idm-ultra-edit-0001/?id=587332864000)
22. 视频播放器 [PotPlayer](https://potplayer.tv/?lang=zh_CN) 恒星播放器(需要自行下载破解版，用来播放特殊高清视频)
23. 视频音频照片格式转换 [File Converter](https://github.com/Tichau/FileConverter/releases)
24. 系统增强 [PowerToys](https://learn.microsoft.com/zh-cn/windows/powertoys/install) [NirLauncher](https://launcher.nirsoft.net/downloads/index.html)
25. 屏幕截图 [ShareX](https://getsharex.com/)
26. 游戏平台 [Steam](https://store.steampowered.com/about/)
27. 虚拟机 [VMWare](https://www.vmware.com/go/getworkstation-win)
28. 火狐 [firefox]()
29. 谷歌 chromium 浏览器 [chromium](https://www.chromium.org/getting-involved/dev-channel/)
30. 谷歌 chrome 浏览器 [chrome](https://www.google.com/chrome/)
31. ATI [驱动](https://www.amd.com/zh-cn/support/download/drivers.html)

## moonlight 和 sunshine

* moonlight 局域网串流客户端 [https://moonlight-stream.org/](https://moonlight-stream.org/)
* moonlight GitHub [https://github.com/moonlight-stream/moonlight-qt](https://github.com/moonlight-stream/moonlight-qt)
* sunshine 局域网串流服务 [https://github.com/LizardByte/Sunshine/releases](https://github.com/LizardByte/Sunshine/releases)
* sunshine 文档 [https://docs.lizardbyte.dev/projects/sunshine/en/latest/about/overview.html](https://docs.lizardbyte.dev/projects/sunshine/en/latest/about/overview.html)
* sunshine 默认管理网址 [https://localhost:47990/](https://localhost:47990/)


## 设置

两步解决Windows11 24H2 专业版无法访问局域网共享：
1. 打开组策略，在“本地计算机策略 > 计算机配置 > 管理模板 > 网络 > Lanman 工作站”中启用“启用不安全的来宾登录”。
2. 打开组策略，在”本地计算机策略 > 计算机配置 > Windows 设置 > 安全设置 > 本地策略>安全选项”中禁用“Microsoft 网络客户端：对通信进行数字签名（始终）”。
立即生效。