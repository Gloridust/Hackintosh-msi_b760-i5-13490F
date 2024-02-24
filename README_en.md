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

## Supported Versions

OpenCore version: 0.9.7

Optimized for Wi-Fi issues on macOS 14.

Note: **Broadcom Wi-Fi drivers are missing in macOS 14**,you must do sth to fix it. Configurations have been adjusted to support Broadcom Wi-Fi cards in macOS Sonoma. After the update, please use [OpenCore-Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/releases) to fix the Wi-Fi card.

## My Hardware

- CPU: i5-13490F
- Motherboard: MSI B760m-Bomber-D4
- Memory: Kingston Silver 3600 16g*2
- Graphics Card: Sapphire RX6600 8g Platinum
- SSD: Tiplus 7100 1tb
- Network Card: bcm943602cs (Original Apple card, with three codes)
- Case: Jonsbo C6
- Power Supply: Cooler Master G600
- CPU Cooler: Lian Li AXP-90-47
- Case Cooling: Lian Li TL-C12 pro

In theory, as long as the brand and model of the motherboard are the same, and the network card is plug-and-play, they can be used interchangeably without being identical.

## Compatibility (Perfect Hackintosh)

### Currently working perfectly:

- [x] Audio (Onboard) / Ethernet (Onboard)
- [x] Graphics Card (Dedicated) / Hardware Acceleration 4K (HEVC + H.264)
- [x] WiFi (PCI-E device) / Bluetooth (PCI-E to USB device)
- [x] AirDrop / Handoff
- [x] FaceTime / iMessage
- [x] Apple Music / Apple TV Plus
- [x] Native Power Management / HWP Frequency Scaling
- [x] Sleep / Keyboard and Mouse Wake
- [x] Other Apple-like features (99%)

It is recommended to turn off the snooze function before using the sleep function, otherwise it will wake up abnormally and be unable to automatically fall back to sleep again.

![sleep_fix](/readme_src/sleep_fix.png)

### The current exceptions include

- [ ] The audio output has multiple lines and cannot be blocked, but it does not affect use.
- [ ] Sidecar black screen.
- [ ] Front USB Type-C port on the case is not functional (if you don't have a Type-C port, you can ignore this).

![voice_output_error](/readme_src/voice_output_error.png)

## Before Using

### Adjust BIOS Settings
First, use the official MSI software to update your BIOS to the latest version (because starting from September 2023, there is D.T.M functionality that can significantly reduce some errors).
Then, in the BIOS, enable:
- D.T.M

Then, refer to the BIOS recommendations provided in [Guoguang's tutorial](https://apple.sqlsec.com/3-%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C/3-1/#intel-bios) and make changes to the BIOS settings. It is recommended to use the search function in the upper right corner of the BIOS for searching. If your motherboard really doesn't have this option, please skip it, as different models or different BIOS versions may have different options. The table below is excerpted from [Guoguang's tutorial](https://apple.sqlsec.com/3-%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C/3-1/#intel-bios).

### Disable - 

| Option                  | Remarks                                                      |
| ------------------------ | ------------------------------------------------------------ |
| **Fast Boot**            | Fast boot                                                     |
| **Secure Boot**          | Secure boot                                                   |
| **CSM**                  | Compatibility Support Module                                 |
| **Intel SGX**            | Also known as `Software Guard Extensions`, a hardware-based security mechanism |
| **Intel Platform Trust** | Intel Platform Trust Technology, mainly used for key management and security authentication services |
| **CFG Lock**             | MSR 0xE2 write protection, recommended to be turned off       |
| **VT-d**                 | Also known as `Intel® Virtualization Technology for Directed I/O (VT-d)` |

### Enable - 

| Option                                  | Remarks                                                      |
| --------------------------------------- | ------------------------------------------------------------ |
| **VT-x**                                | Also known as `Intel® Virtualization Technology`, a CPU hardware virtualization technology |
| **Hyper-Threading**                     | Hyper-threading technology                                    |
| **Execute Disable Bit**                 | A feature of Intel's new-generation processors, primarily used for virus protection |
| **DVMT Pre-Allocated: 64MB**            | Allocate the required memory to DVMT, recommended settings for 4K resolution notebooks are 128MB and above |
| **EHCI/XHCI Hand-off**                  | EHCI/XHCI handoff                                             |

### Modify EFI
- It is recommended to use OCAT to regenerate the serial number, UUID, ROM, and other information in Pi to avoid conflicts with three codes, leading to the inability to use iService.
- Rename the [EFI.example](/EFI.example/) folder to EFI and place it in your ESP boot partition.

## Acknowledgments
Thanks to [Guoguang](https://github.com/sqlsec) for providing the tutorial, and my friend Charles for his guidance. Also, thanks to the open-source authors who have contributed selflessly to Hackintosh and for writing the drivers.