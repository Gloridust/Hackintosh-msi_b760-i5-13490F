# Hackintosh EFI

![GitHub release](https://img.shields.io/github/v/release/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)
![GitHub release date](https://img.shields.io/github/release-date/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)
![GitHub last commit](https://img.shields.io/github/last-commit/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)
![GitHub download latest](https://img.shields.io/github/downloads/Gloridust/Hackintosh-msi_b760-i5-13490F/latest/total?style=flat-square)
![GitHub download total](https://img.shields.io/github/downloads/Gloridust/Hackintosh-msi_b760-i5-13490F/total?style=flat-square)  
![GitHub stars](https://img.shields.io/github/stars/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)
![GitHub forks](https://img.shields.io/github/forks/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)
![GitHub issues](https://img.shields.io/github/issues/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)
![GitHub issues closed](https://img.shields.io/github/issues-closed/Gloridust/Hackintosh-msi_b760-i5-13490F?style=flat-square)  

此文档的语言为简体中文，仅针对中文用户。For English? [Please click here](https://github.com/Gloridust/Hackintosh-msi_b760-i5-/README_en.md).


## 支持版本

目前仅在macOS13测试过，建议安装 macOS12～13，macOS14尚未测试。  
注意：**macOS14中博通网卡驱动丢失**，需要自行修补驱动kext，建议等待成熟方案，**不建议升级macOS14**

## 我的硬件

- CPU：i5-13490F
- 主板：微星B760m-Bomber-D4
- 内存：金百达银爵 3600 16g*2
- 显卡：蓝宝石RX6600 8g白金
- 固态：Tiplus7100 1tb
- 网卡：bcm943602cs （白苹果原厂拆机网卡，有三码）
- 机箱： 乔思伯c6
- 电源： 酷冷至尊g600
- cpu散热： 利民axp90-47
- 机箱散热： 利民TL-C12 pro

理论上来说，只要主板的品牌以及系列型号相同，网卡免驱那么就都可以直接通用，不必完全相同。  

## 兼容性（完美黑苹果）

### 目前正常运行的有

- [x] 声卡 (板载) / 网卡 (板载)
- [x] 显卡 (独显) / 硬解 4K (HEVC + H.264)
- [x] WiFi (PCI-E 设备) / 蓝牙 (PEI-E 载 USB 设备)
- [x] 隔空投送 / 接力
- [x] FaceTime / iMessage
- [x] Apple Music / Apple TV Plus
- [x] 原生电源管理 / HWP 变频
- [x] 睡眠 / 键盘、鼠标唤醒
- [x] 其他白果功能 (99%)

### 目前无法正常运行的有

- [ ] 蓝牙音频设备无法调节声音
- [ ] 随航黑屏
- [ ] 机箱前置 Type-c 接口无法使用（没有Type-c 接口可忽略）

## 使用之前

### 调整BIOS
首先请利用微星官方软件将BIOS更新到最新版本（因为在2023年9月后的版本才有D.T.M功能，能很大程度上避免一些报错）
然后在BIOS中启用：
- D.T.M

然后参考[国光的这篇教程中提供的BIOS建议](https://apple.sqlsec.com/3-%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C/3-1/#intel-bios)对 BIOS 设置做出更改，建议使用 BIOS 右上角的搜索功能进行检索。如果你的主板真的没有这个选项，那么请跳过它，因为不同型号或不同 BIOS 版本可能造成选项不同。下表摘自[国光的教程](https://apple.sqlsec.com/3-%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C/3-1/#intel-bios)。
### 关闭 - Disable

| 选项                     | 备注                                                         |
| ------------------------ | ------------------------------------------------------------ |
| **Fast Boot**            | 快速启动                                                     |
| **Secure Boot**          | 安全启动                                                     |
| **CSM**                  | `Compatibility Support Module` 兼容容性支持模块              |
| **Intel SGX**            | 也叫做 `Software Guard Extensions`，是一种基于 CPU 硬件的安全保障机制 |
| **Intel Platform Trust** | 英特尔平台可信技术，主要用于密钥管理和安全认证服务           |
| **CFG Lock**             | MSR 0xE2 写保护，建议关闭                                    |
| **VT-d**                 | 也叫 `Intel® Virtualization Technology for Directed I/O (VT-d)` |


### 开启 - Enable

| 选项                                  | 备注                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| **VT-x**                              | 也叫 `Intel® Virtualization Technology`是 CPU 硬件虚拟化技术 |
| **Hyper-Threading**                   | 超线程技术                                                   |
| **Execute Disable Bit**               | Intel 新一代处理器的功能，主要做病毒防护使用                 |
| **DVMT Pre-Allocated: 64MB**          | 分配给DVMT所需内存，4k 分辨率笔记本建议设置 128MB 及其以上   |
| **EHCI/XHCI Hand-off**                | EHCI/XHCI 切换                                               |

### 更改 EFI
- 建议使用OCA重新生成Pi中的序列号、UUID、ROM 等信息，避免三码冲突导致 iService 无法使用。
- 将 [EFI.examle](/EFI.example/) 文件夹重命名为 EFI，然后放进你的 ESP 引导分区即可。


## 感谢
感谢[国光](https://github.com/sqlsec)提供的教程，以及我的朋友Charlse的指导。也感谢为Hackintosh无私贡献的各位开源作者，感谢他们写的驱动。
