# 🅿️ Parking Space Detection Using ESP32-CAM with CircuitDigest Cloud API

<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32--CAM-blue?style=for-the-badge&logo=espressif" />
  <img src="https://img.shields.io/badge/AI-CircuitDigest%20Cloud-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Language-C%2B%2B%20(Arduino)-orange?style=for-the-badge&logo=arduino" />
  <img src="https://img.shields.io/badge/Protocol-HTTPS-red?style=for-the-badge" />
</p>

<p align="center">
  A smart, AI-powered <strong>parking space detection system</strong> using the <strong>ESP32-CAM</strong> and <strong>CircuitDigest Cloud API</strong>. Captures a real-time image of a parking area and instantly detects the number of <strong>occupied</strong> and <strong>free</strong> spaces — wirelessly, affordably, and without any ML training!
</p>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [How It Works](#-how-it-works)
- [Components Required](#-components-required)
- [Circuit Diagram](#-circuit-diagram)
- [Getting Started](#-getting-started)
  - [Step 1: Create a CircuitDigest Cloud Account](#step-1-create-a-circuitdigest-cloud-account)
  - [Step 2: Get Your API Key](#step-2-get-your-api-key)
  - [Step 3: Test the API Virtually](#step-3-test-the-api-virtually)
  - [Step 4: Hardware Setup & Code Upload](#step-4-hardware-setup--code-upload)
- [Code Explanation](#-code-explanation)
- [Output](#-output)
- [Advantages & Limitations](#-advantages--limitations)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Relevant Links](#-relevant-links)
- [License](#-license)

---

## 🌍 Overview

Imagine driving into a crowded parking area and not knowing whether a space is available or not. This project solves that problem by creating a **smart and automated parking space detection system** using the **ESP32-CAM** , **ESP32** and **CircuitDigest Cloud**.

the ultrasonic sensor detects the car near it:
1. Then the ESP32 which is connected the ultrasonic sensor sends the alert to the esp32 cam to capture the image
2. The ESP32-Cam capture the image and process the captured image in circuitdigest parking detection API
3. Then if the esp32-cam gives the parking available message the esp32 triggeres the servo motor to open the gate.
4. If it gives the response as parking full the gate will be remain closed.

> **Low-cost. Wireless. Real-time. No ML training required.** ⚡

---


---

## 🧰 Components Required

| S.No | Component | Purpose |
|------|-----------|---------|
| 1 | ESP32-CAM | Microcontroller with built-in camera & Wi-Fi |
| 2 | ultrasonic sensor | Triggers image capture on object near it |
| 3 | Breadboard | Simplifies and organizes circuit connections |
| 4 | USB-to-Serial (FTDI) Adapter *(if needed)* | For programming standard ESP32-CAM without onboard USB |
| 5 | USB Cable | Powers the system via laptop/PC |
| 6 | Servo motor | For the gate control |
| 7 | ESP32 | For controlling the various sensors |

> **⚠️ Note:** If you are using the standard ESP32-CAM (without onboard USB), you need a **USB-to-Serial (FTDI) adapter** for programming:
> - FTDI **TX** → ESP32-CAM **RX** (U0R)
> - FTDI **RX** → ESP32-CAM **TX** (U0T)
> - **GND** → **GND**
> - Hold **GPIO0 LOW** during upload to enter flash mode.

---



## 🚀 Getting Started

### Step 1: Create a CircuitDigest Cloud Account

Go to the [CircuitDigest Cloud website](https://circuitdigest.cloud), create a free account, and log in. On the homepage, scroll down and click on the **Parking Space Detection** feature.

---

### Step 2: Get Your API Key

- Inside the Parking Space Detection page, navigate to **"Get Started"** on the left panel.
- Your **API Key** will be displayed there — copy and save it.
- Adjust the **confidence level** based on your accuracy requirements.

> 📊 **API Limits:** 15 requests/day and 100 requests/month on the free tier.

---

### Step 3: Test the API Virtually

- Use the **"Try API"** feature on the dashboard.
- Upload an image of a parking area with a mix of occupied and empty slots.
- Click **"Run Test"** — within seconds, the system displays:
  - Number of **filled slots**
  - Number of **empty slots**
- Test with different images to evaluate detection accuracy before deploying hardware.

> **⚠️ Note:** Each "Try API" test counts toward your daily/monthly API usage limit.

---


## 📊 Output

After pressing the push button, the Serial Monitor displays:

```
Connecting to WiFi...
WiFi Connected!
car detected - Capturing Image...
Image Captured. Sending to API...

--- Parking Space Detection Result ---
Total Spaces Detected: 10
  Occupied Slots : 7  (Confidence: 96.3%)
  Empty Slots    : 3  (Confidence: 94.1%)

Parking Status: availble
Gate open
```

> The result includes **occupied count**, **empty count**, and the **confidence score** for each category.

---

## ✅ Advantages & Limitations

| S.No | Advantages | Limitations |
|------|------------|-------------|
| 1 | Real-time parking detection within seconds | Cannot work without cloud API access |
| 2 | Low-cost system using ESP32-CAM with built-in camera & Wi-Fi | Requires an active internet connection |
| 3 | No expensive hardware or powerful processors needed | Blurry images may produce incorrect results |
| 4 | Fully wireless communication without extra modules | Limited by daily/monthly API usage limits |
| 5 | Small size and portable design | Captures single images, not continuous live video |

> **Why CircuitDigest Cloud over alternatives like Edge Impulse?**
> Edge Impulse requires dataset collection, model training, optimization, and deployment — time-consuming and complex. CircuitDigest Cloud provides a **ready-to-use API** that eliminates all of that, reducing development time and allowing focus on system integration rather than AI model design.

---

## 🛠️ Troubleshooting

### 🔇 Issue 1: No Output in Serial Monitor
- **Cause:** Incorrect COM port or baud rate setting.
- **Fix:** Set baud rate to **115200**, verify the correct COM port in Arduino IDE, and confirm the USB cable and board are properly connected.

### 🔄 Issue 2: ESP32-CAM Restarting Continuously
- **Cause:** Insufficient or unstable power supply.
- **Fix:** Use a proper **5V regulated external power source**. Avoid relying only on weak USB connections and check for loose wiring.

### 🚫 Issue 3: API Usage Limit Exceeded
- **Cause:** Too many test requests consumed the daily/monthly quota.
- **Fix:** Check your usage in the CircuitDigest Cloud dashboard. Wait for the limit to reset or upgrade your plan.

### 📷 Issue 4: Image Capture Failure
- **Cause:** Loose camera connections or memory limitations.
- **Fix:** Ensure the camera module is **securely connected**. Try reducing image resolution (e.g., VGA) to avoid memory-related issues.

### 🌐 Issue 5: API Connection Error or Timeout
- **Cause:** Unstable internet connection, invalid API key, or incorrect server configuration.
- **Fix:** Verify your internet connection, double-check the **API key**, and ensure HTTPS is properly configured in the code.

### 🔢 Issue 6: Incorrect Detection Results
- **Cause:** Poor image quality, bad lighting, or low confidence threshold.
- **Fix:** Use clear images with proper lighting. Adjust the **confidence level** in the CircuitDigest Cloud dashboard for better accuracy.

---

## ❓ FAQ

**1. Why is ESP32-CAM used in this project?**
> ESP32-CAM has a built-in camera module and Wi-Fi capability, making it ideal for capturing and transmitting images over the internet. It is cost-effective and perfect for IoT-based image processing applications.

**2. Why is the cloud API used instead of local processing?**
> The ESP32-CAM has limited memory and processing power, which makes running complex AI models locally impractical. The cloud API performs heavy inference on powerful servers, ensuring better accuracy and real-time performance.

**3. How accurate is the parking detection system?**
> Accuracy depends on image quality, lighting conditions, and camera positioning. Clear images with good lighting and fully visible parking slots significantly improve detection accuracy.

**4. Can this system work without the internet?**
> No. The system requires an active internet connection because all image processing is performed on the cloud server. Without internet, the ESP32-CAM cannot send data to the API.

**5. What are the limitations of this system?**
> The system depends on internet connectivity and API usage limits. It may also produce incorrect results if image quality is poor or parking slots are not clearly visible in the captured image.

---

## 🔗 Relevant Links

- 📦 **GitHub Repository:** [Circuit-Digest/Parking-Detection-Using-ESP32-Cam](https://github.com/Circuit-Digest/Parking-Detection-Using-ESP32-Cam)
- ☁️ **CircuitDigest Cloud:** [circuitdigest.cloud](https://circuitdigest.cloud)
- 📡 [Real-Time Motion Detection with XIAO ESP32 & WhatsApp Alert](https://circuitdigest.com/microcontroller-projects/real-time-motion-detection-with-xiao-esp32-whatsapp-alert-system)
- 💬 [Send WhatsApp Messages using Arduino & CircuitDigest Cloud](https://circuitdigest.com/microcontroller-projects/send-whatsapp-messages-using-arduino-circuitdigest-cloud)
- 🍓 [Send WhatsApp Messages using Raspberry Pi Pico W](https://circuitdigest.com/microcontroller-projects/send-whatsapp-messages-using-raspberry-pi-pico-w)

---

## Link  For The Full Guide:

https://circuitdigest.com/microcontroller-projects/esp32-cam-parking-space-detection-system-using-circuitdigest-cloud

---

<p align="center">
  Made with ❤️ by <a href="https://circuitdigest.com">CircuitDigest</a> | Powered by <a href="https://circuitdigest.cloud">CircuitDigest Cloud AI</a>
</p>
