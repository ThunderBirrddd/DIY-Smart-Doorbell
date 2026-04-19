# 🚪 Smart Doorbell & Remote Camera System

![Hero Image Placeholder](https://via.placeholder.com/1200x600?text=Hero+Image+Placeholder)

![C++](https://img.shields.io/badge/C++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![ESP32](https://img.shields.io/badge/ESP32-000000.svg?style=for-the-badge&logo=espressif&logoColor=white)
![Home Assistant](https://img.shields.io/badge/home%20assistant-%2341BDF5.svg?style=for-the-badge&logo=home-assistant&logoColor=white)
![Apple HomeKit](https://img.shields.io/badge/Apple%20HomeKit-000000.svg?style=for-the-badge&logo=apple&logoColor=white)
![MQTT](https://img.shields.io/badge/mqtt-%23660066.svg?style=for-the-badge&logo=mqtt&logoColor=white)

---

## 📖 Overview

A fully custom-built IoT doorbell designed from the ground up to completely bypass locked-in, proprietary cloud ecosystems while maintaining a premium user experience. This system delivers ultra-low-latency, real-time video streaming, and crystal-clear Push-to-Talk (PTT) two-way audio. Seamlessly integrated with Home Assistant, it brings native Apple HomeKit Secure Video functionality to a DIY device with uncompromised privacy and control over your own data.

---

## 🏗️ System Architecture & Features

- **🌐 Local First:** Everything runs locally—zero cloud dependencies, forced updates, or subscription fees.
- **⚡ Ultra-Low Latency Video:** Optimized real-time video pipeline streaming reliably over the local network.
- **🗣️ Custom PTT Audio Routing:** Engineered I2S audio routing to handle simultaneous communication without hardware choking.
- **🏠 Native Home Ecosystems:** Exposed flawlessly to Apple HomeKit via Home Assistant integrations.

![Architecture Placeholder](https://via.placeholder.com/800x400?text=System+Architecture+Diagram)

---

## 🛠️ Hardware Bill of Materials (BOM)

| Component | Purpose & Description | Qty | Link |
| :--- | :--- | :--- | :--- |
| **ESP32-CAM** | Core microcontroller for video ingestion and processing. | 1 | [Link](#) |
| **INMP441** | Omnidirectional I2S MEMS microphone for clear voice capture. | 1 | [Link](#) |
| **MAX98357A** | I2S Class D audio amplifier for the outdoor speaker. | 1 | [Link](#) |
| **Mini Speaker** | 3W 4Ohm speaker for visitor playback. | 1 | [Link](#) |
| **Custom Housing** | 3D Printed, weather-resistant enclosure for the unit. | 1 | [Link](#) |
| **Power Supply** | 5V 2A regulator and necessary discrete components. | 1 | [Link](#) |

---

## 💻 Software Stack & Logic

The system functions asynchronously, using the ESP32 to capture frames and pipe both audio and video streams efficiently. The ESP stream is exposed to Home Assistant directly over the local network. Home Assistant then acts as the central intelligence bridge, bringing the stream and the physical doorbell trigger events natively into the Apple HomeKit application.

### Push-to-Talk / Audio Configuration Logic

```cpp
// 💡 [Insert core PTT / I2S audio logic here]
// Example initializing logic for handling full duplex audio via I2S

void setup_audio() {
  // Initialize I2S for MAX98357A (Speaker Output)
  i2s_config_t out_config = {
      .mode = (i2s_mode_t)(I2S_MODE_MASTER | I2S_MODE_TX),
      .sample_rate = 16000,
      .bits_per_sample = I2S_BITS_PER_SAMPLE_16BIT,
      /* ... routing configuration details */
  };
  
  // Initialize I2S for INMP441 (Microphone Input)
  i2s_config_t in_config = {
      .mode = (i2s_mode_t)(I2S_MODE_MASTER | I2S_MODE_RX),
      .sample_rate = 16000,
      .bits_per_sample = I2S_BITS_PER_SAMPLE_16BIT,
      /* ... routing configuration details */
  };
  
  // Custom routing and buffer allocations
}

void loop() {
  // Async logic to handle Push-To-Talk states over MQTT
}
