+++
title = "Windows"
+++
Setup on a Windows system

supported version: 7, 8, 10.

The software consists of 
- "libsensorimotor", a core library, written in C++
- "pysensorimotor", a Python wrapper for easy development
- embedded-firmware, which runs on the micro-controller and doesn't need to be modifyed (but can)

Dependencies:

- C and C++ Compiler: [mingw](https://osdn.net/projects/mingw/releases/) (latest stable version)
- [Python3.6+](https://www.python.org/downloads/windows/)
- [Scons](https://scons.org/pages/download.html) (Production version)
- [Git](https://git-scm.com/download/win)
- Development IDE (z.B. Code::Blocks))

compile libraries:

check out the latest stable version ("master")
if git is installed at $PATH you can do that with the following terminal command:
```bash
git clone https://git.suprememachines.de/supreme/libsensorimotor.git
```
build with scons, terminal command:
```bash
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

Die `Sensorimotor` Klasse dient als Einstiegspunkt, und bildet den Motorstrang ab.

Jeder motor kann sich in einem der verschiedenen Modi befinden:

- Position gibt die anzufahrende Position an, die der Motor versuchen wird zu erreichen
- Velocity gibt eine konstante Geschwindigkeit an, welche erreicht werden soll.
- Hold verwendet den Verzögerungsmodus [CSL](#CSL)

Der Modus kann gewechselt werden, indem ein jeweiliger Befehl gesendet wird. Beispielsweise wechselt set_position automatisch in den Positionsmodus.

zusätzlich können dem Motor limits übergeben werden:

- `set_voltage_limit` regelt die Maximal abgegebene Spannung.
- `set_limits` beschränkt den maximal möglichen Bewegungsbereich des Servos.

## C++

Die gleichen methoden werden in der 'sensorimotor.so' Bibliothek definiert, daher ist die verwendung Analog zu den Beispielen oben.

```cpp
```
