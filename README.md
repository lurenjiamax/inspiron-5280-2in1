# Dell inspirion 5280 2in1
As far as I know, 5280 is a Chinese custimization product.
But on dell website, there is barely no support for this device.

### Hardware Info
```
CPU: i5-7y54
RAM: 8G,1866,LPDDR3
ROM: 256G samsung / Micron 1100_MTFDDAV256TBN / MZ-NLN256C
SCREEN: BOE075C TV123WAM-ND0/1 1080p 12.3inci
SOUND: Realtek ALC3246
LTE Mordem: Fibocom L830-CN
WIRELESS: Intel AC 3165 (Soldered)
```

## Archlinux
6.1.9 mainline kernel

### rotate
Install `iio-sensor-proxy`
#### Gnome
- autorotate "Use the latest auto-rotate extension"
#### KDE@x11
- autorotate "Use `kde-auto-rotate-git`, stylus rotate works with modified version."

### Volume keys and meta key on the device
#### KDE@wayland
- volume key and meta key on the device will stop working after remove the keyboard, it is a libinput quirks issue.
```bash
# Add these to /etc/libinput/local-overrides.quirks 
[Dell 5280 2in1]
MatchName=AT Translated Set 2 keyboard
MatchUdevType=keyboard
MatchDMIModalias=dmi:*svnDellInc.:*
MatchBus=ps2
ModelTabletModeNoSuspend=1
AttrKeyboardIntegration=internal
```
Reboot and it should work.

### LTE moderm
```bash
Install "modemmanager" and "usb_modeswitch" , enable "ModemManager.service" and reboot.
```

### Micphone(only internal mic)
- The micphone will keep disconnectting, which will cause inusability and high cpu usage.
```bash
Install "HDAJackRetask"
Select "Realtek ALC3246" and Set "Black Mic,Right side" to "Not connected".
Remember to apply and "install boot override", reboot.
```

### Powermanage after close the lid
```bash
# Add this to /etc/default/grub GRUB_CMDLINE_LINUX_DEFAULT
acpi_rev_override=1 acpi_osi=Linux mem_sleep_default=deep
```
Then use "grub-mkconfig" to update grub.cfg

### Camera
Not work since no driver.

## Driver backup for win10 and win11
Install the driver to fix Orientation and camera.

From https://tieba.baidu.com/p/6553351466 by @chenwenjieppp
