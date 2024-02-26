# Linux 安装

## 1. EndeavourOS

[下载地址](https://endeavouros.com/latest-release/)安装xfce界面，更新源设置成国内，[个性化设置中文wiki](https://wiki.archlinuxcn.org/wiki/%E9%A6%96%E9%A1%B5)

## 2. Debian 个人电脑安装

- 因为 Debian 支持双拼，安装的时候选 KDE 界面。
- Debian 安装的时候断网，不然联网更新太慢了。
- 给账户 root 权限。`sudo kate /etc/sudoers`。
内容 `test ALL= (ALL) ALL`
- 改 [电子科技大学镜像](https://mirrors.ustc.edu.cn/help/debian.html)
`sudo kate /etc/apt/sources.list`
- 更新系统 `sudo apt-get update` `sudo apt-get -y upgrade`
- 改 hosts 文件 `sudo kate /etc/hosts` [内容](https://raw.hellogithub.com/hosts)
- deb 软件包安装 `sudo dpkg -i ` 后边接上软件包的名字
- deb 软件包 wps edge gitkraken
- 安装 anaconda 输入都是 yes [安装说明](https://raw.hellogithub.com/hosts) 有些之后的配置要做 [更新源](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
执行 `conda config --set show_channel_urls yes` 然后主文件下就有要改的文件了。
- 升级命令 `conda clean -i ` `conda update conda`
- gitkraken 同步仓库。pycharm 解压缩，用 sh 执行，建立快捷方式，打开仓库，项目环境添加 anaconda 环境。
- wps 复制字体 `sudo unzip fronts.zip -d /usr/share/fonts/wps-office/
`

## 3. Debian 服务器安装

### 1. 下载安装Debian

[下载地址](https://www.debian.org/CD/http-ftp/#stable)，安装时注意选清华源，安装里选图形界面lede，软件选ssh 更新命令

`apt-get update`

`apt-get -y upgrade`

用户权限su sudo，自己用无所谓，普通用户su，有些系统命令前加sudo

笔记本盒盖不关电源 `sudo nano /etc/systemd/login.conf` 找到 `LidSwitch`修改所有

### 2. 用ssh和todesk管理Debian

ssh在安装时默认开启

todesk[下载](https://www.todesk.com/linux.html?lang=zh)

todesk 修复错`sudo nano /etc/sudoers` 内容 `Defaults env_keep=DISPLAY`

### 3. 安装qbittorrent

[安装地址](https://software.opensuse.org/download.html?project=home%3Anikoneko%3Atest\&package=qbittorrent-enhanced-nox-qt6)

命令 `sudo nano /etc/systemd/system/qbittorrent-nox.service`

内容

```
[Unit]
Description=qBittorrent-nox
After=network.target

[Service]
User=root
Type=forking
RemainAfterExit=yes
ExecStart=/usr/bin/qbittorrent-nox -d

[Install]
WantedBy=multi-user.target
```

开机自启 `sudo systemctl enable qbittorrent-nox`

定时重启 `sudo crontab -e`&#x20;

编辑内容 `0 6 * * * sudo systemctl restart  qbittorrent-nox`

### 4. 安装配置samba

`apt-get install -y samba` `sudo nano /etc/samba/smb.conf`

内容

```
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

samba 共享文件夹需要开启 home 权限 `sudo chmod 777 下载 -R` 启动 samba `sudo service smb restart`

### 5. 挂载硬盘

#### **1. `fdisk -l` 查看硬盘的使用情况，也就是哪些硬盘没有挂载**

#### **2. `df -h` 查看挂载情况**

#### **3.  使用命名 mkfs.ext4 进行格式化，命令如下 mkfs.ext4 /dev/vdb**

#### **4.  然后，创建挂载目录，用来㩐载数据盘，命令如下：**

```
mkdir /data1 #（创建目录的意思）
mount /dev/vdb /data1 #（将硬盘vdb挂到目录data1下）
df -h
```

#### **5.  系统重启自动挂载硬盘的操作方法**

```
echo '/dev/vdb /data1 ext4 defaults 0 0' >> /etc/fstab #（自动挂载命令，会出现确认命令，选择y）
cat /etc/fstab #（查看自动挂载是不是生效了）
```

#### **6.  重启系统 reboot**

***

### 6. 安装 alist

[下载地址](https://alist.nn.ci/zh/guide/install/script.html)

访问地址：http://YOUR\_IP:5244/

```
配置文件路径：/opt/alist/data/config.json
---------如何获取密码？--------
先cd到alist所在目录:
cd /opt/alist
随机设置新密码:
./alist admin random
或者手动设置新密码:
./alist admin set d
\----------------------------
启动服务中
查看状态：systemctl status alist
启动服务：systemctl start alist
重启服务：systemctl restart alist
停止服务：systemctl stop alist
```
