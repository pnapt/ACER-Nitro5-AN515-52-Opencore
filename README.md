# Disclosure
1. This repository is not heavily maintain
2. If you encounter a problem try asking at the r/hackintosh community first, and create an "Issues" in here less likely to get respond

# ACER-Nitro5-AN515-52-Opencore
Acer Nitro5 AN515-52 Hackintosh (Opencore Bootloader)

# Info
![Screenshot](/Docs/about1.png)

**Laptop Specs**
| Hardware | Details |
|------------|-------------------------------|
| Model | Acer Nitro5 2018 (AN515-52) |
| BIOS | v1.28 (Insyde BIOS) |
| Processor | Intel Core i5 8300H |
| Memory | 2x8GB DDR4 2666MHz |
| iGPU | Intel UHD Graphics 630 |
| dGPU | NVIDIA GeForce GTX 1050Ti |
| Wifi | Intel Wireless-AC 9560 |
| Trackpad | ELAN |
| Sound | Realtek ALC255 |
| M.2 Nvme | Colorful SSD CN600 PRO 512 GB |

**OS**
| OS | Details |
|--------------|-----------------|
| macOS | Ventura 13.2 (22D49)|
| Dual boot OS | Windows 11 22H2 |

**Highlight**
| Status | Name | Notes | 
|--------------|--------------|--------------|
| ✅ | Intel UHD Graphics 630 (iGPU) | Graphic acceleration + Encode/Decode w/`WhateverGreen.kext`+`Device Prop` |
| ✅ | Wifi | w/`AirportItlwm.kext` ❌ Air Drop is NOT work |
| ✅ | Bluetooth | w/`IntelBTPatcher.kext`+`IntelBluetoothFirmware.kext`+`BlueToolFixup.kext` |
| ✅ | Ethernet(LAN) | w/`RealtekRTL8111.kext` |
| ✅ | Build-in Keyboard | w/`VoodooPS2Controller.kext`
| ✅ | Trackpad+Gestures | w/`VoodooI2C&HID kext` & `SSDT-XOSI.aml`
| ✅ | fnkeys | Screen brightness ,Volume ,ETC | w/`BrightnessKeys.kext`
| ✅ | Audio (Speaker + Internal Mic + External Speaker) | w/`AppleALC.kext`+`-alcid=17` & Combo Jack w/`VerbStub.kext`
| ✅ | All USB Port | Type C *1 / USB3.0 *1 / USB2.0 *2 w/`USBMap.kext` |
| ✅ | SDCard Reader | w/`RealtekCardReader.kext`+`RealtekCardReaderFriend.kext`
| ✅ | M.2 NVME + 2.5" HDD | NVME w/`NVMeFix.kext` SATA w/`CtlnaAHCIPort.kext`
| ✅ | Battery status | w/`SMCBatteryManager.kext`+`ECEnabler.kext`
| ✅ | Shutdown/Sleep/Wake | w/`SSDT-PMC.aml` & `SSDT-GPRW.aml`
| ❌ | HDMI | Because it connected to NVIDIA GPU |
| ❌ | dGPU | Apple kill its web driver |

### Opencore Config Guide/Explanation
***always lookout on full guide first***

*1. Offical documentation when you download the pkg*

*2. [Dortaina CFL Laptop](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake.html#starting-point)*

>**Notes**
1. This Config `SMBIOS` is `MacBookPro14,3`
This SMBIOS "Maybe" Required `NoTouchID.kext` for remove TouchID Feature & `SMCLightSensor.kext`+`SSDT-ALS0.aml` for display fake dim sensor
if you wanna change to something else Check: `USBMap.kext` `Info.plist` SMBios Targat
2. Additional CPU tweak w/`CPUFriend.kext`

**ACPI**

| Name | Features | Dependency(Needed Patch) |
|--------------|--------------|----------------------------|
| 1. `SSDT-ALS0.aml` | Fake ambient light sensor for EC | - |
| 2.`SSDT-AWAC.aml` | RTC Patch for Intel 300 Series | - |
| 3. `SSDT-dGPU-Off.aml` | Disable External Unsupported GPU | - |
| 4. `SSDT-EC-USBX.aml` | Generic power properties for CPU+USB | - |
| 5. `SSDT-GPRW.aml` | Instant Wake Patch | I.`Change Method(GPRW,2,N) to XPRW`| - |
| 6. `SSDT-HPET.aml` | HPET _CRS (IRQ conflict fix) | I. ` _CRS to XCRS Rename` II. `IPIC IRQ 2 Patch` III. `RTC IRQ 8 Patch` IV. `TIMR IRQ 0 Patch`|
| 7. `SSDT-PLUG.aml` | Sets plugin-type to 1 on first Processor object | -|
| 8. `SSDT-PMC.aml` | PMCR for native 300-series NVRAM |-|
| 9. `SSDT-PNLF.aml` | Defines PNLF device with a _UID of 19 for backlight control |-|
| 10. `SSDT-SBUS-MCHC.aml` | Fixing SMBus support |-|
| 11. `SSDT-XOSI.aml` | Trackpad Mapping | I. `Change _OSI to XOSI, pair with SSDT-XOSI.aml`|

# Benchmark Info
![Geekbench5](/Docs/Geekbench5TEMP.png)

# Credit
**People who made opencore project and kext**
- [Acidanthera](https://github.com/acidanthera/) for Opencore
- [Corpnewt](https://github.com/corpnewt) for all tools eg.ProperTree ,USB Map ,GenSMBIOS and more.
- [Hackintosh-stuff](https://github.com/hackintosh-stuff/ComboJack) for Combojack 3.5 fix

**Thanks to People who did build EFI for this laptop previously**
- [On tonymacx86 by Middleman](https://www.tonymacx86.com/threads/guide-oc-monterey-acer-nitro-5-an515-52-core-i7-8750h-samsung-1tb-960-evo-pcie-nvme.319629/)
- & [r/hackintosh Community](https://www.reddit.com/r/hackintosh/)
