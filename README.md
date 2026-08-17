  # Ra1nUSB — Sliver 5.5

A bootable USB image based on macOS.

[Download release v1.0.0](https://github.com/kristoferUA/Ra1nUSB-Sliver-5.5-macOS-image/releases/tag/v1.0.0)

## About the image

A macOS boot image with pre-installed bypass and jailbreak tools. Includes Sliver 5.5 and checkra1n versions 0.9.2, 0.10.1, 0.10.2, 0.11.0, and 0.12.4.

## Download

Download the compressed image from [GitHub Releases](https://github.com/kristoferUA/Ra1nUSB-Sliver-5.5-macOS-image/releases/tag/v1.0.0):

**[Download `Ra1nUSB.Sliver.7z`](https://github.com/kristoferUA/Ra1nUSB-Sliver-5.5-macOS-image/releases/download/v1.0.0/Ra1nUSB.Sliver.7z)**

| Release asset | Value |
| --- | --- |
| Version | `v1.0.0` |
| Archive | `Ra1nUSB.Sliver.7z` |
| Compressed size | Approximately 1.23 GB |
| Archive SHA-256 | `9e4a08844b0b2d49f6c8cd308632f28d851fac5554e538f22dc7d6ca39cf7d9a` |

Extract the archive with [7-Zip](https://www.7-zip.org/) or another 7z-compatible archiver before flashing. Do not select the `.7z` archive in balenaEtcher; select the extracted DMG.

### Extracted image

| Property | Value |
| --- | --- |
| File name | `Ra1nUSB Sliver.dmg` |
| Size | 4,005,560,320 bytes (approximately 3.73 GiB) |
| Image SHA-256 | `4b78b3740b5276bbc559ab916746a9d1fd228e8a6652c1737a78e854e955b24e` |

The DMG is distributed as a compressed Release asset and is intentionally kept outside Git history.

## Hardware requirements

### Minimum

- A desktop or laptop with a supported 64-bit Intel Core processor that can boot from USB.
- Firmware access (UEFI/BIOS) and permission to change the boot order.
- An 8 GB or larger USB flash drive. A reliable 16 GB USB 3.x drive is recommended.
- A display and a wired keyboard; a wired mouse may also be required.
- One free USB port for the boot drive.

### Supported processors

This build supports only older Intel Core processors from the following generations:

| Intel Core generation | Microarchitecture | Common model range | Approximate release period |
| --- | --- | --- | --- |
| 2nd generation | Sandy Bridge | Core i3/i5/i7-2xxx | 2011 |
| 3rd generation | Ivy Bridge | Core i3/i5/i7-3xxx | 2012 |
| 4th generation | Haswell | Core i3/i5/i7-4xxx | 2013–2014 |
| 5th generation | Broadwell | Core i3/i5/i7-5xxx | 2014–2015 |
| 6th generation | Skylake | Core i3/i5/i7-6xxx | 2015–2016 |
| 7th generation | Kaby Lake | Core i3/i5/i7-7xxx | 2016–2017 |
| 8th generation | Coffee Lake / Kaby Lake Refresh | Core i3/i5/i7/i9-8xxx | 2017–2018 |
| 9th generation | Coffee Lake Refresh | Core i3/i5/i7/i9-9xxx | 2018–2019 |
| 10th generation | Comet Lake / Ice Lake | Core i3/i5/i7/i9-10xxx | 2019–2020 |

The following processors are not supported:

- AMD processors;
- Intel Core 1st generation and older;
- Intel Core 11th generation and newer;
- Intel Pentium, Celeron, Atom, Xeon, and Core Ultra processors;
- Apple silicon processors.

A processor being in the supported generation range does not guarantee that the motherboard, graphics, USB controller, network adapter, or other components will work. The USB drive's `config.plist` must still be configured for the exact PC.

### Depending on the intended workflow

- A second USB port and a known-good data cable for any external device used with the environment.
- A native USB 2.0 port or a compatible USB 2.0 hub may work better with older USB-based tools and devices.
- Ethernet may be preferable if the image does not contain a compatible Wi-Fi driver.

### Compatibility notes

- Exact CPU, chipset, graphics, network, and USB-controller compatibility depends on the bootloader, drivers, and configuration bundled in the image.
- Only the Intel Core generations listed above are supported by this build.
- Secure Boot may need to be disabled if the firmware refuses to start the image.
- Legacy/CSM boot may be required on some systems, while others may require UEFI mode. Try the documented mode first.

These are baseline requirements rather than a model-by-model compatibility guarantee.

## Write the image to a USB drive

> [!WARNING]
> Flashing erases the selected USB drive completely. Back up the drive first and verify the target device carefully before starting.

Download `Ra1nUSB.Sliver.7z`, verify its checksum, and extract `Ra1nUSB Sliver.dmg` before following either method below.

### Recommended: balenaEtcher

balenaEtcher supports DMG input and performs a validation pass after writing.

1. Install the latest [balenaEtcher](https://etcher.balena.io/) for your operating system.
2. Connect an empty 8 GB or larger USB flash drive.
3. Start balenaEtcher and choose **Flash from file**.
4. Select `Ra1nUSB Sliver.dmg`.
5. Choose the correct USB drive under **Select target**.
6. Select **Flash** and approve the administrator prompt if requested.
7. Wait for both writing and validation to finish.
8. Safely eject the USB drive.

Windows may report that one or more partitions are unreadable after flashing. Do not format them; this can be normal for macOS-formatted boot media.

## Configure `config.plist` on the USB drive

> [!IMPORTANT]
> After flashing the image and before the first boot from the USB drive, edit the bootloader's `config.plist` on the flashed drive for the exact components in your PC. The default configuration is not universal and may fail to boot—or behave incorrectly—on different hardware.

Mount the bootloader/EFI partition of the flashed USB drive, locate `config.plist`, and review at least the following areas where applicable:

- CPU generation, motherboard chipset, and firmware mode;
- ACPI patches and SSDTs;
- graphics configuration and device properties;
- USB controller mapping;
- network, audio, and storage drivers/kexts;
- SMBIOS/PlatformInfo values, boot arguments, and bootloader quirks.

Keep a backup of the original file before editing it. The exact file location and available settings depend on the bootloader included with the image. Validate the completed `config.plist` with a tool that matches the installed bootloader version before booting from the USB drive.

## Boot from the USB drive

1. Confirm that `config.plist` on the flashed USB drive has been adapted to the computer's hardware.
2. Leave the flashed USB drive connected and restart the computer.
3. Open the one-time boot menu. Common keys are `F12`, `F11`, `F9`, `Esc`, or `Option` on Intel Macs; the exact key depends on the manufacturer.
4. Select the USB drive. If two entries are shown, start with the UEFI entry unless the compatibility notes specify Legacy/CSM mode.
5. If the firmware blocks the drive, disable Secure Boot temporarily and try again.
6. At the bootloader screen, select the macOS environment and allow the first boot extra time.

Avoid installing or writing anything to an internal disk unless you have a verified backup and deliberately intend to modify that disk.

## Verify the download

Verify both the downloaded archive and the extracted image before flashing.

### Windows PowerShell

```powershell
Get-FileHash -LiteralPath '.\Ra1nUSB.Sliver.7z' -Algorithm SHA256
Get-FileHash -LiteralPath '.\Ra1nUSB Sliver.dmg' -Algorithm SHA256
```

### macOS or Linux

```bash
shasum -a 256 'Ra1nUSB.Sliver.7z'
shasum -a 256 'Ra1nUSB Sliver.dmg'
```

Expected SHA-256 values:

```text
9e4a08844b0b2d49f6c8cd308632f28d851fac5554e538f22dc7d6ca39cf7d9a  Ra1nUSB.Sliver.7z
4b78b3740b5276bbc559ab916746a9d1fd228e8a6652c1737a78e854e955b24e  Ra1nUSB Sliver.dmg
```

## Troubleshooting

- **The USB drive is not listed:** reconnect it directly, try another port, and confirm that removable drives are visible to the flashing tool.
- **Validation fails:** do not boot from that copy. Reflash it, then try another USB drive or port.
- **The computer returns to the firmware menu:** try the other UEFI/Legacy mode and confirm that Secure Boot is disabled if required.
- **Boot stops or the display goes blank:** the system may need a different graphics, ACPI, or chipset configuration. Record the last visible message and add the hardware model when opening an issue.
- **Keyboard, mouse, or external device is not detected:** try a USB 2.0 port, a compatible hub, or another controller.

## Responsible use

Use this environment only with hardware and devices that you own or are explicitly authorized to service. You are responsible for backups, data loss, warranty implications, software licensing, and compliance with applicable law. This repository does not grant rights to redistribute macOS or third-party software contained in the image.

## Distribution notes

The image is distributed as the compressed `Ra1nUSB.Sliver.7z` asset in [Release v1.0.0](https://github.com/kristoferUA/Ra1nUSB-Sliver-5.5-macOS-image/releases/tag/v1.0.0). Extract the DMG before flashing it to a USB drive.

Large disk images and archives are deliberately excluded from Git history. The repository tracks documentation and checksums, while downloadable builds are published through GitHub Releases.

## Credits

- [AppleTech752](https://appletech752.com/) — developer of the Sliver tool.
- [checkra1n](https://checkra.in/) — the checkra1n team, developers of the checkra1n software.

## License

Copyright (C) 2026 kristoferUA.

Repository-owned materials are licensed under the [GNU General Public License v3.0 or later](LICENSE). Third-party software, macOS, trademarks, and other bundled components remain subject to their respective owners' terms and are not relicensed by this repository.
