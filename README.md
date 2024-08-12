<br />
<div align=center>
    <div align="center">
        <img src="https://github.com/acidanthera/OpenCorePkg/raw/master/Docs/Logos/OpenCore_with_text_Large.png" alt="OpenCore Logo" width="256"/>
    </div>
  <h4>OpenCore EFI for Dell Inspiron 5680</a></h4>
</div>

___

> [!IMPORTANT]  
> This EFI is intended to be used for reference only, and cannot be used as-is. Even for identical hardware, you will need to generate your own [SMBIOS](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo) data (this EFI uses iMacPro1,1 due to lack of iGPU), [USB mapping](https://dortania.github.io/OpenCore-Post-Install/usb/), and [ACPI patches](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-prebuilt.html#desktop-coffee-lake) to ensure proper functionality.

> [!CAUTION]
> Please follow the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) to create your own EFI.

___

## 🖥️ Hardware

| Component         | Model                                                |
| ----------------- | ---------------------------------------------------- |
| CPU               | Intel Core i7-8700                                   |
| iGPU              | Intel UHD Graphics 630 (Force disabled by Dell BIOS) |
| dGPU              | NVIDIA GeForce GTX 1070 8GB                          |
| RAM               | 32GB DDR4 2133MHz                                    |
| Storage           | 256GB SATA M.2 SSD                                   |
| Audio             | Realtek ALC3861                                      |
| Ethernet          | Realtek RTL8111                                      |
| Wi-Fi + Bluetooth | Qualcomm QCA9377 (Windows Only)                      |
| BIOS Version      | 2.13.0                                               |
| Chipset           | Intel Z370                                           |

## 📝 Notes

### 🛠️ BIOS Settings

> [!NOTE]
> This is not an exhaustive list of required BIOS settings. Please refer to the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#intel-bios-settings) for more information.

| Setting                               | Value    |
| ------------------------------------- | -------- |
| SATA Mode                             | AHCI     |
| Secure Boot                           | Disabled |
| Intel Software Guard Extensions (SGX) | Disabled |
| Intel Virtualization Technology (VT)  | Enabled  |
| VT-d                                  | Enabled  |
| CSM                                   | Disabled |
| Legacy Option ROMs                    | Disabled |

### 🔌 USB

Due to the 15 port limit imposed by macOS, a rear USB 3.0 (and the USB 2.0 companion port) and a rear USB 2.0 port was disabled to bring the total number of ports down from 18 to 15.

### ⤵️ Installation

If you have an existing Windows installation and wish to install to a partition on this drive, you will need to expand the EFI partition to at least 200MB. This must be done via a bootable partition manager or another device. If needed, the EFI partition can be formatted and recreated by Windows BCDEDIT once expanded.

The macOS High Sierra internet recovery installer no longer supports HTTPS due to outdated certificates. To force the installer to use HTTP, run the following command in Terminal:

```bash
nvram IASUCatalogURL="http://swscan.apple.com/content/catalogs/others/index-10.13-10.12-10.11-10.10-10.9-mountainlion-lion-snowleopard-leopard.merged-1.sucatalog"
```

Once installed, you will need to install all security updates via the App Store before the [NVIDIA Web Drivers](https://images.nvidia.com/mac/pkg/387/WebDriver-387.10.10.10.40.140.pkg) can be installed. Additionally, you may follow [this answer](https://apple.stackexchange.com/a/422333/) to install updated certificates to the System keychain.

### ⚒️ What works

- [x] Power Management
- [x] Graphics Acceleration (NVIDIA)
- [x] DRM
- [x] USB
- [x] Ethernet
- [x] HDMI Audio
- [x] NVRAM
- [x] DVD Drive

### ⚠️ What doesn't work

- [ ] iGPU (Intel UHD Graphics 630)
  - The iGPU is disabled by the Dell BIOS when a dGPU is present, and the option to enable it is locked. This is a common limitation of Dell desktops, and cannot be easily resolved.
  - If running from the iGPU, support exists up to macOS Sequoia (15.x), but requires further configuration - see [here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#add-2) for more information.
- [ ] Wi-Fi + Bluetooth
  - The Qualcomm QCA9377 card is not supported by macOS, and requires replacement with a compatible card. See [here](https://dortania.github.io/Wireless-Buyers-Guide/types-of-wireless-card/m2.html#m-2) for recommendations.
- [ ] Modern macOS versions (Monterey 10.14.x and later)
  - The NVIDIA Web Drivers required by the NVIDIA GeForce GTX 1070 is not supported by macOS Monterey and later, and requires replacement with a supported card. See [here](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html) for recommendations, or remove the dGPU to enable the iGPU.
  - Alternatively, the NVIDIA Web Drivers can be patched to work with later versions of macOS, however Metal functionality is lost.
- [ ] Audio
  - Further testing required
- [ ] Sleep

## 📦 Versions

| Component                                                          | Version |
| ------------------------------------------------------------------ | ------- |
| [OpenCore](https://github.com/acidanthera/OpenCorePkg/)            | 1.0.1   |
| [AppleALC](https://github.com/acidanthera/AppleALC)                | 1.9.1   |
| [CPUFriend](https://github.com/acidanthera/CPUFriend)              | 1.2.8   |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock/)     | 1.1.6   |
| [Innie](https://github.com/cdf/Innie)                              | 1.3.1   |
| [Lilu](https://github.com/acidanthera/Lilu)                        | 1.6.8   |
| [NVMeFix](https://github.com/acidanthera/NVMeFix)                  | 1.1.1   |
| [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X) | 2.4.2   |
| [RestrictEvents](https://github.com/acidanthera/RestrictEvents)    | 1.1.4   |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC)            | 1.3.3   |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen)      | 1.6.7   |

## 📚 References

- [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [OpenCore Post-Install Guide](https://dortania.github.io/OpenCore-Post-Install/)
