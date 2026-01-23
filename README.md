# Ferris Sweep ZMK Configuration

[![Build firmware](https://github.com/conlank/zmk-config/actions/workflows/build.yml/badge.svg?branch=4.1esb)](https://github.com/conlank/zmk-config/actions/workflows/build.yml)

This repository contains a customized [ZMK](https://github.com/zmkfirmware/zmk) configuration for the split [Ferris Sweep](https://github.com/davidphilipbarr/Sweep) keyboard. It supports a pair of nice!nano v2 peripherals that communicate with a dedicated [Seeed Studio XIAO nRF52840](https://amzn.to/3LOPtYW) board acting as the split dongle. The key split transport is provided by the [ZMK ESB Split Transport module](https://github.com/badjeff/zmk-feature-split-esb) for low-latency communication between the halves and the dongle.

## Highlights

- Ferris Sweep layout with mirrored peripherals and shared keymap.
- ESB-based wireless split transport for reduced latency and reliable peripheral links.
- Dedicated XIAO BLE dongle build target for USB host connectivity.
- Battery reporting retained on peripherals with ESB transport.
- Improved battery benefits of being in Dongle mode.
- GitHub Actions matrix configured to compile dongle and peripheral firmware artifacts.

## Repository Layout

- `boards/shields/sweep/` – Shield overlays, keymap, and Kconfig fragments for central and peripheral builds.
- `config/west.yml` – West manifest that pulls ZMK, the ESB module, and required Nordic SDK components.
- `build.yaml` – GitHub Actions matrix defining build outputs for the dongle and both peripherals.

## ESB Split Transport Notes

- Shared ESB addressing is defined in `boards/shields/sweep/sweep_esb_addr.dtsi`. Change these values if you manage multiple keyboard sets to avoid radio collisions.
- Peripheral IDs (`CONFIG_ZMK_SPLIT_ESB_PERIPHERAL_ID`) are unique per half to distinguish event sources.
- The central build disables BLE advertising to prioritize ESB traffic. Adjust the related options in the `.conf` files if you need BLE connectivity simultaneously.

## Hardware

| Role          | MCU / Module                      |
| ------------- | --------------------------------- |
| Central/Dongle| Seeed Studio XIAO nRF52840 (USB)  |
| Left Peripheral | nice!nano v2 (nRF52840)        |
| Right Peripheral | nice!nano v2 (nRF52840)       |

## Keymap

![keyboard layout](./keymap/sweep.svg)

## Credits

- [Ferris Sweep](https://github.com/davidphilipbarr/Sweep) by David Barr.
- [ZMK Firmware](https://github.com/zmkfirmware/zmk) community.
- [ZMK ESB Split Transport Module](https://github.com/badjeff/zmk-feature-split-esb) by badjeff.
- Seeed Studio for the [XIAO nRF52840](https://amzn.to/3LOPtYW).

## License

This project is released under the MIT License, matching the upstream ZMK licensing.

```
MIT License

Copyright (c) 2025 kmobs

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
