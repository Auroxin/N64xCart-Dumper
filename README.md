# N64xCart Dumper

N64xCart Dumper is an open hardware / firmware project for dumping Nintendo 64 cartridges as a USB mass storage device. It is based on the excellent DreamDumper64 project and the `DrmDmp64_mass` firmware, with changes for the N64xCart Dumper hardware.


## Project Status

This repository contains:

- `firmware/N64xCartDumper/` - RP2040 firmware adapted for the N64xCart Dumper board.
- `hardware/PCB/` - KiCad schematic and PCB layout.
- `hardware/production/` - production files for PCB manufacturing.
- `extras/` - extra project files, if any.

The device appears to the computer as a USB mass storage device. The virtual FAT16 disk exposes N64 cartridge data and save data files such as ROM, EEPROM, SRAM and FlashRAM where supported by the firmware.

### Known Issues – CIC Detection

The current hardware revision (v1.x) does not provide a clock signal to the CIC (Copy Integrity Check) chip inside the cartridge. Under normal operation, this clock signal is supplied by the N64 console itself. Since the clock is not connected in this hardware version, the CIC chip on the cartridge cannot function properly during operation.

Save backup functionality: ✅ NOT affected. The CIC error does not interfere with the ability to read or back up save data from the cartridge. You can safely use the backup feature.
CIC detection / verification: ❌ The CIC chip will not respond correctly. As a result, the TXT log file generated during the backup process will report a CIC-related error. This is expected behavior given the current hardware design.

### Planned Fix
A future hardware revision is planned to address this issue. The updated design will include the necessary clock routing to the CIC chip, allowing proper CIC detection and verification.

## Origin and Credits

This project exists because of prior open source work. Please visit and support the original authors:

- DreamDumper64 hardware project by khill25: https://github.com/khill25/Dreamdumper
- `DrmDmp64_mass` firmware by nopjne: https://github.com/nopjne/drmdmp64_mass
- TinyUSB USB stack: https://github.com/hathach/tinyusb
- Raspberry Pi Pico / RP2040 SDK ecosystem: https://github.com/raspberrypi/pico-sdk

My changes are focused on adapting the firmware and hardware layout for the N64xCart Dumper board, including the PCB layout, production files, and acrylic enclosure design.


## Hardware

The hardware in this repository was redrawn and laid out for the N64xCart Dumper form factor while following the DreamDumper64 hardware principles.

Current hardware files:

- KiCad project: `hardware/PCB/N64xCartDumper-v1.1.kicad_pro`
- Schematic: `hardware/PCB/N64xCartDumper-v1.1.kicad_sch`
- PCB layout: `hardware/PCB/N64xCartDumper-v1.1.kicad_pcb`
- Production archive: `hardware/production/N64xCart-Dumper-v1.1-20260612.zip`

## Firmware

The firmware is based on `DrmDmp64_mass`, a mass storage device firmware for DreamDumper64. It has been modified for the N64xCart Dumper hardware.

Important local changes include:

- USB product strings changed to `N64xCart Dumper`.
- Hardware pin and LED configuration adapted for this board.
- Virtual disk label/product information updated for N64xCart Dumper.
- Project files arranged under `firmware/N64xCartDumper/`.

## Building Firmware

The active firmware build entry is the CMake project in `firmware/N64xCartDumper/`.

Typical build flow:

```sh
cd firmware/N64xCartDumper
mkdir build
cd build
cmake ..
cmake --build .
(optional) put pico in bootloader mode and copy the N64xCartDumper.uf2 to the attached drive.
```

You will need a working Raspberry Pi Pico / RP2040 build environment, including the Pico SDK, CMake, a supported ARM GCC toolchain, and the TinyUSB dependencies used by this project.

Note: the included `Makefile` appears to be inherited from an earlier TinyUSB example layout and may not match the current source file names. Prefer the CMake build unless you intentionally update the Makefile.

## Buying a Finished Unit

I also sell assembled N64xCart Dumper units on AliExpress. Buying one helps support the time spent on PCB layout, testing, assembly, enclosure design, and continued open source maintenance.

- Support Us: [Product Link](https://www.aliexpress.com/item/1005012654363194.html)

Thank you for supporting this project. If you build your own, improve the design, or find a bug, contributions and feedback are welcome.

## License Notes

This repository contains code and design work derived from other open source projects. Please check the original projects and bundled third-party files for their license terms:

- `DrmDmp64_mass`: https://github.com/nopjne/drmdmp64_mass
- DreamDumper64: https://github.com/khill25/Dreamdumper
- TinyUSB license file included at `firmware/N64xCartDumper/external/tinyusb/LICENSE`

Source files inherited from `DrmDmp64_mass` include their original copyright and license headers. New N64xCart Dumper hardware files and modifications should be used with respect for the upstream projects and their licenses.

## Disclaimer

This is an independent hobbyist/open hardware project. It is not affiliated with or endorsed by Nintendo. Use it only with cartridges and data you legally own and are allowed to back up under your local laws.

