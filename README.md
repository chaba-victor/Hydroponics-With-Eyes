
# 🌱 Smart Hydroponics System with AI-Driven Plant Health Monitoring

An **IoT-enabled hydroponics system** that automates plant care (nutrients, water, lighting) and uses **machine learning** to detect plant health issues from leaf images.

---

## ✅ **Features**

* Automated control of **pH**, **EC**, **water level**, **lighting**, and **temperature**.
* **Camera-based plant health analysis** using a trained CNN.
* **Predictive nutrient dosing** based on growth stage.
* Remote monitoring via **web or mobile dashboard**.
* Integration with **Home Assistant** for smart home automation.

---

## 🛠 **Hardware Components**

| Component     | Description                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------------- |
| **MCU**       | ESP32-C6 (Wi-Fi + BLE + good processing for ML inference if TinyML is used)                         |
| **Sensors**   | DHT22 (Temp/Humidity), pH sensor, EC sensor, water level sensor, LDR (light intensity)              |
| **Camera**    | OV2640 (ESP32-CAM module) or Arducam Mini                                                           |
| **Actuators** | Submersible water pump, peristaltic pumps (for nutrients & pH adjustment), grow lights, exhaust fan |
| **Power**     | 12V DC supply + buck converter for 5V and 3.3V                                                      |
| **Extras**    | LCD (I²C) for local display, SD card slot for image/data logging                                    |

---

## 🔍 **System Architecture**

```txt
+-------------------------+
|      Cloud Server       | <-- Web/Mobile Dashboard
|  (Data Storage + API)   |
+-------------------------+
           ↑
           ↓ (MQTT/HTTP)
+-------------------------+
|      ESP32 Controller   |
|  (Sensor + Actuator IO) |
+-------------------------+
      ↑     ↑      ↑
     pH    EC     Camera
     Temp  LDR
     ...   ...
```

---

## 📸 **Machine Learning Workflow**

### **1. Data Collection**

* Capture images of plant leaves using the camera module.
* Store images locally (SD card) and sync to cloud for labeling.

### **2. Data Labeling**

* Categories: **Healthy**, **Nitrogen Deficiency**, **Phosphorus Deficiency**, **Potassium Deficiency**, **Pest Damage**, etc.
* Use tools like **LabelImg** or **Roboflow**.

### **3. Model Training**

* Use **TensorFlow/Keras** for CNN-based classification:

  * Base Model: **MobileNetV2** or **EfficientNet** (lightweight for edge devices).
  * Transfer learning for faster convergence.

### **4. Deployment**

* Two options:

  * **Cloud inference**: Send image to server → return prediction.
  * **Edge inference (TinyML)**: Quantize model with **TensorFlow Lite** and run on ESP32 or external AI accelerator (e.g., **Kendryte K210**).

---

## ⚙️ **Firmware Roadmap**

### **Tasks**

* **Sensor Reading Loop**:

  * pH, EC, Temp, Humidity, Water Level, Light.
* **Control Logic**:

  * Water pump ON/OFF.
  * Nutrient dosing via peristaltic pumps (controlled by PWM).
  * Grow lights schedule (timer + LDR feedback).
* **Camera Integration**:

  * Periodic image capture.
  * Upload via HTTP POST or MQTT.
* **Connectivity**:

  * Wi-Fi + MQTT for real-time data.
  * OTA firmware updates.
* **Local UI**:

  * Show key stats on LCD.

### **Libraries**

* `ArduinoJson` (data handling)
* `PubSubClient` (MQTT)
* `ESPAsyncWebServer` (local dashboard)
* `TFT_eSPI` (for display, if needed)
* `ESP32CAM` (for image capture)

---

## ☁️ **Cloud & Dashboard Setup**

* **Backend**: Node.js + Express (or Python Flask/FastAPI).
* **Database**: PostgreSQL or MongoDB for sensor logs.
* **MQTT Broker**: Mosquitto (self-hosted or cloud).
* **Image Analysis Service**:

  * REST API endpoint for ML model.
  * Could use **Flask + TensorFlow Serving** or **FastAPI + ONNX Runtime**.
* **Dashboard (Frontend)**:

  * **Next.js** or **React** for UI.
  * Charts for sensor data.
  * Alerts for anomalies (e.g., pH out of range).
  * Display plant health predictions (Healthy / Deficient / Pest).

---

## 📈 **Project Roadmap**

### **Phase 1: Core IoT System**

* ✅ Setup ESP32 for sensor reading + pump control.
* ✅ Implement MQTT and dashboard for real-time data.

### **Phase 2: Automation**

* ✅ Add logic for pH & EC regulation.
* ✅ Implement lighting & climate control.

### **Phase 3: Camera & Image Capture**

* ✅ Integrate ESP32-CAM for leaf images.
* ✅ Build local storage + cloud sync.

### **Phase 4: Machine Learning**

* ✅ Collect and label dataset.
* ✅ Train CNN model & deploy (cloud or edge).

### **Phase 5: Cloud Dashboard**

* ✅ Build responsive dashboard with analytics.
* ✅ Add AI-based plant health insights.

---

## 📚 **Skills You’ll Learn**

* Embedded systems (ESP32, sensors, actuators).
* IoT protocols (MQTT, HTTP).
* ML model training & edge deployment.
* Cloud backend & dashboard development.
* Practical application of biology in tech.

---

### 🔗 **Future Enhancements**

* Voice control (Alexa/Google Assistant).
* Automated nutrient mixing based on ML predictions.
* Integration with Home Assistant.
* Multi-plant setup with individual monitoring.

---
