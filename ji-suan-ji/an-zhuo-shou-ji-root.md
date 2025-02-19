# 安卓手机root


## 刷第三方rom
- 电脑软件：搞机工具箱， reiboot 
- 小米5安装 [lineageos](https://wiki.lineageos.org/devices/gemini/install/#installing-lineageos-from-recovery) [lineageos旧版本](https://lineageosroms.com/gemini/)
- 废弃 小米手机 [安装twrp](https://twrp.me/xiaomi/xiaomimi5.html)
- 手机root[小米手机安装magisk](https://magiskcn.com/mi-boot.html) 重命名apk为zip，twrp安装apk。
- [隐藏Magisk自身应用](https://magiskcn.com/hide-the-magisk-app.html)
- 下载[LSPosed](https://magiskcn.com/lsposed-install.html) 在其中搜索隐藏开发者模式和隐藏程序
- [隐藏应用列表安装教程](https://magiskcn.com/hide-my-applist-install.html) 黑名单选想要模拟的软件
- 小米5rom [lineageos](https://download.lineageos.org/devices/gemini/builds)
- 小米5rom [官方rom](https://roms.miuier.com/zh-cn/devices/gemini)

-----------------------------------------

## 模拟定位软件
- [爱思助手](https://www.i4.cn/pro_android.html)

----------------------------------------
## 详细解释

- [lineageos 安装说明](https://wiki.lineageos.org/devices/gemini/install/)


 
lineageos 刷机用 sideload   

Read through the instructions at least once before actually following them, so as to avoid any problems due to any missed steps!  
Make sure your computer has adb and fastboot. Setup instructions can be found here.  
Enable USB debugging on your device.  
Boot your device with the stock OS at least once and check every functionality.  


Warning: Make sure that you can send and receive SMS and place and receive calls (also via WiFi and LTE, if available), otherwise it won’t work on LineageOS either! Additionally, some devices require that VoLTE/VoWiFi be utilized once on stock to provision IMS.
Remove all Google accounts from your device to avoid “Factory reset protection”
LineageOS is provided as-is with no warranty. While we attempt to verify everything works you are installing this at your own risk!

Create a Mi account on Xiaomi’s website. Beware that one account can only unlock four unique devices every year (one HyperOS device, three MIUI devices), and even then only once every 30 days.
Add a phone number to your Mi account.
Insert a SIM into your phone.
Enable developer options in Settings > About Phone by repeatedly tapping MIUI Version.
Link the device to your Mi account in Settings > Additional settings > Developer options > Mi Unlock status.
Download the Mi Unlock app (or v7.6.727.43).
Ensure that your device has the appropriate drivers installed by running driver_install.exe (for 32-bit) or driver_install_64.exe (for 64-bit), which are included with Mi Unlock, otherwise, the Mi Unlock app may not detect your device.
Run the Mi Unlock app and follow the instructions provided by the app. The app may tell you that you have to wait up to 30 days. If it does so, please wait for the quoted amount of time before continuing to the next step! It is ideal to start this step at midnight (GMT+8), as Xiaomi only allows a limited number of devices to be unlocked each day.
After the device and Mi account are successfully verified, the bootloader should be unlocked.
Since the device resets completely, you will need to re-enable USB debugging to continue.



Download Lineage Recovery. Simply download the latest recovery file, named recovery.img.
warning
Important: Other recoveries may not work for installation or updates. We strongly recommend to use the one linked above!
Connect your device to your PC via USB if it isn’t already.
If your device isn’t already in fastboot mode, on the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:

`adb -d reboot bootloader`

You can also boot into fastboot mode via a key combination:

With the device powered off, hold` Volume Down + Power`. Keep holding both buttons until the word “FASTBOOT” appears on the screen, then release.
Once the device is in fastboot mode, verify your PC finds it by typing:

`fastboot devices`

If you don’t get any output or an error:

on Windows: make sure the device appears in the device manager without a triangle. Try other drivers until the command above works!
on Linux or macOS: If you see no permissions fastboot try running fastboot as root. When the output is empty, check your USB cable (preferably use a USB Type-A 2.0 one or a USB hub) and port!
check
Tip: Some devices have buggy USB support while in bootloader mode, if you see fastboot hanging with no output when using commands such as fastboot getvar ..., fastboot boot ..., fastboot flash ... you may want to try a different USB port (preferably a USB Type-A 2.0 one) or a USB hub.
Flash recovery onto your device:
fastboot flash recovery recovery.img
Now reboot into recovery to verify the installation. Do not reboot into the existing OS, since it will overwrite the recovery you just installed!
With the device powered off, hold Volume Up + Power. Keep holding both buttons until the “MI” logo appears on the screen, then release.

info_outline
Note: If you can’t power down the device, try long-pressing the key-combination (if any was used in the instructions above) until the device reboots and follow the instructions above
info_outline
Note: If your recovery does not show the LineageOS logo  , you accidentally booted into the wrong recovery. Please start at the top of this section!



Download the LineageOS zip file that you would like to install or build the package yourself.
If you are not in recovery, reboot into recovery:
With the device powered off, hold `Volume Up + Power`. Keep holding both buttons until the “MI” logo appears on the screen, then release.
Now tap Factory Reset, then Format data / factory reset and continue with the formatting process. This will remove encryption and delete all files stored in the internal storage, as well as format your cache partition (if you have one).
Return to the main menu.
Sideload the LineageOS .zip package but do not reboot before you read/followed the rest of the instructions!
On the device, select “`Apply Update`”, then “`Apply from ADB`” to begin sideload.
On the host machine, sideload the package using: `adb -d sideload `filename.zip.
check
Tip: Normally, adb will report Total xfer: 1.00x, but in some cases, even if the process succeeds the output will stop at 47% and report adb: failed to read command: Success. In some cases it will report adb: failed to read command: No error or adb: failed to read command: Undefined error: 0 which is also fine.



Click Apply Update, then Apply from ADB, then `adb -d sideload `filename.zip for all desired packages in sequence.
When presented with a screen that says Signature verification failed, click Yes. It is expected as add-ons aren’t signed with LineageOS’s official key!
 



-------------------------------------------------------------------------


TWRP Install (Requires TWRP 2.8.4 or higher already installed):
Download the latest TWRP image file (.img) from the download link and boot TWRP. Go to install and find and select the Images... button. Browse to the image that you downloaded and select it. Choose recovery and swipe to flash.

Fastboot Install Method (No Root Required):
You will need the platform-tools from the Android SDK on your computer. Download the platform-tools as per your operating system.

Windows users will need proper drivers installed on their computer. You can try the simple FWUL adb/fastboot ISO or the Naked ADB drivers or the Universal ADB drivers if you don't already have a working driver installed

On your device, go into Settings -> About and find the Build Number and tap on it 7 times to enable developer settings. Press back and go into Developer Options and enable USB debugging. From your computer, open a command prompt and type:

`adb reboot bootloader`

You should now be in fastboot mode.

Download the correct image file and copy the file into the same folder as your platform-tools. Rename the image to twrp.img and type:

`fastboot flash recovery twrp.img`

`fastboot reboot`

Note many devices will replace your custom recovery automatically during first boot. To prevent this, use Google to find the proper key combo to enter recovery. After typing fastboot reboot, hold the key combo and boot to TWRP. Once TWRP is booted, TWRP will patch the stock ROM to prevent the stock ROM from replacing TWRP. If you don't follow this step, you will have to repeat the install.

----------------------------------------------------------------


说明:
如果想刷第三方ROM，或者无法使用MIUI内置卡刷功能的受限版本，唯一的办法就是通过安装第三方恢复来刷机。
其中TWRP是最常用的第三方恢复，官方适配了很多机型，也有很多民间的改装版本。
如果是发布了一段时间以上的机型，一般用正式版就可以了。如果是新机，很可能官方还没有适配，只能用第三方版本。
正式版和第三方版的区别在于，前者不用担心安全问题，可以稳定获得更新，而后者需要自行判断作者的可信度。第三方版本通常会移除MIUI来开始验证。正式版需要手动解决这个问题(通过刷入Magisk)，否则Kami可能无法进入系统。  
最后，对于A/B分区的手机，由于后续更新系统会切换分区，TWRP安装可能会丢失。不建议为该型号安装TWRP。相反，只有在需要时才启动它(参见下面步骤4中的说明)。
下载第三方Recovery:
第三方恢复也分为TWRP官方和私人版本，其中一些在这个网站即可搜索下载，并不断更新。
TWRP 刷入步骤
1.首先将手机与电脑连接安装驱动程序(如果安装失败，可以下载MiFlash，然后手动安装)。另外，确保手机已经完成BL解锁。


2.计算机下载快速启动工具(解压后备用)和相应的模型TWRP(。img后缀文件，并将其放入之前解压缩的文件夹中)。


3.关闭手机，按住开机键+音量减小键进入快速开机模式，连接电脑。


4.电脑打开刚刚解压好的platform-tools文件夹，按住Shift键，同时在文件夹的空白处点击右键，在右键菜单中点击“在此打开Powershell窗口”。运行以下命令在TWRP刷(自己替换文件名)。

fastboot flash recovery twrp-3.4.0-0-davinci.img

注意:如果你不想安装TWRP，但只是暂时使用TWRP，运行以下命令(自己替换文件名)并忽略第5步。

fastboot boot twrp-3.4.0-0-davinci.img

如果你在运行命令后不能启动TWRP，你会一直停留在引导界面。也许TWRP版本改编有问题。可以尝试使用第三方版本。


5.为了防止MIUI用官方恢复自动更换手机，按住手机音量键，同时电脑运行以下命令重启手机，直到进入TWRP界面

fastboot reboot

6.进入TWRP后，你会被问到“你想保持系统分区只读吗”。滑动此处按钮允许修改，否则无法禁止MIUI改回官方恢复。

7.由于MIUI会在启动时检查系统分区的完整性，TWRP在最后一步修改了系统分区。此时重启手机会导致系统无法启动(“卡米”问题)。你需要通过刷入Magisk来移除引导验证。步骤如下。


下载电脑Magisk安装包，复制到手机上(此时电脑可以识别手机的MTP设备)；
在TWRP界面点击“安装”，找到下载的Magisk安装包，点击文件名，滑动按钮刷进去；
等待Magisk刷入，点击“重启系统”。这时候就不会出现“LOGO”问题，重启手机TWRP安装也不会丢失；
通过TWRP安装Magisk的图示

由于安装了Magisk，在启动系统后，您会看到一个Magisk管理器软件。是Magisk图形管理软件，自带Root功能，还可以通过安装功能模块扩展更多的玩法。


--------------------------------------------------------------

