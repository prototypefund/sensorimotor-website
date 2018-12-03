+++
title = "Linux"
+++
Setup on Debian

supported version: 9 (Stretch)

The software consists of 
- "libsensorimotor", a core library, written in C++
- "pysensorimotor", a Python wrapper for easy development
- embedded-firmware, which runs on the micro-controller and doesn't need to be modifyed (but can)

Dependencies:

- C and C++ Compiler: `sudo apt install build-essential`
- Python3.6+ `sudo apt install python3-dev`
- Scons `sudo apt install scons`

compile libraries:

```debian
# check out the latest stable version ("master")
git clone https://git.suprememachines.de/supreme/libsensorimotor.git
# go to project directory
cd libsensorimotor
# build
scons
```

library use:

## Python:

```python
from src.sensorimotor import Sensorimotor

# Motors represents the RS485 Bus with all motors
motors = Sensorimotor(number_of_motors=2)

# Limit both motors to low voltage
motors.set_voltage_limit([0.55, 0.55])

# Activate motors
motors.start()

# Move both motors to position 0.0
motors.set_position([0.0, 0.0])

# Get a tuple with actual motor-positions
motors.print_position(motors.get_position())

# Deactivate motors, no more movements will be executed
motors.stop()
```

An instance of the class `Sensorimotor` represents a strand of motors and controls the communication between them.

There are different modes that a motor can be in:

- Position -> target-position the motor the motor moves to
- Velocity -> target-velocity to be reached.
- Hold -> uses the delay-modus [CSL](#CSL)

The mode can be changed by sending the dedicated command. For example "set_position" automatically switches to popsition-mode.

additional commands that can be send to the motors:

- `set_voltage_limit` Limit the output voltage to the motor (p.e. if you want to use a 5V-motor)
- `set_limits` limits the range of motion of your servo.

## C++

The same methods are defined in the 'sensorimotor.so' library, therefor the usage is analogous to the python library

```cpp
```