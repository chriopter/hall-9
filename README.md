# 1. Overview
- **hall-9**: Local LLM integration with Home Assistant + ESPHome  
- **Goal**: Local speech-to-text, text-to-speech, and LLM on an ESP32-S3, integrated into Home Assistant

---

# 2. Home Assistant + Hardware (Collapsed)

- **Home Assistant**:
  - Install + configure **Whisper** (STT), **Piper** (TTS) via Wyoming
  - Integrate an LLM (e.g. Ollama)  
  - Set up Assistant pipelines (Whisper + Piper)  

- **Hardware**:
  - **ESP32-S3** with local wake-word detection
  - **MAX98357** amplifier + speaker (4/8 Ω)
  - **INMP441** microphone
  - Optional: **SSD1306** display, **LD2410** radar, **DHT22** thermometer
  - Provide 5 V to MAX98357 (some ESP32-S3 boards can do this directly)

---

# 3. ESPHome
1. Use standard ESP32-S3 config with `framework: esp-idf`  
2. Include `hall-9.yaml` packages; ESPHome will auto-fetch dependencies  
3. Set speech end-detection to **aggressive**

---

# 4. Future
- [ESPHOME Request #2562](https://github.com/esphome/feature-requests/issues/2562)  
- [HA Community Discussion](https://community.home-assistant.io/t/voice-assistant-wake-word-media-player/634984/9)

**To-Do**:
- Design a new case  
- Repo updates  
- Docker-based external Whisper setup  
