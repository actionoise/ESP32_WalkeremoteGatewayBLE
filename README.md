# ESP32 BLE Controller

ESP32 Bluetooth Low Energy (BLE) project for low-latency communication with a smartphone.

This project allows an ESP32 to receive commands via BLE, display the received data on the Serial Monitor and immediately send an acknowledgement back to the connected device.

The current version is mainly designed for communication and latency testing, but it can be easily extended to control motors, relays, lights, servos and robotic platforms.

---

## How it works

The ESP32 creates a Bluetooth Low Energy device called:

`ESP32-Latency`

A smartphone can connect to the ESP32 and send commands through a custom BLE characteristic.

Example:

Phone -> FORWARD  
ESP32 -> ACK:FORWARD

Every received command is also displayed on the Arduino Serial Monitor together with the reception time in microseconds.

This makes it possible to test the communication delay between the smartphone and the ESP32.

---

## BLE Configuration

Device name:

`ESP32-Latency`

Service UUID:

`12345678-1234-1234-1234-1234567890ab`

Characteristic UUID:

`abcdefab-1234-5678-1234-abcdefabcdef`

The BLE characteristic supports:

- READ
- WRITE
- WRITE WITHOUT RESPONSE
- NOTIFY

---

## Example communication

The smartphone sends:

`FORWARD`

The ESP32 receives the command and prints it on the Serial Monitor.

Then the ESP32 immediately replies:

`ACK:FORWARD`

The acknowledgement can be used by the smartphone application to measure the round-trip latency.

---

## Possible applications

The BLE communication layer can be connected to ESP32 GPIO outputs and used in many different projects.

Possible applications include:

- DC motor control
- Robot movement
- Motor drivers
- Relay control
- LED control
- Lighting systems
- Servo motors
- PWM speed control
- Robotic vehicles
- Telepresence robots
- Robot vacuum modifications
- Remote control systems
- DIY automation projects

Compatible motor drivers may include:

- L293D
- L298N
- TB6612FNG
- BTS7960

---

## Example commands

Possible commands sent from the smartphone:

- FORWARD
- BACKWARD
- LEFT
- RIGHT
- STOP
- RELAY_ON
- RELAY_OFF
- LIGHT_ON
- LIGHT_OFF
- SERVO:90
- SPEED:200

These commands can be interpreted by the ESP32 and converted into GPIO or PWM signals.

---

## Example hardware implementation

Inside the BLE `onWrite()` callback, commands can be connected to real hardware.

Example:

```cpp
if (value == "FORWARD") {
  digitalWrite(MOTOR_A1, HIGH);
  digitalWrite(MOTOR_A2, LOW);
}

else if (value == "BACKWARD") {
  digitalWrite(MOTOR_A1, LOW);
  digitalWrite(MOTOR_A2, HIGH);
}

else if (value == "STOP") {
  digitalWrite(MOTOR_A1, LOW);
  digitalWrite(MOTOR_A2, LOW);
}

else if (value == "RELAY_ON") {
  digitalWrite(RELAY_PIN, HIGH);
}

else if (value == "RELAY_OFF") {
  digitalWrite(RELAY_PIN, LOW);
}
```

---

## Android APK available for installation

the app apk file for android is available 
on this repo or on PlayStore in this link :


https://play.google.com/store/apps/details?id=appinventor.ai_miktavol.WalkeremoteBLETest1_V11_WSS_FINAL


The app has been designed to work **in the background** and remains active until the user explicitly closes it. This allows it to keep running even when the smartphone display is turned off.

The main goal is to **reuse an old Android smartphone as a gateway**, instead of adding more electronic waste. Smartphones contain batteries, electronic circuits, and several materials that can be difficult to dispose of properly and may have an environmental impact when they unnecessarily become waste.

The smartphone can receive data and commands from an **MQTT broker** through Wi-Fi or the mobile network and forward them via **Bluetooth** to compatible hardware devices such as:

* ESP32
* Bluetooth development boards
* microcontrollers with Bluetooth support
* prototypes and experimental electronic systems

In this way, the smartphone can act as a bridge between the Internet and local hardware.

For example, incoming commands can be used to control:

* motors
* motor drivers
* relays
* servomotors
* PWM outputs
* digital outputs
* other actuators

At the same time, the hardware device can send data back to the smartphone from:

* sensors
* digital inputs
* analog inputs
* monitoring systems
* IoT devices

Another important advantage is related to the phone's physical connection.

On many smartphones, it can be inconvenient or difficult to **keep the device charging while using the USB port at the same time for communication with external hardware**.

By using **Bluetooth** for communication with an ESP32 or other boards, the phone's USB port can remain dedicated entirely to charging.

This makes it possible to keep the smartphone powered and operational for long periods of time, making it suitable for use as a **permanent or semi-permanent IoT gateway**.

The smartphone can therefore make use of its existing hardware capabilities again, including:

* Wi-Fi
* mobile network
* Bluetooth
* battery
* processor
* Android operating system

turning it into a real **reusable IoT gateway**.

In many experimental projects, this approach can remove the need for a dedicated gateway with its own modem or SIM card, allowing an old Android device that is already available to be reused instead.

The basic idea of the project is simple:

**Internet / MQTT Broker → Android Smartphone → Bluetooth → ESP32 / Hardware**

and in the opposite direction:

**Sensors / Hardware → Bluetooth → Android Smartphone → MQTT Broker / Internet**

In this way, an old smartphone can become useful again in IoT, robotics, home automation, and experimental projects, extending its useful life while also helping reduce electronic waste.



