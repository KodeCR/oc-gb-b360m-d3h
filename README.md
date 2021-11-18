# GigaByte B360M D3H BIOS setting for OpenCore

## M.I.T
Default settings (mostly Auto)

## System
BIOS Version F12b

## BIOS
- Fast Boot: Disabled
- Windows 8/10 Features: Windows 8/10
- CSM Support: Disabled
- Secure Boot Enable: Disabled

## Peripherals
- Intel Platform Trust Technology (PTT): Enabled
- Software Guard Extensions (SGX): Disabled
- Trusted Computing -> Security Device Support: Enable
- Super IO Configuration -> Serial Port: Disable
- Super IO Configuration -> Parallel Port: Disable
- *USB Configuration -> Legacy Hand-off: Disabled*
- USB Configuration -> XHCI Hand-off: Enabled
- USB Configuration -> USB Mass Storage Driver Support: Enabled
- *USB Configuration -> Port 60/64 Emulation: Disabled*
- Network Stack Coniguration -> Network Stack: Disabled
- SATA And RST Configuration -> SATA Mode Selection: AHCI
- *SATA And RST Configuration -> Aggressive LPM Support: Disabled*
- *Intel Ethernet Connection -> NIC Configuration -> Wake On LAN: Disabled*

## Chipset
- *VT-d: Disabled*
- *Internal Graphics: Enabled*
- *DVMT Pre-Allocated: 64M*
- *DVMT Total Gfx Mem: MAX*
- *Audio Controller: Enabled*
- *Above 4G Decoding: Enabled*
- *PCH LAN Controller: Enabled*
- *Wake on LAN Enable: Disabled*
- *IOAPIC 24-119 Entries: Disabled*

## Power
- *Platform Power Management: Disabled*
- *AC Back: Always Off*
- *Power On By Keyboard: Disabled*
- *Power On By Mouse: Disabled*
- *ErP: Disabled*
- *Soft-Off by PWR-BTTN: Instant-Off*
- *Resume by Alarm: Disabled*
- *Power Loading: Auto*
- *CEC 2019 Ready: Disabled*
- *RC6(Render Standby): Disabled*
