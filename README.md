# Hello Hackintosh

----
##System
一般人都是选兼容硬件，然后跟着Apple升级系统。
不过我个人不喜欢Apple现在的UI和系统稳定性，所以，我把系统版本锁死在了10.9.5。然后根据系统去挑兼容硬件。

    System Version:	OS X 10.9.5 (13F34)
    Kernel Version:	Darwin 13.4.0

##Hardware
比较困难的是网卡和显卡驱动，尽量挑选同芯片型号的产品，可能需要自己改PID，VID等。

    WiFi：Atheros AR9380(PCI-E), MTK MT7601(USB)
    Bluetooth：Broadcom 20702(USB)
    Graphics：AMD Radeon HD 7750/5770(PCI-E)
    Displays：Dell P2416D/P2414H

显卡不推荐N卡，我出过莫名其妙的冻瓶问题，而且网上几乎说几乎无解。<br>HD7750强烈推荐"铭影2GD5 900/4500MHZ 2G/128BIT", 2K以下的显示器随便carry，而且不需要外部供电，免驱，HiDPI能打到最高分辨录。<br>WiFi网卡我买的是TP-LINK TL-WDN4800，免驱，直接用。WiFi USB dongle则是腾讯全民WiFi，便宜，以备不时之需。<br>Bluetooth dongle是胜为UDC324。<br>显示器HP的也可以。<br>
至于主板，CPU，内存，HDD，SSD这些，选通用的就行，一般不会出什么问题。<br>手头上没有的，可以去http://www.tonymacx86.com/上看看2013和2014年的Buyer's Guide，硬件不要太新，否则10.9.5 drive不动。

##Boot
Hackintosh的引导跟普通的Mac是不同的，一般来说可选的引导也就Clover和Chameleon，我自己一般用MBR，从Windows的Boot Configuration Data(BCD)引导到Chameleon，Chameleon再拉起MacOS。

我的BCD配置

我的Chameleon配置

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	<plist version="1.0">
	<dict>
	    <key>Default Partition</key>
	    <string>hd(0,9)</string>
	    <key>GUI</key>
	    <string>No</string>
	    <key>Quiet Boot</key>
	    <string>Yes</string>
	    <key>Timeout</key>
	    <string>2</string>
    	<key>DSDT</key>
       	<string>dsdt.aml</string>
       	<key>EthernetBuiltIn</key>
       	<string>Yes</string>
       	<key>DropSSDT</key>
       	<string>Yes</string>
       	<key>GenerateCStates</key>
       	<string>Yes</string>
       	<key>GeneratePStates</key>
       	<string>Yes</string>
       	<key>Kernel</key>
       	<string>mach_kernel</string>
       	<key>Kernel Flags</key>
       	<string>npci=0x2000 darkwake=0 dart=0</string>
       	<key>USBBusFix</key>
       	<string>Yes</string>
	</dict>
	</plist>