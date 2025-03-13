# OpenCore-MAG-B460M-MORTAR-i5-10500-RX-5700XT
微星B460M 迫击炮 ，i5-10400，迪兰恒进RX 6600XT 8G 完美黑苹果。

⚠️** 如果使用我的配置，请自行替换三码。**

### 更新
- 2024/09/15 基于OpenCore 1.0.1，macOS Sonoma 14.6.1
- 2024/09/15 为了测试macOS Sequoia， 更新Lilu.kext ANFIPass.kext IOSkywalkFamily.kext。添加启动参数 -lilubetaall 
- 2024/09/18 更新到Sequoia 15.0 版本
- 2024/10/29 更新 OpenCore 到 1.0.2，更新 相关kext，更新 MacOS Sequoia 到 15.1
- 2024/12/04 更新OpenCore到1.0.3，更新相关kext到最新
- 2025/03/13 更新OpenCore到1.0.4，更新相关kext到最新


### 硬件配置

|  配置|  型号|
|---|---|
|  CPU| I5 10500 |
|  主板| 微星B460M MORTAR |
|  内存|  16G x4 |
|  板载网卡|  RTL8125B|
|  网卡+蓝牙|  博通943602CS|
|  显卡|  核显UHD630+迪兰恒进 RX 6600XT |

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
- Settings -> 安全 -> 安全引导 -> 安全启动：关闭
- Settings -> 唤醒设置 -> USB设备从S3/S4/S5唤醒：允许
- Settings -> 唤醒设置 -> PS/2鼠标从S3/S4/S5唤醒：允许
- Settings -> 唤醒设置 -> USB键盘从S3/S4/S5唤醒：任意键
- Settings -> 高级 -> 内建显示器配置 -> 集成显卡多显示器：允许（否则核显硬件解码失效，只使用核显的可以忽略）
- Settings -> 高级 -> PCIe -> PCI子系统设置 -> Re-Size BAR Support ：禁止
- OC -> CPU 特征 -> Intel 虚拟化技术：允许
- OC -> CPU 特征 -> Intel VT-D 技术：禁止
- OC -> CPU 特征 -> CFG锁定：禁止

启动的时候卡：
```
IOPCIConfigurator::configure kIOPCIEnumerationWaitTime is 900
```
通过在 BIOS 中禁用 Resizable Bar 确实可以解决 macOS 的启动问题，同时你也正确地在 config.plist 中添加了 agdpmod=pikera 来确保显卡兼容性

### 使用的SSDT
- SSDT-AWAC
- SSDT-EC-USBX-DESKTOP
- SSDT-MSI-B460M-Devices
- SSDT-GPRW
- SSDT-PLUG
- SSDT-PM
  
#### 说明
SSDT-AWAC、SSDT-PLUG、SSDT-EC-USBX-DESKTOP这三个为推荐添加的

SSDT-MSI-B460M-Devices，运行稳定且没有遇到以上问题，你可能不需要这个 SSDT 文件。但如果遇到设备识别、音频、USB、睡眠等问题可以添加

SSDT-GPRW修复睡眠即醒或者休眠问题，遇到问题可以添加

SSDT-PM，加载节能第五项（断电后自动重启生效，PC基本通用的补丁）

### DeviceProperties
#### PciRoot(0x0)/Pci(0x1F,0x3)
主板自带声卡为ALCS1200A,声卡ID可选为：1、2、3、7、49、50、51、52、69

我这里用的是1

```xml
			<key>PciRoot(0x0)/Pci(0x1F,0x3)</key>
			<dict>
				<key>layout-id</key>
				<data>AQAAAA==</data>
			</dict>
```
#### PciRoot(0x0)/Pci(0x2,0x0)
核显 Intel UHD Graphics 630
不填写可能会导致VideoProc 中显示HEVC不支持。 
```xml
<key>PciRoot(0x0)/Pci(0x2,0x0)</key>
			<dict>
				<key>AAPL,ig-platform-id</key>
				<data>AwDImw==</data>
				<key>AAPL,slot-name</key>
				<string>Internal@0,2,0</string>
				<key>device-id</key>
				<data>mz4AAA==</data>
				<key>device_type</key>
				<string>VGA compatible controller</string>
				<key>model</key>
				<string>Intel UHD Graphics 630</string>
			</dict>
```

#### RX 6600XT 独显优化

使用 Hackintool 获取具体的设备路径，替换下面的路径：PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)
```xml
			<key>PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)</key>
			<dict>
				<key>@0,name</key>
				<string>ATY,Henbury</string>
				<key>@1,name</key>
				<string>ATY,Henbury</string>
				<key>@2,name</key>
				<string>ATY,Henbury</string>
				<key>@3,name</key>
				<string>ATY,Henbury</string>
				<key>AAPL,slot-name</key>
				<string>Slot-1</string>
				<key>ATY,DeviceName</key>
				<string>W6600X</string>
				<key>ATY,EFIVersion</key>
				<string>01.01.270</string>
				<key>ATY,FamilyName</key>
				<string>Radeon Pro</string>
				<key>CFG_LINK_FIXED_MAP</key>
				<integer>1</integer>
				<key>device_type</key>
				<string>ATY,HenburyParent</string>
				<key>model</key>
				<string>AMD Radeon RRO W6600X</string>
				<key>name</key>
				<string>ATY,Henbury</string>
			</dict>
```

开启启动出现苹果logo后，读取进度条进入第二段进度，黑屏一段时间然后直接进入登录界面
通过OC为显卡注入CFG_LINK_FIXED_MAP属性，属性值可以尝试1/3/4数值，目前来看对绝大多数显卡都有效，但是此方法在4K高刷显示器下无效，因为白苹果也这样。

如这里我注入的是1
  
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
- SMCRadeonSensors.kext  # 读取GPU温度导出到 VirtualSMC 以供监控工具，需要Lilu
- USBPorts.kext  # USB定制
- WhateverGreen.kext  # 显卡驱动
- XHCI-unsupported.kext  # 配合解决 USB 问题的驱动，常用于400以上主板
- HibernationFixup.kext  #解决休眠和唤醒过程中可能遇到的问题

以前是用RadeonSensor.kext + SMCRadeonGPU.kext：读取GPU温度，现在这个项目已经归档，交由 [SMCRadeonSensors](https://github.com/ChefKissInc/SMCRadeonSensors) 

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


### Win+Mac双系统解决Win系统时间时差问题

在Windows下运行
```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

### 设置默认启动项
在启动选择界面，先选中要启动的项，然后按键盘的 Ctrl + Enter (回车键) 进入系统，下次重启后默认就选中该项了
