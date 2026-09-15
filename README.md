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
