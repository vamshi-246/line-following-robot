# Line Follower Robot

This project demonstrates the development of a **Line Follower Robot** as part of the AI for Robotics hardware challenge series. The robot is designed to follow a black line on a white surface using infrared sensors and is controlled using an Arduino-based proportional controller.

---

## 📁 Source Code

The Arduino source code is organized into two main files:

- `motors.ino`: Implements basic motor control (Hardware Challenge #2).
- `p_controller.ino`: Implements the proportional control logic for line following (Hardware Challenge #3).

---

## 🧰 Hardware Challenge #0: Component Acquisition

All essential electronic and mechanical components required to build the robot were procured:

- Transparent plastic chassis  
- 4 DC motors with wheels  
- L298N dual H-bridge motor driver module  
- Arduino Uno  
- 5 × TCRT5000 infrared sensor modules  
- 5 × LEDs with corresponding resistors  
- Mini breadboard  
- Battery holders and 3 × batteries  
- USB cable for Arduino programming  
- Jumper wires, screws, and bolts  

![Hardware Challenge 0](images/hardware-challenge-0.jpg)

---

## 🧠 Hardware Challenge #1: Environmental Sensing

The robot uses 5 TCRT5000 infrared sensors to detect the contrast between a black line and the white floor. Each sensor setup includes:

- A TCRT5000 module  
- A resistor and an LED  
- Power (5V), Ground, and Signal connections  

The analog signal from each sensor is read using `analogRead()` on the Arduino. The sensor readings typically return:

- ~400 for black (line detected)  
- ~20 for white (no line)  

These values help determine the presence and position of the line. The LED visually indicates detection — ON for black and OFF for white.

📽️ **Video Demonstration:**  
[![Hardware Challenge 1](images/hardware-challenge-1.png)](https://youtu.be/YxFP9dMudcE)

---

## 🛞 Hardware Challenge #2: Controlled Movement

Motor control is handled through the L298N dual H-bridge driver connected to the Arduino. Each side of the robot consists of two motors wired in parallel, meaning:

- ENA/ENB pins control speed using PWM signals  
- IN1/IN2 and IN3/IN4 control motor direction  
- Motor direction logic is adjusted due to the physical motor layout  

An interesting observation: when manually rotating one motor, the paired motor moves due to back EMF, demonstrating electrical and mechanical coupling.

📽️ **Video Demonstration:**  
[![Hardware Challenge 2](images/hardware-challenge-2.png)](https://youtu.be/lya-ddb5DFg)

---

## ⚙️ Hardware Challenge #3: Proportional Control (P-Controller)

The core logic for line following is based on a simple **P-Controller**.

### Working Principle:
- Each of the 5 sensors contributes a weight to a variable `line`:
  - Sensor weights: `[-4, -2, 0, 2, 4]`
- If a sensor detects the line, its weight is added to `line`
- `line` is then averaged over the number of active sensors
- The final value of `line` ranges from -4 to 4

### Modes of Operation:

**1. Tracking Mode (1–2 sensors active):**
- The robot is on track  
- Motors are adjusted proportionally — one motor slows down to correct the course  
- `LED_BUILTIN` is turned ON  

**2. Recovery Mode (0 or all 5 sensors active):**
- The robot has lost the line  
- It rotates in place toward the last known direction (based on previous `line` value)  
- `LED_BUILTIN` is turned OFF  

### Why Only P (Proportional) Control?
- **Integral** term is not required due to negligible drift  
- **Derivative** term is not required since oscillations are minimal  
- Simple P-control is sufficient to keep the robot stable and responsive

📽️ **Video Demonstration:**  
[![Hardware Challenge 3](images/hardware-challenge-3.png)](https://youtu.be/DaOiyH9NtPE)

---

## ✅ Summary

This project integrates sensor data acquisition, motor control, and feedback-based navigation to build an autonomous line-following robot. It progresses through a structured development process using affordable and widely available components.

---
