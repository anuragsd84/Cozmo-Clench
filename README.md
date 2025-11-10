Cozmo-Clench – RC Controlled Robot

A high-power RC-controlled robot built using 4 Johnson motors, an L298N motor driver, and a dual-claw mechanism.
The robot is controlled using PWM signals from an EPW6 receiver + Radiomaster transmitter, supporting:

Differential drive

Independent dual claw motors

Automatic failsafe

Dead-zones for smooth response

Full ±255 speed mapping

This repository contains the Arduino firmware that powers the complete system.

✅ Hardware Used

4× Johnson Motors

2 × Drive motors

2 × Claw motors

L298N Motor Driver (Dual H-Bridge)

Radiomaster Transmitter

EPW6 / Any PWM RC Receiver

Arduino UNO / Nano

3S 2200mAh Li-Po Battery

Chassis, wiring, connectors, etc.


✅ Receiver → Arduino Pin Mapping

RC Channel	Arduino Pin	        Purpose
Throttle	    D3	        Forward / Backward
Direction 	  D6	        Left / Right steering
Claw Motor1 	D9	        Open / Close Claw 1
Claw Motor2	  D11	        Open / Close Claw 2

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
Claw 1	        2	        4
Claw 2	        7       	8

✅ Features

✅ Smooth differential drive

✅ Full RC PWM decoding using pulseIn()

✅ Failsafe: invalid PWM defaults to 1500 µs

✅ Dead-zone filtering to prevent jitter

✅ Dual independent claw motors

✅ 1000–2000 µs mapped to −255 → +255 motor PWM

✅ Stable 20 ms loop timing

✅ RC Signal Processing

✅ 1. Pulse Reading

Each RC channel is read using:

pulseIn(pin, HIGH);


Invalid signals (<900 or >2100) are replaced with 1500 µs (neutral).


✅ 2. Mapping to Motor Speed

Throttle and direction values are converted to speed:

map(pulse, 1000, 2000, -255, 255);

✅ 3. Differential Drive Mixing
left_speed  = throttle + direction;
right_speed = throttle - direction;


Values are constrained to −255…255.

✅ 4. Claw Motor Control

Simple threshold-based logic:

> 1800 µs → Forward

< 1200 µs → Reverse

Otherwise → Stop

✅ How To Use

Connect all RC channels to pins 3, 6, 9, 11.

Connect motors & L298N exactly as per pin tables above.

Power the L298N with a 3S Li-Po (12.6V).

Power the Arduino using a stable 5V regulator.

Upload the firmware: clench_robot.ino.

Turn ON the RC transmitter → power the robot.

Controls:

Right stick up/down → forward/back

Right stick left/right → turning

AUX channels → claw opening/closing


✅ Safety Notes

Use common GND for Arduino, receiver, and L298N.

Never power Arduino directly from the Li-Po.

Test with wheels lifted before first run.

L298N may heat under load → heatsink recommended.

Author

Anurag Deshmukh
Embedded Systems • Robotics • Automation
