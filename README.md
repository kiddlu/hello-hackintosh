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
    WiFi/BT Combo: Broadcom 94360 / 94352
    Graphics：AMD Radeon HD 7750/5770(PCI-E)
    Displays：Dell P2416D/HP E241i

显卡不推荐N卡，我出过莫名其妙的冻瓶问题，而且网上几乎说几乎无解。<br>1080p的屏幕，推荐用HD7750，免驱，HiDPI能打到超过屏幕分辨录。2K屏幕用HD5770，毕竟Mac Pro原配。<br>WiFi网卡我买的是TP-LINK TL-WDN4800，免驱，直接用。WiFi USB dongle则是腾讯全民WiFi，便宜，以备不时之需。<br>Bluetooth dongle是胜为UDC324。<br>Combo芯片推荐MacBook上那几款原装，需要去淘宝一个Mini PCIe到PCIe的转接板。<br>
至于主板，CPU，内存，HDD，SSD这些，选通用的就行，一般不会出什么问题。<br>手头上没有的，可以去 http://www.tonymacx86.com/ 上看看2013和2014年的Buyer's Guide，硬件不要太新，否则10.9.5 drive不动。


##Windows
我的Hackintosh，是在Windows已经安装好之后的，再安装MacOS的双系统电脑。So，Windows下有几个工具很重要，一个叫ddmac，另外一个叫transmac，transmac的试用期是15天，应该够用吧？我暂时没有找到好的替代工具。

##Boot
Hackintosh的引导跟普通的Mac是不同的，一般来说可选的引导也就Clover和Chameleon，我自己一般用MBR，从Windows的Boot Configuration Data(BCD)引导到Chameleon，Chameleon再拉起MacOS。

我的BCD配置

	Windows Boot Manager
	--------------------
	identifier              {bootmgr}
	device                  partition=C:
	description             Windows Boot Manager
	locale                  zh-CN
	inherit                 {globalsettings}
	default                 {default}
	resumeobject            {db68b149-55b2-11e6-abde-de4757fa2150}
	displayorder            {current}
							{default}
	toolsdisplayorder       {memdiag}
	timeout                 1
	
	Windows Boot Loader
	-------------------
	identifier              {current}
	device                  boot
	path                    \windows\system32\winload.exe
	description             Windows 7 Ultimate x64
	locale                  zh-CN
	inherit                 {bootloadersettings}
	recoverysequence        {e78c39b7-55b2-11e6-abde-de4757fa2150}
	recoveryenabled         Yes
	osdevice                boot
	systemroot              \windows
	resumeobject            {db68b149-55b2-11e6-abde-de4757fa2150}
	nx                      OptIn
	detecthal               Yes
	
	Real-mode Boot Sector
	---------------------
	identifier              {default}
	device                  boot
	path                    \Avldr.bin
	description             MacOS X 10.9.5

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

##Driver
到了这里其实已经可以省心了，去下载一个MultiBeast-Mavericks-Edition-6.5.1，就包含了常用到的声卡和有线网卡驱动，安装上就行。不过我一般用蓝牙和WiFi，所以，上面那几个东西驱动好了，这些也无所谓。<br>[Softpedia](http://mac.softpedia.com/get/System-Utilities/MultiBeast.shtml#download)

##Snapshot

![](https://github.com/kiddlu/hello-hackintosh/raw/master/res/01.png)

![](https://github.com/kiddlu/hello-hackintosh/raw/master/res/02.png)

##End
到此为止，基本上已经是一台体验不错的Hackintosh了。我的操作系统软件环境布置，可以直接去 https://github.com/kiddlu/posix 下找mac的一键部署脚本。

##Links:
###AMD Graphics:

https://www.tonymacx86.com/threads/radeon-compatibility-guide-ati-amd-graphics-cards.171291/

https://www.tonymacx86.com/threads/amd-radeon-hd-7xxx-graphics-support-in-os-x-10-8-3.93318/

https://www.tonymacx86.com/threads/list-of-confirmed-radeon-hd-7xxx-series-10-8-3.92952/

http://www.vendev.ru/ven/1002/dev

http://developer.amd.com/resources/ati-catalyst-pc-vendor-id-1002-li/
