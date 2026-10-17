# OrangeFox Infinix Hot 60 Pro+

Unofficial OrangeFox device tree.

| Device | `X6885` (Infinix) |
|---|---|
| Platform | MT6789 |
| Firmware | 155SP15 |
| Android | Android 16 |

## Layout

| Path | Purpose |
|---|---|
| `.github/workflows/Build.yml` | Builder. Syncs the OrangeFox manifest, then copies **this repo** to `DEVICE_PATH`. |
| `tools/` | `unpack_vendor_boot.py`, `make_vendor_boot.py` (swap only the recovery fragment of a stock `vendor_boot.img`). |
| `prebuilt/modules/` | Stock platform kernel modules (`.ko`) + `modules.load/.dep/.alias/.softdep` for vendor ramdisk. |
| `prebuilt/dtb` | Prebuilt DTB. |
| `recovery/root/lib/modules/touch/` | Recovery touch modules loaded via init rc. |
| `recovery/root/lib/modules/flashlight/` | Recovery flashlight modules loaded via init rc. |
| `patches/` | Source patches applied by `vendorsetup.sh`. |

## Build

1. Fork this repository.
2. Go to `Actions` > `Build Orangefox` > `Run workflow`. Manifest inputs (`SYNC_URL`, `MANIFEST_BRANCH`) stay as before; `DEVICE_PATH` defaults to `device/infinix/X6885`.
3. The image is published as a pre-release together with `SHA256SUMS.txt`.

## Install

1. Reboot to fastboot:
   ```bash
   adb reboot bootloader
   ```
2. Flash the image:
   ```bash
   fastboot flash vendor_boot OrangeFox-X6885-<date>-vendor_boot.img
   ```
3. Reboot to recovery using **Power + Volume Up**.