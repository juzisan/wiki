# Linux 安装

## 1. EndeavourOS

- [下载地址](https://endeavouros.com/latest-release/)安装xfce界面，更新源设置成国内，[个性化设置中文wiki](https://wiki.archlinuxcn.org/wiki/%E9%A6%96%E9%A1%B5) 中文输入法得多次重启电脑
- xfce 没有采用 wayland，所以可以 pyautogui 截屏。gly end
- 安装 office ， kate ， gitkraken ， edge ， chromium
- sudo pacman -S ， yay 安装软件
- 中文注音輸入法 `sudo pacman -S fcitx5-im fcitx5-chinese-addons  fcitx5-rime`
- 中文輸入配置。nano是比較基本的文字編輯器，簡單好上手，大家可以更換成自己習慣的文字編輯器。
  `nano /etc/environment` 在文件中加入以下內容

```bash
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
```

- 存檔後reboot就可以看到更動。 和windows的shift切換字體不同，這裡是預設為Ctrl+空白鍵更換字體。
- 什麼好看免費的字體通通都灌進來就對了。

```bash
sudo pacman -S noto-fonts-cjk wqy-microhei wqy-microhei-lite wqy-bitmapfont
sudo pacman -S wqy-zenhei ttf-arphic-ukai ttf-arphic-uming adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts
```

- 設定藍芽。因為EndeavourOS為了達到簡潔的地步，並沒有預設藍芽驅動，需要靠用戶自行下載使用。

```bash
sudo pacman -S --needed bluez bluez-utils
sudo pacman -S blueberry
```

接著需要開啟藍芽 `sudo systemctl enable bluetooth` 然後就可以在應用軟體中找到圖形化界面的藍芽程式了！

宝贵经验来源于[范剛哲的部落格](https://fgzblog.com/2022/08/安裝EndeavourOS後做的六件事)

## 2. Debian 个人电脑安装

### 1. 下载

- [linux mint](https://www.linuxmint.com/download.php)
- [edge](https://www.microsoft.com/en-us/edge/download?form=MA13RB)
  [motrix](https://motrix.app/download)

### 2. 设置

- 给账户 root 权限。`sudo xed /etc/sudoers`。
  内容 `test ALL= (ALL) ALL`
  
- 更新系统 `sudo apt-get update && sudo apt-get -y upgrade`

- 改 hosts 文件 `sudo xed /etc/hosts` [内容](https://raw.hellogithub.com/hosts)

- deb 软件包安装 `sudo dpkg -i` 后边接上软件包的名字

- 开启 openssh 

  ```bash
  # 查看运行状态:
  
  sudo systemctl status ssh
  
  # 安装命令:
  
  sudo apt-get install openssh-server
  
  # 修改端口:
  
  sudo nano /etc/ssh/sshd_config
  
  # 启用开机自启：
  
  sudo systemctl enable ssh
  
  # 启动服务：
  
  sudo systemctl start ssh
   
  
  ```

### 3. 软件安装

```bash
sudo apt-get install scrot vlc gimp okular chromium
```

- 安装截图软件 scrot ,pyautogui 能不能截图 
- snap 安装 [https://snapcraft.io/store?categories=featured](https://snapcraft.io/store?categories=featured)
- 安装 snap flatpak 命令[flatpak上海交通大学源](https://mirrors.sjtug.sjtu.edu.cn/docs/flathub)

```bash
sudo apt update
sudo apt install snapd
sudo snap install snapcraft --classic
sudo snap install snap-store

sudo snap remove vlc --purge

wget https://mirror.sjtu.edu.cn/flathub/flathub.gpg
sudo flatpak remote-modify --gpg-import=flathub.gpg flathub

sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub

```

- 星火软件商店 [https://gitee.com/spark-store-project/spark-store/releases](https://gitee.com/spark-store-project/spark-store/releases)
- 安装字体
- 在海豚中增加服务器共享 `smb://10.10.10.11/share`
- 网络视频软件 [https://github.com/Hiram-Wong/ZyPlayer/releases](https://github.com/Hiram-Wong/ZyPlayer/releases)
  
  

## 3. Debian 服务器安装

### 1. 下载安装Debian

[下载地址](https://www.debian.org/CD/http-ftp/#stable)，安装时注意选清华源，安装里选图形界面lede，软件选ssh 更新命令

`apt-get update`

`apt-get -y upgrade`

用户权限su sudo，自己用无所谓，普通用户su，有些系统命令前加sudo

笔记本盒盖不关电源 `sudo nano /etc/systemd/login.conf`

  `sudo nano /etc/systemd/logind.conf`  找到  `LidSwitch`  修改所有

重启电脑 `sudo systemctl reboot`

### 2. 用ssh和todesk管理Debian

ssh在安装时默认开启

todesk[下载](https://www.todesk.com/linux.html?lang=zh)

todesk 修复错`sudo nano /etc/sudoers` 内容 `Defaults env_keep=DISPLAY`

### 3. 安装qbittorrent

[安装地址](https://software.opensuse.org/download.html?project=home%3Anikoneko%3Atest\&package=qbittorrent-enhanced-nox-qt6)

命令 `sudo nano /etc/systemd/system/qbittorrent-nox.service`

内容

```bash
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

定时重启 `sudo crontab -e`

编辑内容 `0 6 * * * sudo systemctl restart  qbittorrent-nox`

### 4. 安装配置samba

`apt-get install -y samba` `sudo nano /etc/samba/smb.conf`

内容

```bash
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

### 5. 添加启动项

 **使用rc.local文件设置手动启动项**

`/etc/rc.local`文件允许您在系统启动时执行自定义命令。编辑方法如下：

```
sudo nano /etc/rc.local
```

在文件中添加启动命令，每行一个命令，例如：

```
#!/bin/sh -e

/home/gly/c/frpc -u
```

保存后，赋予文件执行权限：`sudo chmod +x /etc/rc.local`



### 6. 挂载硬盘

#### **5. 1 `fdisk -l` 查看硬盘的使用情况，也就是哪些硬盘没有挂载**

#### **5. 2 `df -h` 查看挂载情况**

#### **5.3  使用命名 mkfs.ext4 进行格式化，命令如下 mkfs.ext4 /dev/vdb**

#### **5.4  然后，创建挂载目录，用来㩐载数据盘，命令如下：**

```bash
mkdir /data1 #（创建目录的意思）
mount /dev/vdb /data1 #（将硬盘vdb挂到目录data1下）
df -h
```

#### **5.5  系统重启自动挂载硬盘的操作方法**

```bash
echo '/dev/vdb /data1 ext4 defaults 0 0' >> /etc/fstab #（自动挂载命令，会出现确认命令，选择y）
cat /etc/fstab #（查看自动挂载是不是生效了）
```

#### **5.6  重启系统 reboot**

***

### 7. 安装 alist

[下载地址](https://alist.nn.ci/zh/guide/install/script.html)

访问地址：<http://YOUR\_IP:5244/>

```bash
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

## 4. VmWare 安装黑苹果

## 5. istoreOS 安装

### 1 下载 istoreOS

- [下载地址](https://fw.koolcenter.com/iStoreOS/x86_64_efi/) [安装说明](https://doc.linkease.com/zh/guide/istoreos/install_x86.html)
- [rufus下载地址](https://rufus.ie/zh/) 固件下载打镜像文件只能在 win 下用 rufus 写盘
- `quickstart` 命令进行安装， root 密码是 password
- 添加硬盘，增加共享 samba

### 2. 插件

- CUPS打印服务（驱动ppi文件在deb包里，地址是ip加斜杠加打印机名字）
- 定时设置
- iStore增强
- qBittorrent下载器（配置和下载目录需要设定）

## 6. fedora 安装

### 1. fedora 下载

- [fedora 下载](https://fedoraproject.org/workstation/)
- Fedora 科学计算 LinuxOS [https://labs.fedoraproject.org/zh\_Hans\_CN/scientific/](https://labs.fedoraproject.org/zh\_Hans\_CN/scientific/)
- Fedora 中文社区 [https://zh.fedoracommunity.org/](https://zh.fedoracommunity.org/)

### 2. fedora 设置

- 换清华源  [fedora | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/fedora/)
  
  ```bash
  sudo sed -e 's|^metalink=|#metalink=|g' \
      -e 's|^#baseurl=http://download.example/pub/fedora/linux|baseurl=https://mirrors.tuna.tsinghua.edu.cn/fedora|g' \
      -i.bak \
      /etc/yum.repos.d/fedora.repo \
      /etc/yum.repos.d/fedora-updates.repo
  ```

- 更新系统 
  
  ```bash
  sudo dnf clean all && sudo dnf makecache
  sudo dnf upgrade
  ```

- 

- `sudo passwd root` 改 root 密码 

- 关闭wayland

```bash
以 root 用户身份打开 /etc/gdm/custom.conf 文件。

sudo nano /etc/gdm/custom.conf

在文件的 [daemon] 部分找到以下行：

#WaylandEnable=false
通过删除 # 字符取消对行的注释。因此，行显示：

WaylandEnable=false
重启系统：
reboot
```

- 设置 snap 和 flatpak（上海交通大学源）

```bash
sudo dnf install snapd
sudo ln -s /var/lib/snapd/snap /snap
sudo snap install snapcraft --classic

不需要安装商店 sudo snap install snap-store

sudo snap remove v4freedom --purge

wget https://mirror.sjtu.edu.cn/flathub/flathub.gpg
sudo flatpak remote-modify --gpg-import=flathub.gpg flathub

sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub
```

### 3. fedora 安装软件

1. `sudo dnf install ` 和 `sudo dnf remove `
2. `sudo dnf install scrot marker gimp okular chromium `
3. 下载 [edge](https://www.microsoft.com/en-us/edge/download?form=MA13RB) [vivaldi](https://vivaldi.com/zh-hans/)
4. [flathub](https://flathub.org/) gitkraken `flatpak install flathub com.axosoft.GitKraken`
5. `sudo snap install v4freedom`
6. [gitkraken rpm](https://www.gitkraken.com/download/linux-rpm)
7. flatpak 安装 pycharm `flatpak install flathub com.jetbrains.PyCharm-Professional`

---
