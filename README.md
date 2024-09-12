# OpenCore-MAG-B460M-MORTAR-i5-10500-RX-5700XT
微星B460M 迫击炮 ，i5-10400，蓝宝石RX 5700XT 8G 完美黑苹果。

⚠️ 如果使用我的配置，请自行替换三码。

### 更新
- 2024/03/30，基于OpenCore 0.9.0，macOS Sonoma 14.4.1
- 2024/05/14，基于OpenCore 1.0.0，macOS Sonoma 14.5
- 2024/09/09，更换显卡为蓝宝石RX 5700XT 8G白金版。之前的显卡RX580 4G的配置文件归档，不再更新
- 2024/09/10，为了测试macOS Sequoia， 更新Lilu.kext ANFIPass.kext IOSkywalkFamily.kext。添加启动参数 -lilubetaall 


### 硬件配置

|  配置|  型号|
|---|---|
|  CPU| I5 10500 |
|  主板| 微星B460M MORTAR |
|  内存|  16G x4 |
|  板载网卡|  RTL8125B|
|  网卡+蓝牙|  博通943602CS|
|  显卡|  核显UHD630+蓝宝石 RX 5700XT|

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
- SSDT-GPRW
- SSDT-MSI-B460M-Devices
- SSDT-PLUG
- SSDT-PM
- SSDT-RX5700XT-Version1.0
- SSDT-SBUS
  
#### 说明
SSDT-AWAC、SSDT-PLUG、SSDT-EC-USBX-DESKTOP这三个为推荐添加的


SSDT-RX5700XT-Version1.0.aml优化 RX 5700XT 独显显示，配合dAGPM.kext一起。


SSDT-GPRW修复睡眠即醒或者休眠问题，遇到问题可以添加


SSDT-MSI-B460M-Devices，运行稳定且没有遇到以上问题，你可能不需要这个 SSDT 文件。但如果遇到设备识别、音频、USB、睡眠等问题可以添加


SSDT-SBUS当主板的 SMBus 存在兼容性问题时，特别是某些电源管理相关的设备无法正确工作时添加


SSDT-PM，加载节能第五项（断电后自动重启生效，PC基本通用的补丁）

### DeviceProperties
#### PciRoot(0x0)/Pci(0x2,0x0)
Intel UHD Graphics 630 
```xml
<dict>
				<key>AAPL,ig-platform-id</key>
				<data>BwCbPg==</data>
				<key>device-id</key>
				<data>mz4AAA==</data>
				<key>framebuffer-patch-enable</key>
				<data>AQAAAA==</data>
				<key>framebuffer-stolenmem</key>
				<data>AAAwAQ==</data>
			</dict>
```


#### RX 5700XT 独显优化
⚠️ 使用了SSDT-RX5700XT-Version1.0 可以不用这部分，两者二选一

使用 Hackintool 获取具体的设备路径，替换下面的路径：PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)
```xml
			<key>PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)</key>
			<dict>
				<key>@0,name</key>
				<string>ATY,Adder</string>
				<key>@1,name</key>
				<string>ATY,Adder</string>
				<key>@2,name</key>
				<string>ATY,Adder</string>
				<key>@3,name</key>
				<string>ATY,Adder</string>
				<key>AAPL00,DualLink</key>
				<data>AQAAAA==</data>
				<key>ATY,Card#</key>
				<string>102-D32200-00</string>
				<key>ATY,Copyright</key>
				<string>Copyright AMD Inc. All Rights Reserved. 2005-2019</string>
				<key>ATY,DeviceName</key>
				<string>W5700X</string>
				<key>ATY,EFIVersion</key>
				<string>01.01.190</string>
				<key>ATY,FamilyName</key>
				<string>Radeon Pro</string>
				<key>ATY,Rom#</key>
				<string>113-D3220E-190</string>
				<key>CAIL_EnableLBPWSupport</key>
				<integer>0</integer>
				<key>CAIL_EnableMaxPlayloadSizeSync</key>
				<integer>1</integer>
				<key>CFG_CAA</key>
				<integer>0</integer>
				<key>CFG_FB_LIMIT</key>
				<integer>0</integer>
				<key>CFG_FORCE_MAX_DPS</key>
				<integer>1</integer>
				<key>CFG_GEN_FLAGS</key>
				<integer>0</integer>
				<key>CFG_NO_MST</key>
				<integer>0</integer>
				<key>CFG_NVV</key>
				<integer>2</integer>
				<key>CFG_PAA</key>
				<integer>0</integer>
				<key>CFG_PULSE_INT</key>
				<integer>1</integer>
				<key>CFG_TPS1S</key>
				<integer>1</integer>
				<key>CFG_TRANS_WSRV</key>
				<integer>1</integer>
				<key>CFG_UFL_CHK</key>
				<integer>0</integer>
				<key>CFG_UFL_STP</key>
				<integer>0</integer>
				<key>CFG_USE_AGDC</key>
				<integer>1</integer>
				<key>CFG_USE_CP2</key>
				<integer>1</integer>
				<key>CFG_USE_CPSTATUS</key>
				<integer>1</integer>
				<key>CFG_USE_DPT</key>
				<integer>1</integer>
				<key>CFG_USE_FBC</key>
				<integer>0</integer>
				<key>CFG_USE_FBWRKLP</key>
				<integer>1</integer>
				<key>CFG_USE_FEDS</key>
				<integer>1</integer>
				<key>CFG_USE_LPT</key>
				<integer>1</integer>
				<key>CFG_USE_PSR</key>
				<integer>0</integer>
				<key>CFG_USE_SCANOUT</key>
				<integer>1</integer>
				<key>CFG_USE_SRRB</key>
				<integer>0</integer>
				<key>CFG_USE_STUTTER</key>
				<integer>1</integer>
				<key>CFG_USE_TCON</key>
				<integer>1</integer>
				<key>PP_DisableDIDT</key>
				<integer>1</integer>
				<key>PP_DisablePowerContainment</key>
				<integer>1</integer>
				<key>PP_DisableVoltageIsland</key>
				<integer>0</integer>
				<key>PP_FuzzyFanControl</key>
				<integer>1</integer>
				<key>device_type</key>
				<string>ATY,AdderParent</string>
				<key>hda-gfx</key>
				<string>onboard-1</string>
				<key>model</key>
				<string>Radeon Pro W5700X</string>
				<key>name</key>
				<string>ATY_GPU</string>
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
- XHCI-unsupported.kext  # 配合解决 USB 问题的驱动，常用于400以上主板
- dAGPM.kext # 配合SSDT-RX5700XT-Version1.0.aml优化 RX 5700XT 独显

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


### 声卡ID

主板自带声卡为ALCS1200A,声卡ID可选为：1、2、3、7、49、50、51、52、69


### Win+Mac双系统解决Win系统时间时差问题

在Windows下运行
```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

### 设置默认启动项
在启动选择界面，先选中要启动的项，然后按键盘的 Ctrl + Enter (回车键) 进入系统，下次重启后默认就选中该项了
