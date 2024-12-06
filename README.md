# Salt Level Measurement System

This project uses an ESPHome configuration to monitor the salt level in a container using a Wemos D1 Mini (ESP8266) board. It integrates a VL53L0X distance sensor and provides visual feedback through RGB LEDs. Measurements can be triggered manually or via a button in the ESPHome interface.

---

## Features

- **Distance Measurement**: Uses a VL53L0X laser distance sensor to calculate the salt level.
- **Wi-Fi Connectivity**: Connects to your Wi-Fi for remote monitoring.
- **RGB Status Indicator**: Displays the sensor's status using RGB LEDs.
- **Manual and Automated Measurements**: Includes a button for manual measurements and periodic updates.
- **Fallback AP Mode**: Provides a fallback access point in case of Wi-Fi issues.
- **OTA Updates**: Supports over-the-air firmware updates for easy maintenance.

---

## Hardware Requirements

1. **Wemos D1 Mini (ESP8266)**
2. **VL53L0X Distance Sensor**
3. **RGB LED**
   - Red, Green, and Blue channels with resistors (if required)
4. **Push Button**
5. Connecting wires and breadboard (or soldered connections)

---

## Connections

### VL53L0X Distance Sensor

- **SDA (Data)**: Connect to D2 (GPIO4) on the Wemos D1 Mini.
- **SCL (Clock)**: Connect to D1 (GPIO5) on the Wemos D1 Mini.
- **VCC**: Connect to the 3.3V pin on the Wemos D1 Mini.
- **GND**: Connect to the GND pin on the Wemos D1 Mini.

### RGB LED

- **Red**: Connect to D5 (GPIO14) via a suitable resistor.
- **Green**: Connect to D6 (GPIO12) via a suitable resistor.
- **Blue**: Connect to D7 (GPIO13) via a suitable resistor.

### Push Button

- **One Terminal**: Connect to D3 (GPIO0).
- **Other Terminal**: Connect to GND.

---

## Configuration Overview

### Substitutions

- **`name`**: Internal name for the ESPHome node.
- **`friendly_name`**: Display name for the node.
- **`board`**: Specifies the board type (e.g., `d1_mini`).

### Main Components

1. **Wi-Fi Settings**:

   - Connects to the defined Wi-Fi SSID and password.
   - Provides a fallback access point in case of connection failure.

2. **I2C Configuration**:

   - Configures I2C communication for the VL53L0X sensor.

3. **Sensors**:

   - VL53L0X sensor with custom lambda to calculate the percentage based on distance.

4. **Status LED**:

   - RGB LED indicates the measurement status.

5. **Manual Button**:

   - Initiates a measurement when pressed.

6. **Interval Updates**:

   - Automatic updates every 20 seconds.

7. **Buttons**:

   - Manual measurement trigger.
   - Restart button for the ESPHome node.

---

## Usage

1. **Flashing the Firmware**:

   - Upload the ESPHome configuration to the Wemos D1 Mini.

2. **Connecting to Wi-Fi**:

   - Use the `captive_portal` to set up Wi-Fi credentials if not preconfigured.

3. **Operation**:

   - View the salt level readings in your ESPHome dashboard.
   - Trigger manual readings via the push button or the ESPHome dashboard.
   - Observe the status LED for real-time feedback.

---

## LED Status Indicators

- **Green (ON)**: Measurement successful.
- **Red (ON)**: Sensor idle or error.
- **Blinking Red/Green**: Measurement in progress.

---

## Troubleshooting

1. **Wi-Fi Connection Issues**:

   - Use the fallback access point to reconnect.

2. **Sensor Not Responding**:

   - Verify I2C connections and ensure the VL53L0X sensor is powered.

3. **LED Not Working**:

   - Check RGB LED connections and resistor values.

---

## Secrets

Ensure the following secrets are defined in your ESPHome secrets file:

- `wifi_ssid`
- `wifi_password`
- `salt_level_ap_password`
- `salt_level_api_encryption_key`
- `salt_level_ota_password`

---

## Additional Notes

- The lambda function for the sensor calculation assumes a barrel height of 100 units and a gap of 15 units. Adjust these values in the configuration if needed.
- Regularly update the ESPHome firmware to include the latest features and fixes.

---

Enjoy your automated salt level monitoring system.


## To-Do List

- Replace ESP8266 with an ESP32 (consider using an ESP32-C3 Supermini).
- Implement deep sleep mode to conserve power between measurements.
- Wake up the system using the momentary push button.
