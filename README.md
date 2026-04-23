# hall-9

Hall-9 is a Home Assistant and ESPHome voice device project built as a fork of [esphome/home-assistant-voice-pe](https://github.com/esphome/home-assistant-voice-pe) and adapted for Hall-9 hardware.

The current Hall-9 configuration keeps the upstream Voice PE structure where practical and only patches the hardware-specific parts needed for the Hall-9 board.

- Objective: robust local/offline STT/TTS with wake word on ESP32-S3 hardware
- Base firmware: Home Assistant Voice Preview Edition
- Legacy project history: [`chriopter/hall-9-legacy`](https://github.com/chriopter/hall-9-legacy)

## Hardware

<img width="300" alt="Hall-9 hardware" src="assets/hardware/hall-9-hardware.png" />

### Hardware Parts

- ESP32-S3
- MAX98357 amplifier + speaker (4 Ohm / 8 Ohm)
- INMP441 microphone
- SSD1306 display
- LD2410 radar (optional)
- DHT22 thermometer (optional)

### Bench Case

- Use the bench case in `assets/case/` during development

### Wiring

- Follow the pinout from the Hall-9 configuration
- Provide 5 V for the MAX98357; some ESP32-S3 boards can supply this directly
- If your board cannot switch or supply the amplifier cleanly, add a small transistor stage for the amp power/enable path

## Install

Use this minimal ESPHome package stub in Home Assistant or the ESPHome Device Builder:

```yaml
substitutions:
  device_name: hall-9-device
  device_friendly_name: Hall 9 Device
  device_name_add_mac_suffix: "false"

packages:
  hall9:
    url: https://github.com/chriopter/hall-9
    ref: dev
    file: hall-9.yaml

api:
  encryption:
    key: "YOUR_API_KEY"

ota:
  - platform: esphome
    password: "YOUR_OTA_PASSWORD"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  ap:
    ssid: "Hall-9 Fallback Hotspot"
    password: "YOUR_FALLBACK_PASSWORD"

captive_portal:
```

This package targets the ESP-IDF framework through the included Hall-9 configuration; do not switch it to Arduino.

## Development

Local compile via the official ESPHome Docker image — no Python/ESPHome install needed.

1. Create `secrets.yaml` in the repo root (gitignored):

   ```yaml
   wifi_ssid: "YourSSID"
   wifi_password: "YourPassword"
   ```

2. Create a local wrapper, e.g. `hall-9.local.yaml` (gitignored), that includes the package locally so your in-tree edits get picked up:

   ```yaml
   substitutions:
     device_name: hall-9-device
     device_friendly_name: Hall 9 Device
     device_name_add_mac_suffix: "false"

   packages:
     hall9: !include hall-9.yaml

   api:
     encryption:
       key: "REPLACE_WITH_BASE64_KEY"

   ota:
     - platform: esphome
       password: "REPLACE_WITH_OTA_PASSWORD"

   wifi:
     ssid: !secret wifi_ssid
     password: !secret wifi_password
     ap:
       ssid: "Hall-9 Fallback Hotspot"
       password: "REPLACE_WITH_AP_PASSWORD"

   captive_portal:
   ```

3. Compile:

   ```bash
   docker run --rm -v "$PWD":/config -it ghcr.io/esphome/esphome compile hall-9.local.yaml
   ```

   Flash via USB (replace the device path):

   ```bash
   docker run --rm --device=/dev/ttyACM0 -v "$PWD":/config -it ghcr.io/esphome/esphome run hall-9.local.yaml
   ```

First run pulls the ESP-IDF toolchain (~2–3 GB). Build artifacts land in `.esphome/` (gitignored).

## Credits

- Forked from [`esphome/home-assistant-voice-pe`](https://github.com/esphome/home-assistant-voice-pe); this repository builds on the upstream Home Assistant Voice Preview Edition firmware and keeps its license terms.
- Licensed according to the upstream Home Assistant Voice Preview Edition project; see `LICENSE`.
