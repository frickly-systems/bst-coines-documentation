# Key Features

## USB DFU

- Code download to RAM or FLASH
- Code read back (upload) from  RAM or FLASH (Useful for taking firmware backups)
- Works with Windows, Linux, macOS and Android.

## BLE DFU

- Code download to FLASH.
- Works with PC and mobile devices with iOS/Android.

Bootloader was written taking into account the following aspects

- Usability.
	1. No special driver installation or admin rights should be required.
	2. The update process should be straight forward.
- Maintainability
	1. Open source community takes care of PC side tools. For eg: dfu-util is a cross platform tool.
	2. Use Google Chrome's WebUSB to update firmware. [Sample implementation](https://devanlai.github.io/webdfu/dfu-util/)
- Size
- COINES on MCU.
