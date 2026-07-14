# Xiao Flight Computer - README

## 🌐 Network & Access Details (Wi-Fi & OTA)
* **Wi-Fi Network Name (SSID):** `XIAO_Flight_Data`
* **Wi-Fi Password:** `Password123`
* **Web Interface URL (Browser):** [http://192.168.4.1](http://192.168.4.1)
* **Wireless Flashing Network Name (IDE Ports):** `Xiao-Flight-Computer`
* **OTA Security Password:** `admin123`

---

## 🔌 Wiring Diagram & Pin Configuration
* **Status LED:**
  * Pin **D0** connected to the Anode (+) (via a 220-ohm resistor).
* **MicroSD Card Slot (SPI):**
  * **CS** ──> Pin **D2** (GPIO 21)
  * **MOSI** ──> Pin **D10** (MOSI)
  * **MISO** ──> Pin **D9** (MISO)
  * **SCK** ──> Pin **D8** (SCK)
* **Sensors (KX134 + MPU-9250 - Shared I2C):**
  * **SDA** ──> Pin **D4** (Shared between both sensors)
  * **SCL** ──> Pin **D5** (Shared between both sensors)
* **Power Supply:**
  * **VCC** (All components) ──> Pin **3.3V**
  * **GND** (All components) ──> Shared **GND** Pin

---

## 🕹️ Operating Instructions
*The system mode is determined by the board's orientation during boot-up.*

### 🚀 Flight Mode (Autonomous) - *Booted Right-Side Up*
* The system detects proper upright orientation and initializes a new `log_XXX.csv` file.
* Automatic high-speed data logging begins immediately at **1000 samples per second**.
* **Visual Indicator:** The status LED flashes rapidly (every 100 milliseconds).
* **Crash Protection:** At forces of **60G and above**, the log file is instantly locked to prevent any data corruption or loss in the event of a crash.

### 🛠️ Recovery & OTA Mode - *Booted Upside Down*
* The system bypasses data logging and launches the Wi-Fi network and web server.
* **Visual Indicator:** The status LED blinks at a slow, steady pace (1 second on, 1 second off).
* **Web Accidental Deletion Protection:** The "Wipe All SD Logs" button is locked by default. To format/clear the card, you must first check the confirmation checkbox, which dynamically enables the wipe button.

---

## 📊 Data File Columns (CSV Structure)
Each log file contains telemetry data formatted into the following schema:
`Timestamp_ms`, `AccelX_G`, `AccelY_G`, `AccelZ_G`, `GyroX_dps`, `GyroY_dps`, `GyroZ_dps`, `Velocity_m_s`, `Roll`, `Pitch`, `Yaw`
