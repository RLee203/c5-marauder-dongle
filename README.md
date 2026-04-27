# C5 Marauder Dongle

Boot-safe split firmware files for the ESP32 T-Dongle C5 Marauder build tested on April 27, 2026.

This repo now tracks the current boot-safe C5 build that replaces the older SPIFFS-based snapshot. The C5 settings path was moved to NVS/Preferences so the dongle boots cleanly after a full erase and still keeps settings across reboot.

## Files

- bootloader.bin
- partitions.bin
- boot_app0.bin
- firmware.bin

## Confirmed flash offsets

- 0x2000 -> bootloader.bin
- 0x8000 -> partitions.bin
- 0xE000 -> boot_app0.bin
- 0x10000 -> firmware.bin

## Confirmed on-device

- Clean boot on the T-Dongle C5 after erase and reflash
- Settings persistence working through reboot
- SD mount, browse, and delete working
- Bluetooth sniffers and analyzer working
- Bluetooth attack status screens working
- Wi-Fi attack status screens working
- Probe Request and Beacon Sniff working
- Deauth Sniff working
- Channel Analyzer and Channel Summary working
- Signal Monitor usable
- Scan AP and Scan AP/STA working
- Card Skimmer Detect display working
- GPS NMEA communication active

## Known issues

- Probe Request, Beacon Sniff, and Packet Monitor still have some top-line background bleed on the C5 UI
- BLE Wardrive counter still needs investigation

## ESP Flash Download Tool

Use chip type `ESP32-C5` and add the four files above with the exact offsets shown.

## esptool example

```text
esptool.py --chip esp32c5 --port COM17 --baud 921600 write_flash -z \
  0x2000 bootloader.bin \
  0x8000 partitions.bin \
  0xE000 boot_app0.bin \
  0x10000 firmware.bin
```

## Notes

- The bootloader offset for this dongle is `0x2000`.
- Flashing only `firmware.bin` is not enough.
- These files are intended for manual flashing and testing.
