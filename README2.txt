# RFID Secure Relay Terminal 🛡️💳

An industrial-style access control system built with an Arduino Uno. This project uses an MFRC522 RFID scanner to grant access to a high-power relay module, monitored by an SSD1306 OLED screen and protected by a PIR motion sensor.

## 🌟 Features
* **Biometric-Style Access:** Uses RFID tags/cards instead of a keypad for fast, secure entry.
* **Specific Card Authorization:** The system checks the unique UID of the scanned card against an authorized "Master Card" database.
* **Relay Control:** Replaces a standard servo with a 5V Relay Module, allowing the system to control heavy-duty electronic door strikes, magnetic locks, or lighting.
* **Motion Security:** A PIR sensor actively monitors the area. If movement is detected, the OLED flashes a warning and triggers an audio alarm.
* **Visual & Audio Feedback:** Uses an OLED screen for status updates, a Green LED for approved access, a Red LED for denials/alarms, and an Active Buzzer for sound feedback.

## 🛠️ Components Required
* 1x Arduino Uno
* 1x MFRC522 RFID Reader
* 1x SSD1306 OLED Display (128x64, I2C)
* 1x 5V Relay Module
* 1x PIR Motion Sensor
* 1x Active Buzzer
* 1x Green LED & 1x Red LED (with 220Ω resistors)
* Jumper Wires & Breadboard

## 🔌 Pin Mapping (Strict SPI Protocol)

| Component | Arduino Pin | Notes |
| :--- | :--- | :--- |
| **RFID SCK** | 13 | Hardcoded SPI Pin |
| **RFID MISO** | 12 | Hardcoded SPI Pin |
| **RFID MOSI** | 11 | Hardcoded SPI Pin |
| **RFID SDA (SS)** | 10 | Slave Select |
| **RFID RST** | 9 | Reset Pin |
| **Relay Signal** | 8 | Triggers lock mechanism |
| **Green LED (+)** | 7 | Success Indicator |
| **Red LED (+)** | 6 | Error/Alarm Indicator |
| **Buzzer (+)** | 5 | Audio Feedback |
| **PIR Sensor** | 4 | Motion Signal |
| **OLED SDA / SCL**| A4 / A5 | I2C Communication |

*⚠️ Important: The MFRC522 must be powered by the 3.3V pin. Connecting it to 5V will damage the sensor.*

## 🚀 Setup & Usage

1. **Find Your Card's UID:** * Wire the system and upload the code.
   * Open the Arduino IDE Serial Monitor (115200 baud rate).
   * Scan the physical card you want to be the "Master Key" (e.g., your Blue Card).
   * Note the Hexadecimal code printed in the console (e.g., `DE AD BE EF`).
2. **Update the Code:**
   * Open `sketch.ino` and replace the placeholder array `byte authorizedUID[4]` with your card's numbers.
   * Re-upload the code.
3. **Run the System:**
   * The screen will display "SECURE TERMINAL".
   * **Authorized Card:** Triggers the Green LED, sounds a happy tone, and activates the Relay for 5 seconds.
   * **Unauthorized Card:** Triggers the Red LED, sounds a low error tone, and displays "DENIED!".
   * **Motion Detected:** Flashes a warning on the OLED, lights the Red LED, and sounds a pulsing alarm until movement stops.

Wokvi Link : https://wokwi.com/projects/460738515475162113