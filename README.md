# OpenCore-MAG-B460M-MORTAR-i5-10500-RX-580
微星B460M 迫击炮 ，i5-10400，RX 580 4G 完美黑苹果。

⚠️ 如果使用我的配置，请自行替换三码。

### 更新
- 2024/03/30，基于OpenCore 0.99，macOS Sonoma 14.4.1

### 硬件配置

|  配置|  型号|
|---|---|
|  CPU| I5 10500 |
|  主板| 微星B460M MORTAR |
|  内存|  16G x4 |
|  板载网卡|  RTL8125B|
|  网卡+蓝牙|  博通943602CS|
|  显卡|  核显UHD630+RX 580|

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

### 声卡ID

主板自带声卡为ALCS1200A,声卡ID可选为：1、2、3、7、49、50、51、52、69


### Win+Mac双系统解决Win系统时间时差问题

在Windows下运行
```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

### 设置默认启动项
在启动选择界面，先选中要启动的项，然后按键盘的 Ctrl + Enter (回车键) 进入系统，下次重启后默认就选中该项了
