# Funkbasis-ESP32: Base Board for Radio Devices

[Deutsch](README.md) | [English](README.en.md)

**Status: requirements (draft).** No hardware and no firmware yet. The main documentation ([README](README.md) and [docs/pflichtenheft.md](docs/pflichtenheft.md)) is in German. This page is a short summary.

A common base board for radio devices built around an ESP32-S3. The radio module plugs in through connector RX. The module decides which device it becomes.

* **Brain:** ESP32-S3-DevKitC-1 (N16R8) on socket headers.
* **UI:** 2.0" ST7789V display and a rotary encoder with push button.
* **Power:** one cell (14650 or flat LiPo), linear regulator, reverse polarity protection, USB-C charging with a linear charger. No switching regulators, to keep MW and SW quiet.
* **Audio:** PAM8403 amplifier module, speaker, 3.5 mm jack with switch contact, line out, optional Bluetooth transmitter socket.
* **Radio module:** connector RX with I2C, reset, audio left and right, 3.3 V and reserved I2S lines.
* **Devices:** [Funkfüürli](https://github.com/MaShaoDe/Funkfuerli) (emergency radio for kids, FM, MW, SW, RX board with Si4732) and [Wellenjäger](https://github.com/MaShaoDe/Wellenjaeger) (ham SDR receiver, later).
* **Firmware** lives in the project repos, not here.

Licenses: hardware CERN-OHL-P-2.0, documentation CC-BY-4.0. See [LICENSE.md](LICENSE.md).

73 de Marcel (MaShaoDe)
