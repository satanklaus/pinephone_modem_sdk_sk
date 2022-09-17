#TODO
0) доступ по ssh
1) можно ли подключиться напрямую к модему через Интернет?
2) поставить zabbix?
3) поставить salt?
4) поставить asterisk

# Pinephone Modem SDK

### (nearly) Free custom firmware for your Pinephone's modem!

This repository contains everything you need to make your own Modem userspace for your Pinephone.

### Latest release: [Version 0.6.7](https://github.com/Biktorgj/pinephone_modem_sdk/releases/latest)

### Supported devices:
* Pinephone
* Pinephone Pro
* EG25-G connected via USB audio

- [Flashing guide](./docs/FLASHING.md)
- [Recommended settings for this firmware](./docs/SETTINGS.md)
- [Build your own](./docs/HOWTO.md)
- [Returning back to stock](./docs/RECOVERY.md)
- Having issues? [Check out if the issue is already documented or create a new one](https://github.com/Biktorgj/pinephone_modem_sdk/issues)
- [We also have a Matrix room!](https://matrix.to/#/#pinephone_modem_sdk-issue-9:matrix.org)


#### Current Status:
* LK Bootloader: Working
  * On reset, the bootloader enters into fastboot mode automatically for 5 seconds, and boots normally unless instructed to stay (leave the command `fastboot oem stay` running while rebooting the modem to make it stop at fastboot).
   * Custom fastboot commands:
    * fastboot reboot-bootloader: Reboot to fastboot
    * fastboot oem stay: Stay in fastboot instead of booting normally
    * fastboot oem reboot-recovery: Reboot to recovery mode
* CAF Kernel: Working
* Audio: Working [Check out recommended settings for your phone](./docs/SETTINGS.md)
* SMS: Working
* GPS: Working
* Sleep / Power management: Working (New current measurement and profiling required after latest changes)
* System images:
  * root_fs: Default system image. Includes a minimal root filesystem and one application replacing the entire Qualcomm / Quectel stack. Some functions may not yet functional
  * recovery_fs: Minimal bootable image to be flashed into the recovery partitions to retrieve logs and make changes to the root image
* Custom AT Commands: Please see this [document](./docs/AT_INTERFACE.md#custom-commands-in-this-firmware)

#### Features not available on stock firmware:
 * Cell broadcast relay to the host as SMS
 * Internal call and SMS support
   * Functionality is added on every release, feel free to check out the [document for available commands](./docs/SMS_INTERFACE.md)
 * Optional persistent storage: By default an unexpected shutdown can't mess your modem
   * If you want to keep logs after reboot, you can enable persistent storage
 * SMS logging capability: It can log every message you send or receive
 * Automatic time synchronization from the carrier into the userspace
 * Minimum clock frequency is set to 100Mhz, either awake or sleeping (stock is 800MHz awake and 400Mhz sleep), making the modem run cooler
 * Different sampling rates available at runtime without requiring a reboot (missing companion app in the pinephone to make use of them)
 * 0 binary blobs in the userspace. Only closed source running on the modem are TZ Kernel and ADSP firmware

#### TODO (in no particular order)
1. [WIP] Find and fix the last remaining USB port reset cause(s)
2. [Testing] Fix audio when doing conferences (audio is cut off when hanging up the first call)
3. [WIP] Internal SMS functionality (Working reliably with ModemManager and in testing with oFono):
  - Can send and receive messages to/from the modem
  - Modem will answer to the number: +22 33 44 55 66 77
  - Send "help" for a list of commands or check the [docs](./docs/SMS_INTERFACE.md)
4. [WIP] Internal call ability (Working with ModemManager / testing with oFono):
  - Can accept outgoing calls or automatically call you when requested from the chat (send "call me" or "call me in X" -seconds- to make it call you)
  - TTS support: While in call, send an SMS to the modem and it will speak the response back

 Contribution is always welcome! Feel free to share any issue or something that you think may be interesting to have!

#### Related Repositories
This project depends on the following repositories:
* [LK2nd fork with a few patches](https://github.com/Biktorgj/lk2nd)
* [Downstream 3.18.140 Kernel based on CAF](https://github.com/Biktorgj/quectel_eg25_kernel)
* [Forked meta-qcom repository](https://github.com/Biktorgj/meta-qcom)
* [The Yocto Project](https://yoctoproject.org)
* [Quectel EG25 firmware repo](https://github.com/Biktorgj/quectel_eg25_recovery)

#### Documentation
I'm really bad at documentation, but you have some docs [here](./docs)

#### Donations
If you want, you can buy me a coffee [ko-fi](https://ko-fi.com/biktorgj)/[liberapay](https://liberapay.com/biktorgj/donate)
