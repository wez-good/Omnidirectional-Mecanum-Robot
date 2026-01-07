# Omnidirectional-Mecanum-Robot
This project features an Arduino-based Mecanum wheel robot controlled via an RC Receiver. It uses specialized kinematics to move in any direction—forward, backward, sideways (strafing), and rotation.

# 🛠️ Hardware Requirements
This project is a fully custom-built mechatronic system.

3D Printed Components: The chassis, motor mounts, platform for electronics, and the Mecanum wheels themselves were custom 3D printed to reduce weight and allow for modular component mounting.

Microcontroller: Arduino Uno R3.

Motor Drivers: 2x L298N Dual H-Bridge Modules.

Motors: 4x DC Gear Motors.

Control: 3+ Channel RC Receiver (PWM).

Power: 12V LiPo Battery (Motors) + 5V Regulator (Arduino).

# 🔌 Wiring Configuration
To ensure smooth speed control, all motor PWM pins are connected to the Arduino's hardware timers.

| Position    |   Motor |  Arduino PWM |  Logic IN 1 |  Logic IN 2 |
|-------------|---------|--------------|-------------|-------------|
| Front Left  |  M1     |   Pin 5      |   Pin 4     |  Pin 7      |
| Front Right |  M2     |   Pin 6      |   Pin 8     |  Pin A0     |
| Back Left   | M3      |  Pin 9       |  Pin A1     |  Pin A3     |
| Back Right  | M4      |  Pin 10      |  Pin A4     |  Pin A5     |

| RC Channel  |   Function       |   Arduino Pin |
|-------------|------------------|---------------|
| CH1         | Strafe (X-Axis)  |   Pin 2       |
| CH2         | Forward (Y-Axis) |   Pin 3       |
| CH4         | Rotation (Yaw)   |   Pin 11      |

# 📐 Kinematics & Logic
The robot uses a vector addition matrix to translate 3-axis input ($X, Y, R$) into 4 individual wheel speeds.

| The Math       |
|----------------|
| M1 = Y + X + R |
| M2 = Y - X - R |
| M3 = Y - X + R |
| M4 = Y + X - R |

Feature Optimizations
Speed Cap: Limited to 200/255 to prevent the L298N drivers from overheating and to keep the robot controllable.

Min-Kick Logic: Automatically boosts low PWM signals to a minimum threshold (45) to overcome motor gearbox friction.

Deadzone: A software deadzone of 35 prevents "creeping" when the RC sticks are at rest.

# 📜 License
This project is open-source and available under the MIT License.

