# 小米路由器3G (Mi Wifi Router 3G/MIR3G/MI3G)刷机教程
## 硬件资源
CPU: MediaTek MT7621A (880 MHz, 2 cores)  
FLASH: 128 MiB  
RAM: 256 MiB  
USB: 1 (usb3.0)  
WI1 chip1: MediaTek MT7603EN (2x2:2)  
WI2 chip1: MediaTek MT7612EN (2x2:2)  
LAN: 2x 10/100/1000  
WAN: 1x10/100/1000  

## 小米路由器3G 从官方开发板ROM刷OpenWrt

- 1.路由器新买或未使用过（已正常联网使用跳至步骤4），用网线将路由器WAN口连接至光猫LAN口，然后给路由器通电。

- 2.待路由器前面板LED灯蓝色常量时，电脑连接路由器WiFi(如：Xiaomi_xxxx或Xiaomi_xxxx_5G)。

- 3.浏览器输入 http://miwifi.com，并按向导设置路由器（WiFi密码和路由器密码），并确保路由器能正常上网。

- 4.准备一个U盘，并格式化为FAT或FAT32格式。

- 5.小米官网 http://www1.miwifi.com/miwifi_download.html 下载路由器3G开发板ROM(miwifi_r3g_firmware_c2175_2.25.122.bin)，保存至电脑桌面。

- 6.小米官网 https://d.miwifi.com/rom/ssh 下载SSH授权文件(miwifi_ssh.bin)保存至U盘，下载页面含有SSH的用户名root和密码。

- 7.Putty官网 https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html 下载SSH客服端程序(putty.exe)保存至电脑桌面。

- 8.OpenWrt官网 https://downloads.openwrt.org/releases/18.06.1/targets/ramips/mt7621/ 下载内核(mir3g-squashfs-kernel1.bin)和根文件系统(mir3g-squashfs-rootfs0.bin)保存至U盘。

- 9.浏览器输入 http://miwifi.com，填入路由器密码进行登陆。

- 10.进入路由器固件更新的界面，点击“手动更新”，从电脑桌面选择路由器开发板ROM(miwifi_r3g_firmware_c2175_2.25.122.bin)，执行刷写操作（刷写过程中不能断电！！！直至路由器前面板LED灯蓝色常量）。

- 11.断开路由器电源，将U盘插入路由器USB口(含miwifi_ssh.bin文件)，按住路由器reset，重新接通路由器电源，直到路由器前面板LED灯黄色闪烁即可松开reset。

- 12.运行桌面putty.exe程序，“Host Name”输入路由器地址192.168.31.1，“Port”输入22，点击下方“Open”。若提示输入用户名则输入步骤6页面中的用户名root和密码，否则重复步骤11。

- 13.SSH成功登陆后，执行下列命令：
    cd /extdisks/sda1  
    mtd write lede-ramips-mt7621-mir3g-squashfs-kernel1.bin kernel1  
    mtd write lede-ramips-mt7621-mir3g-squashfs-rootfs0.bin rootfs0  
    nvram set flag_try_sys1_failed=1  
    nvram commit  
    reboot  

- 14.路由器重启至前面板LED灯蓝色常量，网线连接电脑和路由器LAN口，浏览器输入192.168.1.1，显示登陆界面表示小米路由器3G刷写OpenWrt成功，你可以为所欲为了 ~ ^o^

  参考地址：https://forum.openwrt.org/t/xiaomi-wifi-router-3g/5377

## 小米路由器3G 从OpenWrt刷回官方稳定版/开发板ROM
  该方法适用于路由器从OpenWrt正常或异常（LED亮红色）状态刷回官方ROM。（以下以官方开发板ROM为例）
### 情况一：路由器运行OpenWrt正常
- 1.下载官方开发板ROM（miwifi_r3g_firmware_c2175_2.25.122.bin）保存至格式化FAT或FAT32的U盘，并重命名为miwifi.bin

- 2.U盘插入路由器USB，SSH登陆192.168.1.1执行命令：
  fw_setenv flag_try_sys2_failed 1  
  reboot  
  
- 3.LED变为红色闪烁，按下reset，保持1~2秒，LED变为LED显示黄色（5分钟左右不能断电重启）。

- 4.等待直至LED变为蓝色，即刷回官方ROM成功（此时路由器地址为192.168.31.1）。

### 情况二：路由器运行OpenWrt异常
- 1.下载官方开发板ROM（miwifi_r3g_firmware_c2175_2.25.122.bin）保存至格式化FAT或FAT32的U盘，并重命名为miwifi.bin

- 2.断开路由器电源，U盘插入路由器USB。

- 3.按住路由器reset，并重启接通电源，直至LED黄色闪烁再松开reset。

- 4.等待直至LED变为蓝色，即刷回官方ROM成功（此时路由器地址为192.168.31.1）。
