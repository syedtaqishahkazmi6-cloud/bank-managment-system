# Smart Bank Safe 🏦🔒

An interactive, Arduino-based security system that uses a 4x4 matrix keypad for PIN entry, an OLED screen for user feedback, a servo motor for the locking mechanism, and a PIR sensor for intruder detection. 

## 🌟 Features
* **Interactive Display:** Provides real-time visual feedback (Welcome screen, PIN entry, Success/Denied messages, and Motion Warnings) using a 128x64 OLED.
* **Keypad Security:** Requires a 4-digit PIN (default: `1234`) to unlock the safe.
* **Auto-Locking Mechanism:** A servo motor opens the safe upon successful entry and automatically relocks it after 4 seconds.
* **Intruder Detection:** A PIR motion sensor monitors the area. If movement is detected, the system triggers a warning screen and flashes a visual/audio alarm.
* **Anti-Tamper Lockout:** If an incorrect PIN is entered 2 times, the system triggers a heavy alarm and temporarily locks out the user.
* **Audio/Visual Feedback:** Uses a Green LED for access granted, a Red LED for access denied/alarms, and a Buzzer for keystroke clicks and siren tones.

## 🛠️ Components Required
* 1x Arduino Uno
* 1x 4x4 Membrane Keypad
* 1x SSD1306 OLED Display (128x64, I2C)
* 1x Micro Servo Motor (e.g., SG90)
* 1x PIR Motion Sensor
* 1x Active Buzzer
* 1x Green LED (with 220Ω resistor)
* 1x Red LED (with 220Ω resistor)
* Jumper Wires & Breadboard

## 🔌 Pin Mapping (Wiring Guide)

| Component | Arduino Pin | Notes |
| :--- | :--- | :--- |
| **OLED SDA** | A4 | I2C Data |
| **OLED SCL** | A5 | I2C Clock |
| **Keypad Rows (R1-R4)** | 5, 4, 3, 2 | Digital Pins |
| **Keypad Cols (C1-C4)** | A3, A2, A1, A0 | Analog Pins (Used as Digital) |
| **Servo Motor (PWM)** | 9 | Controls locking mechanism |
| **PIR Sensor (OUT)** | 13 | Motion detection signal |
| **Buzzer (+)** | 12 | Audio feedback |
| **Red LED (+)** | 11 | Access Denied / Alarm indicator |
| **Green LED (+)** | 10 | Access Granted indicator |

*(Note: Ensure all components share a common Ground (GND) with the Arduino, and the OLED/Servo/PIR receive 5V power).*

## 📚 Libraries Required
To compile this code, you must install the following libraries via the Arduino IDE Library Manager:
* `Wire.h` (Built-in)
* `Servo.h` (Built-in)
* `Keypad` by Mark Stanley, Alexander Brevig
* `Adafruit SSD1306` by Adafruit
* `Adafruit GFX Library` by Adafruit

## 🚀 How to Use the System

1. **Power On:** Upon booting, the OLED will display "SMART BANK SAFE" and initialize the components. Give it about 2 seconds to stabilize.
2. **Enter PIN:** The screen will prompt "ENTER PIN:". Use the keypad to type your 4-digit code.
    * *Default PIN:* `1234`
    * *Clear Input:* Press the `*` key to erase your current input and start over.
3. **Access Granted:** If the PIN is correct, the Green LED lights up, the OLED says "GRANTED", and the Servo rotates 90° to open the safe. It will close automatically after 4 seconds.
4. **Access Denied:** If the PIN is wrong, the Red LED lights up, a low buzzer sounds, and the attempt is recorded. 
5. **Lockout:** Failing to enter the correct PIN 2 times will trigger a loud system lock alarm. 
6. **Motion Alert:** If the PIR sensor detects movement at any time, the screen flashes "WARNING!" and the buzzer pulses until the motion stops.

## 🔧 Customization
To change the default password or the maximum allowed failed attempts, simply modify these variables at the top of the `sketch.ino` file:
```cpp
const String CORRECT_PIN = "1234"; // Change your PIN here
const int MAX_ATTEMPTS = 2;        // Change lockout threshold

## Wokvi link https://wokwi.com/projects/460658892848908289

