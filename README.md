# 1. Overview

- **hall-9**: Local LLM integration with Home Assistant & ESPHome
- **Objective**: Achieve offline STT/TTS with a wake-word on an ESP32-S3

Repo primarily contains the [hall-9.yaml](hall-9.yaml) file for ESPHome configuration and the [/assets/case](assets/case/) folder for case files.

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

- Use the bench case available in the [/assets/case](assets/case/) folder during development

### **Wiring**

- Follow the pinout from the `hall-9.yaml` configuration
- Provide **5 V** for MAX98357 (some ESP32-S3 boards supply this directly)

</details>

<details>
  <summary>⚙️ Install ESP32</summary>

### **ESPHome Setup**

1. **ESP32 Deployment**
   - Create a standard config in ESPHome
   - Set `framework: esp-idf`

2. **Packages**
   - Include packages from [hall-9.yaml](hall-9.yaml) or selectively by umcommenting
   - Changes are automatically pulled by ESPHome upon updating

3. **Speech End Detection**
   - Set to “aggressive” to reduce latency

</details>

<details>
  <summary>📡 Prepare Home Assistant Voice Pipeline</summary>

### **Home Assistant Voice Pipeline**

1. **Whisper (STT) & Piper (TTS)**
   - Install add-ons
   - Configure both via Wyoming
   - Piper: Set Noise Scale to 0
   - Maybe run Whisper externally
   - docker run -it -p 10300:10300 -v /Users/chriopter/whisper-server:/data rhasspy/wyoming-whisper --model base --language de --beam-size 2 --initial-prompt "nachfolgend ist eine deutsche Untehraltung zur Steuerung eines Smart Homesystems. Wörter wie Licht, Rolladen und ähnliches werden verwendet."


2. **LLM of Choice**
   - Example: Ollama (networked) or ChatGPT
   - Integrate via Add-On

3. **Assistant Pipeline**
   - Configure in Home Assistant
   - Reference Whisper & Piper

</details>

---

# 🚀 Future To-Dos

- Design a new case
- Timer
- Mic Settings
