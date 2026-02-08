---
description: nas 设置
---



## Fedora 服务器当 nas

### 安装 Fedora
1. 下载地址 [https://fedoraproject.org/server/download/](https://fedoraproject.org/server/download/)
2. 安装的时候没什么特殊的
3. 远程登陆 https://10.10.10.13:9090/ https://10.10.10.11:9090/
4. 安装更新 
5. 设置日志文件为2天 `sudo journalctl --vacuum-time=2d`
6. 列出已安装的 linux 内核 `rpm -qa kernel`
### 安装 smb 服务
1. 安装 smb `sudo dnf install samba samba-client`
2. 安装完成后，启动 SMB 和 NMB 服务，并设置为开机自动启动：`sudo systemctl enable --now smb nmb`
3. 配置防火墙: 
``` bash
   sudo firewall-cmd --permanent --add-service=samba &&   sudo firewall-cmd --reload
```

4. 将该用户添加到 Samba 用户数据库：`sudo smbpasswd -a gly`

5. 创建目录：

   ```bash
   sudo mkdir -p /home/{back,m,q,p}  && sudo chown -R gly:gly /home/{back,m,q,p}  && sudo chmod -R 755 /home/{back,m,q,p}
   ```
6. 编辑 Samba 主配置文件 /etc/samba/smb.conf：`sudo nano /etc/samba/smb.conf`
7. 增加配置，重启 smb 服务：`sudo systemctl restart smb nmb`


```text
# See smb.conf.example for a more detailed config file or
# read the smb.conf manpage.
# Run 'testparm' to verify the config is correct after
# you modified it.
#
# Note:
# SMB1 is disabled by default. This means clients without support for SMB2 or
# SMB3 are no longer able to connect to smbd (by default).

[global]
        workgroup = SAMBA
        security = user

        passdb backend = tdbsam

        printing = cups
        printcap name = cups
        load printers = yes
        cups options = raw

        # Install samba-usershares package for support
        include = /etc/samba/usershares.conf

#[homes]
#        comment = Home Directories
#        valid users = %S, %D%w%S
#        browseable = No
#        read only = No
#        inherit acls = Yes

[printers]
        comment = All Printers
        path = /var/tmp
        printable = Yes
        create mask = 0600
        browseable = No

[print$]
        comment = Printer Drivers
        path = /var/lib/samba/drivers
        # printadmin is a local group
        write list = printadmin root
        force group = printadmin
        create mask = 0664
        directory mask = 0775

[back]

        comment = My Fedora Share
        path = /home/back
        browseable = yes
        writable = yes


[M]

        comment = My Fedora Share
        path = /home/m
        browseable = yes
        writable = yes

[Q]

        comment = My Fedora Share
        path = /home/q
        browseable = yes
        writable = yes

[P]

        comment = My Fedora Share
        path = /home/p
        browseable = yes
        writable = yes



```

8. 之前的配置
  ```text
    # Global parameters
    [global]
            workgroup = WORKGROUP
            dns proxy = No
            map to guest = Bad User
            netbios name = SAMBASERVER
            security = USER
            server string = Samba Server %v
            idmap config * : backend = tdb
            guest account = nobody
            guest ok = yes
    
    [1_share]
            comment = this is debian
            path = /home/gly/下载/
            read only = No
            browseable = yes
            public = yes
            writeable = yes
     [2_share]
            comment = this is debian
            path = /jxyp/下载/
            read only = No
            browseable = yes
            public = yes
            writeable = yes
  ```

9. 改正权限：

    ```bash
    sudo setsebool -P samba_export_all_ro on && sudo setsebool -P samba_export_all_rw on && sudo setsebool -P samba_enable_home_dirs on
    ```
    
    

10. 重启 smb 服务：`sudo systemctl restart smb nmb`
### 安装 qbittorent
1. 安装 qbittorent `sudo dnf install qbittorrent-nox -y`

2. 创建服务 `sudo nano /etc/systemd/system/qbittorrent-nox.service`

    ```text
    [Unit]
    Description=qBittorrent Daemon Service
    After=network.target
    
    [Service]
    # 如果你不想创建专用用户，可以将下面的 user/group 改为 root
    User=gly
    Group=gly
    Type=forking
    # -d 表示后台运行
    ExecStart=/usr/bin/qbittorrent-nox -d
    Restart=on-failure
    
    [Install]
    WantedBy=multi-user.target
    
    ```

3. 启动并设置开机自启：`sudo systemctl daemon-reload && sudo systemctl enable --now qbittorrent-nox`

4. 配置防火墙:

    ```bash
    sudo firewall-cmd --permanent --add-port=8080/tcp
    
    sudo firewall-cmd --permanent --add-port=6881/tcp
    sudo firewall-cmd --permanent --add-port=6881/udp
    
    sudo firewall-cmd --reload
    
    ```

    

5. 配置 qbittorent  `sudo nano /home/gly/.config/qBittorrent/qBittorrent.conf`

    ```text
    [Preferences]
    WebUI\AuthSubnetWhitelist=10.10.10.0/24
    WebUI\AuthSubnetWhitelistEnabled=true
    
    ```

6. | 功能     | 命令                                     |
    | -------- | ---------------------------------------- |
    | 查看状态 | `sudo systemctl status qbittorrent-nox`  |
    | 查看日志 | `sudo journalctl -u qbittorrent-nox -f`  |
    | 重启服务 | `sudo systemctl restart qbittorrent-nox` |
    | 停止服务 | `sudo systemctl stop qbittorrent-nox`    |

### 安装打印机

1. 安装 cups 服务

2. 改权限，改监听

3. 驱动选 通用的pcl驱动

4. 无论网页测试是否正确，当添加网络打印机的时候，本地电脑添加的驱动正确就好了,本地驱动解压缩安装程序，选P2500.inf。复制以下粘贴到添加打印机里面。`http://10.10.10.11:631/printers/Pantum_P2200_series`

   

## win10ltsc2019 当 nas

1. [win10ltsc2019](ed2k://|file|cn_windows_10_enterprise_ltsc_2019_x64_dvd_2efc9ac2.iso|4027760640|4B1C7640C3A280F205A0BCFFF65472FC|/)
   迅雷链接 ed2k 的资源。
2. [ntlite](https://www.puresys.net/%e7%b3%bb%e7%bb%9f%e5%b7%a5%e5%85%b7) 修改安装镜像。导入注册表，别的无所谓。

    ```text
    Windows Registry Editor Version 5.00
    
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]
    
    "updateRDStatus"=dword:00000001
    "AllowRemoteRPC"=dword:00000000
    "fDenyTSConnections"=dword:00000000
    
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp]
    
    "UserAuthentication"=dword:00000000
    
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa]
    
    "LimitBlankPasswordUse"=dword:00000000
```

3. [easyrc](https://firpe.cn/page-196) 安装修改后的镜像。高级都选上，账号写我常用的管理员。

4. 启动后就可以远程连接上了。共享文件夹：back ，p ，q ，m 。

5. 组策略，用户权限分配：“拒绝从网络访问这台计算机”中删除 Guest 用户。

> [!CAUTION]
>
> cpu 占用率高的解决办法：没启动的时候用 Dism 删除拼音输入法。禁止系统更新。

## win10 当 nas 系统设置和软件安装

1. 之前通过注入注册表开启远程协助，如果进系统用这个办法:**windows设置** ---》**安全设置**---》**本地策略**---》**安全选项
   **---》**账号：使用空密码的本地账户只允许进行控制台登录**---》**禁用**

2. 打开**控制面板**，**凭据管理器**，**添加windows凭据**，输入直连打印机电脑的**IP**，**用户名：guest ，密码为空**。点击确定。

3. 更改注册表，解决打印机问题。

    ```text
    Windows Registry Editor Version 5.00    
    
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print]
    
    "RpcAuthnLevelPrivacyEnabled" = dword:00000000
    
    [HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\Printers\PointAndPrint]
    
    "RestrictDriverInstallationToAdministrators" = dword:00000000
    
    [HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\AppXSvc]
    "Start"=dword:00000004
    
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ClipSVC]
    "Start"=dword:00000004
    
```

4. 打开 **控制面板**-**管理工具**-**任务计划程序**---》 **创建基本任务**---》**输入名称、描述**---》**选择执行的操作，选择启动程序
   **---》执行命令 `shutdown -r -f` 命令---》勾选，打开任务属性对话框---》选择不管用户是否登录都要运行，不选不存储密码

5. 安装 [qBittorrent-Enhanced-Edition](https://github.com/c0re100/qBittorrent-Enhanced-Edition/releases) ，设置下载位置为q盘，改 [tracker](https://cf.trackerslist.com/all.txt)

6. 电脑访问 `\\10.10.10.11`

7. win10 用 cmd 查看系启动时间 `systeminfo | find "系统启动时间"`

8. 按下 win+r 在框中输入`shell:Startup` 就会出现添加快捷方式到启动目录
   * 步骤一：需要先激活自动登录选项，方法是修改注册表，依次展开
   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\PasswordLess\Device`
   将 `DevicePasswordLessBuildVersion` 的值改为 0，并点击【确定】按钮。重启计算机。
   * 步骤二：按下 win+r 在框中输入 `netplwiz` 指令
   在弹出的窗口中选择要自动登录的用户，然后取消勾选“要使用本计算机，用户必须输入用户名和密码”
   在弹出的窗口中输入上一步对应的用户名和密码，单击【确定】按钮。
   单击重新启动，自动登录设置完成。

9. 按下 Win + R 键打开运行窗口；

   * 输入 eventvwr.msc 并回车，启动事件查看器；
   * 在左侧导航栏依次展开：Windows日志 → 系统；
   * 在右侧点击“筛选当前日志”；
   * 在弹出窗口中输入事件ID：6005,6006；
   * 点击“确定”，即可看到与系统开关机相关的事件列表。
   
   | 事件ID | 描述                     |
   |------|------------------------|
   | 6005 | 表示事件日志服务已启动，通常发生在系统开机时 |
   | 6006 | 表示事件日志服务已停止，通常发生在系统关机时 |

10. 关机和重启

    ```cmd
    shutdown -p
    ```
    
    ```cmd
    shutdown -r -t 0
    ```

11. 磁盘自动整理：碎片整理软件 [O&O Defrag Professional]((https://filecr.com/windows/oo-defrag/))。
12. 内网穿透：` `  [ChmlFrp Panel v3](https://panel.chmlfrp.cn/sign)  设置通道，绑定域名，域名解析到给出来地址，域名得用全新的域名。协议选http。

## 解决 Win11 无法访问 samba：

1. 打开组策略，在“本地计算机策略 > 计算机配置 > 管理模板 > 网络 > Lanman 工作站”中启用“启用不安全的来宾登录”。
2. 打开组策略，在”本地计算机策略 > 计算机配置 > Windows 设置 > 安全设置 > 本地策略>安全选项”中禁用“Microsoft
   网络客户端：对通信进行数字签名（始终）”。
3. 立即生效。

## nas 设置

1. [下载地址](https://fw.koolcenter.com/iStoreNAS/x86_64_efi/)

2. [文档教程](https://doc.linkease.com/zh/guide/istoreos/)

3. 默认密码：`password`

4. cups 打印机地址 `http://10.10.10.11:631/printers/Pantum_P2200_series` 添加ppd文件 `/usr/lib/cups/filter/pt2500Filter`

5. 挂载点要用uuid，不然重启后会变
   `UUID: ef6909e4-45e8-4c92-9d3c-cd840ab7b8cb (/dev/sdb1, 698.62 GiB)    /hdd    auto (ext4)    defaults    是    `
   ，samba 添加挂载点 share 路径 `/mnt/sata2-1/`

6. qb enhance下载设置  `/mnt/sata2-1/down1` `/mnt/sata2-1/qb` nas里和qb网页设置里都设置一次 内网白名单

   ```text
   WebUI\AuthSubnetWhitelist=10.10.10.0/24
   WebUI\AuthSubnetWhitelistEnabled=true
   ```

7. samba 路径 `/hdd` `share` 添加 `\\10.10.10.11`

8. 安装 [passwall2](https://github.com/xiaorouji/openwrt-passwall2/releases) ，下载后上传到 nas ，安装命令
   `opkg install *.ipk --force-reinstall` ，`添加socks代理 ，1081 端口`

## qBittorrent备份还原

备份：

```cmd
@echo off
echo Copy file...
md D:\back\qBittorrent\1
md D:\back\qBittorrent\2
xcopy /e /y C:\Users\gly\AppData\Local\qBittorrent\ D:\back\qBittorrent\1
xcopy /e /y C:\Users\gly\AppData\Roaming\qBittorrent\ D:\back\qBittorrent\2
echo File copy successfully.
echo Press Any Key Exit!
pause >nul
exit

```

还原：

```cmd
@echo off
echo Copy file...
xcopy /e /y D:\back\qBittorrent\1 C:\Users\gly\AppData\Local\qBittorrent\ 
xcopy /e /y D:\back\qBittorrent\2 C:\Users\gly\AppData\Roaming\qBittorrent\
echo File copy successfully.
echo Press Any Key Exit!
pause >nul
exit

```

