# C5 Marauder Dongle GPS Test

Split firmware files for the ESP32 T-Dongle C5 Marauder GPS test build.

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

## After flashing

When flashing finishes, unplug the dongle and plug it back in before testing the firmware.

## Notes

- The bootloader offset for this dongle is `0x2000`.
- Flashing only `firmware.bin` is not enough.
- These files are intended for manual flashing and testing.
