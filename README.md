# Cozmo-Clench
Cozmo Clench – RC Controlled Robot

A high-power RC-controlled robot built using 4 Johnson motors, an L298N motor driver, and a dual-claw mechanism.
The robot is controlled through PWM signals from an EPW6 receiver + Radiomaster transmitter, supporting:

Differential drive

Independent dual claw motors

Automatic failsafe

Dead-zones for smooth response

Full ±255 speed mapping

This repository contains the Arduino firmware that powers the complete system.

✅ Hardware Used

4× Johnson Motors

2 for drive

2 for claw actuation

L298N Motor Driver (dual H-bridge)

Radiomaster Controller

EPW6 / any PWM RC Receiver

Arduino UNO / Nano

3S 2200mAh Li-Po Battery

Jumper wires, chassis, connectors, etc.

✅ Receiver → Arduino Pin Mapping
RC Channel	Arduino Pin	Purpose
Throttle	D3	Forward / Backward
Direction	D6	Left / Right steering
Claw Motor 1	D9	Open / Close Claw 1
Claw Motor 2	D11	Open / Close Claw 2
✅ Motor Driver Pin Mapping
Drive Motors (L298N)
Function	Arduino Pin
IN1 — Left Forward	A1
IN2 — Left Reverse	A2
ENA — Left PWM	10
IN3 — Right Forward	A3
IN4 — Right Reverse	A4
ENB — Right PWM	5
Claw Motors
Claw Motor	Forward Pin	Reverse Pin
Claw 1	2	4
Claw 2	7	8
✅ Features

✅ Differential drive with smooth steering

✅ Full RC PWM decoding via pulseIn()

✅ Robust failsafe if signal is out of valid range

✅ Dead-zone filtering to prevent jitter

✅ Two fully independent claw motors

✅ 1000–2000 µs mapped to −255 → +255 speed

✅ 20 ms loop for stable operation

✅ RC Signal Processing
✅ 1. Pulse Reading

Each input is read using:

pulseIn(pin, HIGH);


Invalid pulses (<900 or >2100) → replaced with 1500 µs (neutral).

✅ 2. Mapping to Motor Speed

Throttle & direction stick positions → mapped to speed:

map(pulse, 1000, 2000, -255, 255);

✅ 3. Differential Drive Mixing
left_speed  = throttle + direction;
right_speed = throttle - direction;


Speeds are then constrained to −255..255.

✅ 4. Claw Motor Logic

Threshold-based simple control:

> 1800 µs → Forward

< 1200 µs → Reverse

Else → Stop

✅ How To Use

Wire the receiver to pins 3, 6, 9, 11.

Connect drive motors and claw motors to L298N as per tables above.

Power L298N with 3S Li-Po (12.6V).

Power Arduino using stable 5V regulator.

Upload the Arduino firmware (clench_robot.ino).

Power ON transmitter → power ON robot.

Controls:

Right stick up/down → forward/back

Right stick left/right → turning

AUX switches → control claws (open/close)

✅ Safety Notes

Ensure common ground between receiver, Arduino, and drivers.

Do not power Arduino directly from Li-Po.

Lift wheels during your first test.

L298N may heat at high loads → add heatsinks if needed.



 **Author**

Anurag Deshmukh
Embedded Systems • Robotics • Automation
