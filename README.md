# C5 Marauder Dongle

Polished split firmware files for the ESP32 T-Dongle C5 Marauder build tested on April 26, 2026.

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

- SD mount, browse, and delete working
- Bluetooth attack status screens working
- Wi-Fi attack status screens working
- Bluetooth Analyzer and WiFi Channel Analyzer working
- Probe Request screen working
- Detect Pineapple, Detect Pwnagotchi, and Detect MultiSSID status screens working
- Card Skimmer Detect display working
- GPS NMEA communication active
- WiFi Wardrive counters and satellite display working

## Known issue

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
