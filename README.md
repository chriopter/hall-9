# hall-9 Overview
HomeAssistant Local LLM Voice Interface

## Parts 
- ESP32-S3 Compatible with local Wake Word Detection
- MAX98357 Amplifier for Speaker
- 4 / 8 Ohm Sepaker
- inmp441 Microphone
- SSD1306 Display (Optional)
- LD2410 Radar (Optional Sensor)
- DHT22 Thermometer (Optional Sensor)

## Bench Case
For Dev purposes, use Bench Case 

## Future Developments
- https://github.com/esphome/feature-requests/issues/2562

# Setup

## Hardware
- Wire up according to Pinout in YAML Code
- 5v for MAX98357 needed (may be provided by ESP32-S3 Board depending on model)

## HA
- Instal Add-On Whisper for Speech to Text
- Install Add-On Piper for Text to Speech
- Both configured via Wyoming
- Use LLM of choice via Add On (e.g. Ollama via Network or ChatGPT)
- Configure Assistant Pipeline in HA
- Place Font ttf in /config/esphome/ and adjust ESP yaml accordingly
- Configure Whisper & Piper 

## ESPHome
- Deploy Code on ESP32
- Set Detect end of speaking detection to aggressive 
