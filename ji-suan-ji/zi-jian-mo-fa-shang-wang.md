---
description: 每年10美元魔法上网，懂原理就很简单了。不限客户端，windows，安卓，Linux都可以。
---

# 自建魔法上网
-------------------------------------

## 先点开读一下[理论](https://github.com/Alvin9999/new-pac/wiki)知识

-------------------------------------

## 具体操作步骤
1. [vps优惠推荐](https://www.vpsgo.com/racknerd-coupons.html)，推荐[vps服务器racknerd](https://www.racknerd.com/) 这个一年10美元,选流量大的，美国的，安装Ubuntu系统，之后用root账号的密码登录ssh软件。Ubuntu更新命令需要su权限，`apt-get update && apt-get upgrade`。安装 Debian 13 也行。注意防火墙是不是关闭。

2. [mobaxterm](https://filecr.com/windows/mobaxterm/) 推荐的ssh登录软件，记住本地密码，忘记后没办法找回保存的密码。这个下载地址，魔法加速的速度比直接快，bt则无所谓。

3. 1. [v2ray服务器安装脚本](https://github.com/yonggekkk/sing-box-yg) 安装后，会显示链接，复制，保存，导入。

   2. 端口代理和全局魔法 [v2rayN客户端](https://github.com/2dust/v2rayN)

4. 1. [openvpn服务器安装脚本](https://github.com/Nyr/openvpn-install) 在左边目录下可见配置文件，扩展名是ovpn，下载到本地。

   2. 全局魔法 [openvpn客户端](https://openvpn.net/client/)

5. 1. [wireguard服务器安装脚本](https://github.com/Nyr/wireguard-install) 在左边目录下可见配置文件，扩展名是conf，下载到本地，一次安装也许不行，就卸载了再安装。

   2. 全局魔法  [wireguard客户端](https://www.wireguard.com/install/)

6. 优选v2ray，其次openvpn和wireguard

7. [浏览器切换代理插件SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega/releases/tag/v2.5.20) 下载安装到谷歌内核浏览器。

8. 服务器服务定时重启

```crontab
# 编辑定时服务

crontab -u root -e

# 每2小时重启服务，每天3:30重启服务器

0 */2 * * * systemctl restart sing-box;rc-service sing-box restart
10 */2 * * * systemctl restart --now openvpn-server@server.service
20 */2 * * * systemctl restart wg-quick@wg0.service
30 3 * * * reboot

0 1 * * * systemctl restart sing-box;rc-service sing-box restart


# 查看服务运行时间

ps -eo pid,lstart,etime,cmd | grep 'sing-box'

ps -eo pid,lstart,etime,cmd | grep 'openvpn'

ps -eo pid,lstart,etime,cmd | grep 'wg'

```

## apk 翻墙软件
1.  [小火箭](https://rocketapp666.github.io/)
2.  [v4freedom](https://v4freedom.com/) 
3.  [v2rayNG](https://github.com/2dust/v2rayNG)



##  电脑端另类vpn

[Cloudflare WARP](https://developers.cloudflare.com/warp-client/get-started/windows/) 必须在梯子的情况下连接，等连接上就可以退了梯子了，好奇怪的啊。
