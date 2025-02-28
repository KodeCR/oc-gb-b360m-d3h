# GigaByte B360M D3H BIOS setting for OpenCore
Italic settings are not required

## M.I.T
*Default settings (mostly Auto)*

## System
*BIOS Version F15b*

## BIOS
- CFG Lock: Disabled 
- Fast Boot: Disabled
- *Windows 8/10 Features: Windows 8/10*
- CSM Support: Disabled
- Secure Boot Enable: Disabled

## Peripherals
- *Intel Platform Trust Technology (PTT): Enabled*
- *Software Guard Extensions (SGX): Disabled*
- *Trusted Computing -> Security Device Support: Enable*
- Super IO Configuration -> Serial Port: Disable
- Super IO Configuration -> Parallel Port: Disable
- *USB Configuration -> Legacy Hand-off: Disabled*
- *USB Configuration -> XHCI Hand-off: Enabled*
- *USB Configuration -> USB Mass Storage Driver Support: Enabled*
- *USB Configuration -> Port 60/64 Emulation: Disabled*
- Network Stack Configuration -> Network Stack: Disabled
- SATA And RST Configuration -> SATA Mode Selection: AHCI
- *SATA And RST Configuration -> Aggressive LPM Support: Disabled*
- Intel Ethernet Connection -> NIC Configuration -> Wake On LAN: Disabled (breaks sleep, restart on wake)

## Chipset
- VT-d: Disabled (causes WiFi/Bluetooth issues, bad connection, alternative is DisableIoMapper: True)
- *Internal Graphics: Enabled*
- *DVMT Pre-Allocated: 64M*
- *DVMT Total Gfx Mem: MAX*
- *Audio Controller: Enabled*
- *Above 4G Decoding: Enabled*
- *PCH LAN Controller: Enabled*
- *Wake on LAN Enable: Enabled*
- *IOAPIC 24-119 Entries: Enabled*

## Power
- *Platform Power Management: Enabled*
- *PEG ASPM: Enabled*
- PCH ASPM: Disable (cause WiFi/Bluetooth issues, no connection)
- *DMI ASPM: Enabled*
- *AC Back: Always Off*
- *Power On By Keyboard: Disabled*
- *Power On By Mouse: Disabled*
- *ErP: Enabled*
- *Soft-Off by PWR-BTTN: Instant-off*
- *Resume by Alarm: Disabled*
- *Power Loading: Auto*
- CEC 2019 Ready: Disabled (needed, otherwise forces PCH ASPM to enabled)
- RC6(Render Standby): Disabled (breaks sleep, no wake)

# GigaByte B360M D3H USB port map
USB ports on the rear pannel
- 2 USB2 on the left side: top is port 7, bottom is port 8
- USB3 gen 2 port in the middle: port 1(USB2)/17(USB3)
- USB-C port (with switch) in the middle: port 2(USB2)/18(USB3)
- 2 USB3 on the right side: top is port 6(USB2)/22(USB3), bottom is port 5(USB2)/21(USB3)

USB internal connectors
- F_USB30: port 4(USB2)/20(USB3) and port 3(USB2)/19(USB3)
- F_USB1: port 13(USB2) and port 14(USB2)
- F_USB2: port 9(USB2) and port 10(USB2)

The DSDT uses \UMAP for USB2 ports (HS__) and \UMP3 for USB3 ports (SS__).
They are bitmaps where a high bit at a bit position enables the corresponding port. So 0x33FF/0b0011_0011_1111_1111 enables all USB2 port and 0x3F/0b0011_1111 enables all USB3 ports.
macOS only supports a maximum of 15 ports. The following SSDT disable the internal F_USB1/F_USB2 except for port 14 and enables all others.

```
//
// SSDT to set USB map (UMAP)
//
DefinitionBlock ("", "SSDT", 2, " ", "UMAP", 0x00001000)
{
    External (\UMAP, IntObj)
    External (\UMP3, IntObj)
 
    Scope (\_SB)
    {
        Method (_INI, 0, NotSerialized)  // _INI: Initialize
        {
            Store (0x20FF, \UMAP)
            Store (0x003F, \UMP3)
        }
    }
}
```
