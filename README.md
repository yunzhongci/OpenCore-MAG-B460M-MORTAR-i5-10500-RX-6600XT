# OpenCore-MAG-B460M-MORTAR-i5-10500-RX-5700XT
微星B460M 迫击炮 ，i5-10400，蓝宝石RX 5700XT 8G 完美黑苹果。

⚠️ 如果使用我的配置，请自行替换三码。

### 更新
- 2024/03/30，基于OpenCore 0.9.0，macOS Sonoma 14.4.1
- 2024/05/14，基于OpenCore 1.0.0，macOS Sonoma 14.5
- 2024/09/09，更换显卡为蓝宝石RX 5700XT 8G白金版。之前的显卡RX580 4G的配置文件归档，不再更新


### 硬件配置

|  配置|  型号|
|---|---|
|  CPU| I5 10500 |
|  主板| 微星B460M MORTAR |
|  内存|  16G x4 |
|  板载网卡|  RTL8125B|
|  网卡+蓝牙|  博通943602CS|
|  显卡|  核显UHD630+RX 5700XT|

### Works
- 睡眠
- 独显+核显
- 音频
- WIFI
- 蓝牙
- DP+HDMI
- 隔空投送+接力
- USB定制
### 已知问题
暂无

### BIOS 设置
- 安全启动：关闭
- USB设备从S3/S4/S5唤醒：允许
- PS/2鼠标从S3/S4/S5唤醒：允许
- USB键盘从S3/S4/S5唤醒：任意键
- 集成显卡多显示器：允许（否则核显硬件解码失效，只使用核显的可以忽略）
- OC -> CPU 特征 -> Intel 虚拟化技术：允许
- OC -> CPU 特征 -> Intel VT-D 技术：禁止
- OC -> CPU 特征 -> CFG锁定：禁止

### 使用的SSDT

- SSDT-AWAC
- SSDT-EC-USBX-DESKTOP
- SSDT-GPRW
- SSDT-MSI-B460M-Devices
- SSDT-PLUG
- SSDT-PM
- SSDT-RX5700XT
- SSDT-SBUS
SSDT-RX5700XT是一个实验性的自定义 SSDT，用于增强AMD RX 5700 XT显卡的性能

### DeviceProperties
#### PciRoot(0x0)/Pci(0x2,0x0)
Intel UHD Graphics 630 

| **Key**                  | **Type** |   **Value**  |
|--------------------------|:--------:|:------------:|
| AAPL,ig-platform-id      |   Data   | ``07009B3E`` |
| device-id                |   Data   | ``9B3E0000`` |
| enable-metal             |   Data   | ``01000000`` |
| disable-agdc             	|   Data   	|        ``01000000``       	|
| enable-hdmi-dividers-fix 	|   Data   	|        ``01000000``       	|
| enable-hdmi20            	|   Data   	|        ``01000000``       	|
| framebuffer-con0-busid  	|   Data   	|        ``02000000``       	|
| framebuffer-con0-enable    	|   Data   	|        ``01000000``       	|
| framebuffer-con0-flags  	|   Data   	|        ``C7030000``       	|
| framebuffer-con0-index    	|   Data   	|        ``02000000``       	|
| framebuffer-con0-pipe  	|   Data   	|        ``0A000000``       	|
| framebuffer-con0-type    	|   Data   	|        ``00080000``       	|
| framebuffer-con1-busid  	|   Data   	|        ``04000000``       	|
| framebuffer-con1-enable    	|   Data   	|        ``01000000``       	|
| framebuffer-con1-flags  	|   Data   	|        ``C7030000``       	|
| framebuffer-con1-index    	|   Data   	|        ``03000000``       	|
| framebuffer-con1-pipe  	|   Data   	|        ``08000000``       	|
| framebuffer-con1-type    	|   Data   	|        ``00080000``       	|
| framebuffer-con2-busid  	|   Data   	|        ``01000000``       	|
| framebuffer-con2-enable    	|   Data   	|        ``01000000``       	|
| framebuffer-con2-flags  	|   Data   	|        ``C7030000``       	|
| framebuffer-con2-index    	|   Data   	|        ``01000000``       	|
| framebuffer-con2-pipe  	|   Data   	|        ``09000000``       	|
| framebuffer-con2-type    	|   Data   	|        ``00080000``       	|
| framebuffer-patch-enable 	|   Data   	|        ``01000000``       	|
| framebuffer-stolenmem    	|   Data   	|        ``00003001``       	|
| rps-control              	|   Data   	|        ``01000000``       	|
| hda-gfx                 	|   String   	|        ``onboard-1``       	|
| model                   	|   String   	|        ``Intel UHD Graphics 630``       	|
| igfxfw                   |   Data   | ``02000000`` |

想将上述条目复制并粘贴为.plist数据

```xml
<key>PciRoot(0x0)/Pci(0x2,0x0)</key>
<dict>
	<key>AAPL,ig-platform-id</key>
	<data>BwCbPg==</data>
	<key>device-id</key>
	<data>mz4AAA==</data>
	<key>disable-agdc</key>
	<data>AQAAAA==</data>
	<key>enable-hdmi-dividers-fix</key>
	<data>AQAAAA==</data>
	<key>enable-hdmi20</key>
	<data>AQAAAA==</data>
	<key>enable-metal</key>
	<data>AQAAAA==</data>
	<key>framebuffer-con0-busid</key>
	<data>AgAAAA==</data>
	<key>framebuffer-con0-enable</key>
	<data>AQAAAA==</data>
	<key>framebuffer-con0-flags</key>
	<data>xwMAAA==</data>
	<key>framebuffer-con0-index</key>
	<data>AgAAAA==</data>
	<key>framebuffer-con0-pipe</key>
	<data>CgAAAA==</data>
	<key>framebuffer-con0-type</key>
	<data>AAgAAA==</data>
	<key>framebuffer-con1-busid</key>
	<data>BAAAAA==</data>
	<key>framebuffer-con1-enable</key>
	<data>AQAAAA==</data>
	<key>framebuffer-con1-flags</key>
	<data>xwMAAA==</data>
	<key>framebuffer-con1-index</key>
	<data>AwAAAA==</data>
	<key>framebuffer-con1-pipe</key>
	<data>CAAAAA==</data>
	<key>framebuffer-con1-type</key>
	<data>AAgAAA==</data>
	<key>framebuffer-con2-busid</key>
	<data>AQAAAA==</data>
	<key>framebuffer-con2-enable</key>
	<data>AQAAAA==</data>
	<key>framebuffer-con2-flags</key>
	<data>xwMAAA==</data>
	<key>framebuffer-con2-index</key>
	<data>AQAAAA==</data>
	<key>framebuffer-con2-pipe</key>
	<data>CQAAAA==</data>
	<key>framebuffer-con2-type</key>
	<data>AAgAAA==</data>
	<key>framebuffer-patch-enable</key>
	<data>AQAAAA==</data>
	<key>framebuffer-stolenmem</key>
	<data>AAAwAQ==</data>
	<key>hda-gfx</key>
	<string>onboard-1</string>
	<key>igfxfw</key>
	<data>AgAAAA==</data>
	<key>model</key>
	<string>Intel UHD Graphics 630</string>
	<key>rps-control</key>
	<data>AQAAAA==</data>
</dict>
```

  
### Kext说明
- Lilu.kext  # 基础必备，很多kext都依赖于它
- VirtualSMC.kext  # 模拟白苹果的 SMC 芯片
- SMCProcessor.kext  # VirtualSMC 的插件，用于监控 CPU 温度
- SMCSuperIO.kext  # VirtualSMC 的插件，用于监控风扇的转速
- NVMeFix.kext  # 用于修复非 Apple 苹果的 NVMe 上的电源管理和初始化
- AppleALC.kext  # 声卡驱动
- AMFIPass.kext  # 禁止AMFI，配合OCLP在Sonoma下修复博通网卡问题
- IO80211FamilyLegacy.kext  # 配合OCLP在Sonoma下修复博通网卡问题
- IOSkywalkFamily.kext  # 配合OCLP在Sonoma下修复博通网卡问题
- LucyRTL8125Ethernet.kext  # Realtek 的 2.5Gb 的网卡驱动
- RadeonSensor.kext  # 读取GPU温度所需，需要Lilu
- SMCRadeonGPU.kext  # 可以选择用于将 GPU 温度导出到 VirtualSMC 以供监控工具读取
- USBPorts.kext  # USB定制
- WhateverGreen.kext  # 显卡驱动
- XHCI-unsupported.kext  # 配合解决 USB 问题的驱动，常用语400以上主板

### 关于Mac序列号的问题
- 下载 OpenCore Configurator for Mac，打开 PlatformInfo -> Model Lookup | Check Coverage 右侧选择 iMac20,1 机型（生成你的唯一硬件UUID），然后 Save as (另存为) config.plist
- 在config.plist文件中找到如下代码，记录MLB、SystemSerialNumber和SystemUUID的值并记住它，更新EFI时，用你记录的值替换 /OC/config.plist 下对应的值即可
PS: 还可使用 Hackintool 工具（系统 -> 序列号生成器）来获取三码

```
<key>PlatformInfo</key>
<dict>
    <key>Generic</key>
    <dict>
        <key>AdviseWindows</key>
        <false/>
        <key>MLB</key>
        <string>C02047501CDPHCDAD</string>
        <key>ProcessorType</key>
        <integer>4105</integer>
        <key>ROM</key>
        <data>ESIzRFVm</data>
        <key>SpoofVendor</key>
        <true/>
        <key>SystemMemoryStatus</key>
        <string>Auto</string>
        <key>SystemProductName</key>
        <string>iMac20,1</string>
        <key>SystemSerialNumber</key>
        <string>C02DQSZFPN5T</string>
        <key>SystemUUID</key>
        <string>C567A1A9-9233-4D4D-B021-E1F38B112F33</string>
    </dict>

```
这部分内容引用自 [Coopydood/OpenCore-Z490E-CometLakeh](https://github.com/Coopydood/OpenCore-Z490E-CometLake) 2024 年 8 月 25 日起更新的，用于修复 HDMI 输出。请添加这些新条目以启用 HDMI！

### 声卡ID

主板自带声卡为ALCS1200A,声卡ID可选为：1、2、3、7、49、50、51、52、69


### Win+Mac双系统解决Win系统时间时差问题

在Windows下运行
```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

### 设置默认启动项
在启动选择界面，先选中要启动的项，然后按键盘的 Ctrl + Enter (回车键) 进入系统，下次重启后默认就选中该项了
