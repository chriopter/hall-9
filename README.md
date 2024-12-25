# hall-9 Overview

- **hall-9**: Local LLM integration with Home Assistant & ESPHome
- **Objective**: Achieve offline STT/TTS with a wake-word on an ESP32-S3

---

<details>
  <summary>🔧 Building the Device</summary>

### **Hardware Parts**

- **ESP32-S3** (local wake-word detection capable)
- **MAX98357** Amplifier + **Speaker** (4 Ω / 8 Ω)
- **INMP441** Microphone
- **SSD1306** Display
- **LD2410** Radar (optional)
- **DHT22** Thermometer (optional)

### **Bench Case**

- Use asset folder linked bench case if you want

### **Wiring**

- Follow pinout from YAML configuration
- Provide **5 V** for MAX98357 (some ESP32-S3 boards supply this directly)

</details>

<details>
  <summary>⚙️ Install ESP32</summary>

### **ESPHome Setup**

1. **ESP32 Deployment**
   - Create a standard config in ESPHome
   - Set `framework: esp-idf`

2. **Packages**
   - Include those from `hall-9.yaml`
   - Changes are Automatically pulled by ESPHome on updating

3. **Speech End Detection**
   - Set to “aggressive” to reduce latency

</details>

<details>
  <summary>📡 Home Assistant Voice Pipeline</summary>

### **Home Assistant Voice Pipeline**

1. **Whisper (STT) & Piper (TTS)**
   - Install add-ons
   - Configure both via Wyoming

2. **LLM of Choice**
   - Example: Ollama (networked) or ChatGPT
   - Integrate via Add-On

3. **Assistant Pipeline**
   - Configure in Home Assistant
   - Reference Whisper & Piper

</details>

---

<details>
  <summary>🚀 4. Future To-Dos</summary>

### **Future Developments**

- [ESPhome Feature Request #2562](https://github.com/esphome/feature-requests/issues/2562)
- [HA Community Discussion](https://community.home-assistant.io/t/voice-assistant-wake-word-media-player/634984/9)

### **To-Do**

- Design a new case
- Update from repo
- Docker for external Whisper

</details>
