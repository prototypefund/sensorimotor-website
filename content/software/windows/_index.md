Setup unter Windows

Unterstützte version: 7, 8, 10

Die Software besteht aus:

- "libsensorimotor", einer Core Library, geschrieben in C++
- "pysensorimotor", einem Python Wrapper für einfache Entwicklung.
- embedded-Firmware, welche auf dem Mikrocontroller läuft und nicht angepasst werden muss (aber kann)

Abhängigkeiten installieren:

- C und C++ Compiler: [mingw](https://osdn.net/projects/mingw/releases/) (latest stable version)
- [Python3.6+](https://www.python.org/downloads/windows/)
- [Scons](https://scons.org/pages/download.html) (Production version)
- [Git](https://git-scm.com/download/win)
- Development IDE (z.B. Code::Blocks))

Bibliotheken kompilieren:

Auschecken der letzten stabilen version ("master"), falls git in den PATH installiert wurde kann dies über das terminal passieren:
```bash
git clone https://git.suprememachines.de/supreme/libsensorimotor.git
```
Bauen mit scons, ebenfalls über das terminal.
```bash
scons
```

Verwenden der Bibliotheken:

## Python:

```python
from src.sensorimotor import Sensorimotor

# Strang representiert den RS232 Bus mit allen Motoren
motors = Sensorimotor(number_of_motors=2)

# Limitiere beide motoren auf eine schwache Spannung
motors.set_voltage_limit([0.55, 0.55])

# Aktiviere Motoren
motors.start()

# Fahre Position 0.0 mit beiden Motoren an
motors.set_position([0.0, 0.0])

# Erhalte ein Tupel mit den aktuellen Motorpositionen
motors.print_position(motors.get_position())

# Deaktiviere Motoren, Keine weiteren Bewegungen werden ausgeführt
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
