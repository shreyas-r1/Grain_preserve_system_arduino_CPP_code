======================================
IoT Grain Handling & Preservation System
======================================

This project is an automated system designed to manage and preserve grain by monitoring environmental conditions and controlling material flow. It integrates a conveyor belt for grain transport with a climate control system to prevent spoilage. A cloud-based dashboard provides comprehensive remote monitoring and data analysis.

---
Features
---

* Real-Time Monitoring: Continuously acquires temperature and humidity data using DHT11 sensors.
* Automated Climate Control: Implements a closed-loop algorithm that automatically activates a ventilation system when moisture levels exceed a pre-defined threshold.
* Automated Grain Conveyance: Controls a conveyor belt mechanism for loading and unloading grain from storage.
* Cloud-Based Dashboard: Sends all sensor data and system status (fans, conveyor) to a custom ThingSpeak dashboard for remote monitoring.
* Dual-MCU Architecture: Leverages an Arduino for robust, real-time control logic and an ESP32 for powerful Wi-Fi connectivity and data handling.

---
System Architecture
---

1. Arduino (Control Unit):
   This is the brain of the physical control system. It reads data from the DHT11 sensors, runs the core control algorithms for both ventilation and the conveyor belt, and controls separate relays to activate the machinery.

2. ESP32 (Communication Gateway):
   This unit handles all network-related tasks. It connects to the local Wi-Fi network, collects sensor data, monitors the status of all mechanical systems, and periodically sends this complete dataset to the ThingSpeak cloud platform.

3. ThingSpeak (Cloud Platform):
   Acts as the remote dashboard for the project. It receives, logs, and visualizes the data sent from the ESP32, allowing for real-time monitoring and historical analysis.

---
Hardware Requirements
---

* Microcontrollers:
  - 1x Arduino board (e.g., Uno, Nano)
  - 1x ESP32 Development Board
* Sensors:
  - 1x or more DHT11 Temperature and Humidity Sensors
* Actuators & Control:
  - 2x Relay Modules (one for fans, one for the conveyor motor)
  - 1x or more Ventilation Fans
  - 1x Conveyor Belt System with Motor
* Other:
  - Breadboard and Jumper Wires
  - Dedicated power supplies

---
Setup and Configuration
---

Step 1: Configure ThingSpeak
1. Create a ThingSpeak account and sign in.
2. Create a new channel.
3. Enable and name at least four fields:
   - Field 1: Temperature (C)
   - Field 2: Humidity (%)
   - Field 3: Fan Status (1 for ON, 0 for OFF)
   - Field 4: Conveyor Status (1 for ON, 0 for OFF)
4. Go to the API Keys tab and copy your Write API Key.

Step 2: Program the Microcontrollers
1. For the ESP32 Code:
   Enter your Wi-Fi credentials and the ThingSpeak Write API Key.
   
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";
   String apiKey = "YOUR_THINGSPEAK_API_KEY";
   
   Upload the code to your ESP32 board.

2. For the Arduino Code:
   Set the moisture threshold for the ventilation system and implement the logic for controlling the conveyor belt.
   
   #define MOISTURE_THRESHOLD 65.0 // Example value
   
   Upload the code to your Arduino board.

---
How It Works
---

1. Power On: The system initializes and the ESP32 connects to Wi-Fi.
2. Climate Control: The Arduino continuously monitors humidity and activates the fans via a relay if the threshold is exceeded.
3. Material Handling: The Arduino listens for a command (e.g., a button press) to run the conveyor belt, activating its relay as needed.
4. Data Communication: The ESP32 reads the sensor data and the status of both relays.
5. Cloud Logging: The ESP32 sends all data points to your ThingSpeak channel.
6. Remote Monitoring: You can log into ThingSpeak from any device to view the live dashboard.
