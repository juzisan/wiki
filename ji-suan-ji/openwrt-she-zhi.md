# Openwrt设置

## 软路由设置
### 网络
#### 接口
lan 10.10.10.10

lan 取消 wan 选择

dhcp 

### 刷新固件

```
dd if=/tmp/tmp/op.img of=/dev/sda 
```

|        mac        |     ip      |    备注     |
|:-----------------:|:-----------:|:---------:|
| 68:f7:28:7d:51:00 | 10.10.10.11 |    nas    |
| b4:2e:99:90:ec:ca | 10.10.10.12 |  AmdDesk  |
| 28:d2:44:f1:db:6f | 10.10.10.13 |   lx笔记本   |
| 30:3a:64:f4:c9:46 | 10.10.10.14 | lx笔记本wifi |



## 软路由端口

|     左1     |   2    |   3    |   3    |   2    |    右1     |
|:----------:|:------:|:------:|:------:|:------:|:---------:|
|    eth0    |  eth1  |  eth2  |  eth3  |  eth4  |   eth5    |
| vmnic0（管理） | vmnic1 | vmnic2 | vmnic3 | vmnic4 |  vmnic5   |
|   42(b4)   | 43(be) |   44   |   45   |   46   |    47     |
|    eth5    |  eth0  |  eth1  |  eth2  |  eth3  | eth4（wan） |

## esxi登陆

```
cdromBoot runweasel autoPartitionOSDataSize=8192
10.10.10.100
密码 Lyq-2022


exsi 升级命令 用绝对目录
显示VMware版本号
vmware -vl 
一共两条命令升级固件
esxcli software sources profile list
esxcli software profile update 


例子 esxcli software sources profile list -d /vmfs/voIumes/datastore1/VMware-ESXi-8.0U1-21495797-depot.zip 
之后显示软件包内容选项，根据软件包内容选项改下面的命令 -p 部分
esxcli software profile update  -d /vmfs/volumes/629ddc14-779d129f-c4ed-009027e51742/VMware-ESXi-8.0U1-21495797-depot.zip --profile=ESXi-8.0U1-21495797-standard --no-hardware-warning
```

## esxi控制台

```
vim /etc/config/netwwork

ip 改为 10.10.10.10
lan 改为 eth5
vim 命令
i 插入
esc 退出插入
:wq 退出保存
reboot 重启路由器
```

## 进入网页管理地址


```
LOID配置	2131537695
密码为空
改密码为 rly2020

网络
LAN 物理设置 接口全选
DHCP 静态地址
WAN 协议 PPPoE
用户名和密码 fs_ep57710920
DNS 1: 101.6.6.6
DNS 2: 94.140.14.14
DNS 3: 94.140.15.15
DNS 4: 202.96.64.68
DNS 5: 202.96.69.38


101.6.6.6,94.140.14.14,94.140.15.15,114.114.114.114,114.114.115.115,223.5.5.5,223.6.6.6,180.76.76.76,119.29.29.29,119.28.28.28,1.2.4.8,210.2.4.8,202.96.64.68,202.96.69.38

DNS 1: 2408:8000:6001:7000::8888
DNS 2: 2408:8000:6001:7000::9999
2408:8000:6001:7000::9999


服务 bypass
运行模式 智能模式（基于ChinaDNS-NG）
需要代理的端口 仅常用端口（p2p不走流量到代理）
国外DNS解析方式 使用SmartDNS DoH查询
国内DNS解析方式 使用SmartDNS DoH查询
高级 Socks5服务端（全局） 本地端口 1080

SmartDNS
基本设置 启用 服务器名称： china 本地端口 6053 自动设置Dnsmasq 自动设置为Dnsmasq的上游服务器
上游服务器 
第二组服务器 启用 本地端口 5335 服务器组 overseas

```


## 上游服务器

* 公共 DNS 域名服务器 [https://dns.iui.im/](https://dns.iui.im/)

|  DNS服务器名称  | DNS服务器IP                          | DNS服务器端口 | 协议类型  |
|:----------:|-----------------------------------|----------|-------|
|    101     | 101.6.6.6                         | default  | udp   |
|    ad1     | 94.140.14.14                      | default  | udp   |
|    ad2     | 94.140.14.15                      | default  | udp   |
|   lnlt1    | 202.96.64.68                      | default  | udp   |
|   lnlt2    | 202.96.69.38                      | default  | udp   |
|  google1   | 8.8.8.8                           | 853      | tls   |
|  google2   | 8.8.4.4                           | default  | udp   |
|  google3   | https://dns.google/dns-query      | default  | https |
|  opendns1  | https://doh.opendns.com/dns-query | default  | https |
|  opendns2  | 208.67.222.222                    | 53       | tcp   |
|  opendns3  | 208.67.222.222                    | 853      | tls   |
| cloudflare | 1.1.1.1                           | default  | udp   |
|     联通     | 2408:8000:6001:7000::8888         |          |       |
|     联通     | 2408:8000:6001:7000::9999         |          |       |
|     阿里     | 2400:3200::1                      |          |       |
|     阿里     | 2400:3200:baba::1                 |          |       |
|  OpenDNS   | 2620:0:ccc::2                     |          |       |
|  OpenDNS   | 2620:0:ccd::2                     |          |       |

## ROS 配置

* 密码 ros2021
* 10.10.10.59
* 10.10.10.13
* [ipv4设置](https://post.smzdm.com/p/ag8782mm/)
* [ipv6设置](https://post.smzdm.com/p/aqm47w6p/)

## v2rayN 设置

订阅分组 https://bulinkbulink.com/freefq/free/master/v2

## wireguard配置

```
# Allow incoming traffic to the wireguard service
/ip firewall filter add action=accept chain=input dst-port=51820 protocol=udp
```

*   网络 接口 LAN

    ipv4 地址 10.10.10.16 ipv4 网关 10.10.10.10 使用自定义的NDS服务器 10.10.10.10 101.6.6.6 94.140.14.14 94.140.15.15 dhcp 忽略此接口
* 网络 接口 添加新接口
*   wireguard VPN

    协议选 wireguard VPN 私钥 复制 监听端口 不用设置 ip地址 私有地址/32,为指定一个固定网址，/24为254网段ip地址数，是网段 公钥 复制 预共享密钥 复制 允许的ip地址 0.0.0.0/0, ::/0 路由允许的IP 选上对号 端口主机 vps远端ip地址 端点端口 复制 keep-alive 25 s 一般配置 防火墙 选wan 必须选
* 服务 bypass
* 服务端 启动服务端
* 添加 启用 服务类型 Socks5，服务器端口 1080

## 主路由添加 socks5 服务器节点

## v2ray 设置


* 服务器器端 [https://github.com/Alvin9999/new-pac/wiki](https://github.com/Alvin9999/new-pac/wiki)
* 一键多端 [一键多端](https://github.com/Alvin9999/new-pac/wiki/%E4%B8%80%E9%94%AE%E6%90%AD%E5%BB%BA%E5%A4%9A%E4%B8%AA%E5%8D%8F%E8%AE%AE%E8%8A%82%E7%82%B9%E6%95%99%E7%A8%8B)
* linux redhat 更新软件 `yum update`
* 本地 v2ray 客户端下载 [https://github.com/2dust/v2rayN/releases](https://github.com/2dust/v2rayN/releases)
* 路由器 bypass 设置
* vps 推荐 [https://www.vpsgo.com/](https://www.vpsgo.com/)
* 云端 10美元一年 [https://app.cloudcone.com/cloud](https://app.cloudcone.com/cloud) 每年8月20日付费
* 免费 vpn [https://app.zoogvpn.com/sign-in](https://app.zoogvpn.com/sign-in)
* [https://zoogvpn.com/products/vpn-for-windows/](https://zoogvpn.com/products/vpn-for-windows/)
* vps [https://my.racknerd.com/clientarea.php](https://my.racknerd.com/clientarea.php) 10美元一年，速度挺快的
* 美国地址生成器 [https://www.meiguodizhi.com/](https://www.meiguodizhi.com/)

```// Some code 
Ubuntu 16+ / Debian 8+ 系统 v2ray一键部署管理脚本（ps：如果这个脚本不好用，教程末尾还有一个八合一共存脚本）

安装命令：

source <(curl -sL https://multi.netlify.app/v2ray.sh) --zh

升级命令(保留配置文件更新)：

source <(curl -sL https://multi.netlify.app/v2ray.sh) -k

卸载命令：

source <(curl -sL https://multi.netlify.app/v2ray.sh) --remove

如果输入安装命令后提示curl: command not found，那是因为服务器系统没有自带curl命令，安装一下curl。

CentOS系统安装curl命令：yum install -y curl

Debian/Ubuntu系统安装curl命令：apt-get install -y curl

安装完成后，输入v2ray可进入管理页面。脚本来自Jrohy/multi-v2ray。


一键多端脚本安装命令：

bash <(curl -Ls https://gitlab.com/rwkgyg/sing-box-yg/raw/main/sb.sh)

安装完成后，输入sb可进入管理页面。脚本来自yonggekkk。

----------------------------------------------------------------------------------

编辑定时任务
crontab -u root -e

每小时重启一次
30 */1 * * * root init 6

每天执行一次

45 3 * * *   systemctl restart v2ray
30 3 * * 1 /sbin/reboot



0 */1 * * * systemctl restart sing-box;rc-service sing-box restart
0 */1 * * * systemctl restart --now openvpn-server@server.service
30 3 * * 1 reboot





------------------------------------------------------------------------------------
开启 bbr 加速

1、修改系统变量

echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf

2、保存生效

sysctl -p

3、查看内核是否已开启BBR

sysctl net.ipv4.tcp_available_congestion_control
显示以下即已开启：

# sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno

4、查看BBR是否启动

lsmod | grep bbr

显示以下即启动成功：

# lsmod | grep bbr
tcp_bbr                20480  14
```



## 网络测速网址

- [东北大学](https://speed.neu.edu.cn/)
- [中国科技大学](https://test.ustc.edu.cn/)
- [上海交通大学](https://mirror.sjtu.edu.cn/speedtest/)
- [上海大学](https://speedtest.shu.edu.cn/)
- [华东师范大学](https://speedtest.ecnu.edu.cn/)
- [南京大学](http://test.nju.edu.cn/)
- [南京航空航天大学](http://speed.nuaa.edu.cn/)
- [浙江大学](http://speedtest.zju.edu.cn/)
- [nperf](https://www.nperf.com/zh_CN/)
- [librespeed](https://www.librespeed.cn/) ipv6 测试
- [台湾大学](http://speed5.ntu.edu.tw/speed5/)
- [speedtest](https://www.speedtest.net/)