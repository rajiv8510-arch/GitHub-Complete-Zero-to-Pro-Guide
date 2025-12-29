# Templates - Arduino Git Projects

**Ready-to-use templates for libraries and projects**

---

## .gitignore Template

**Purpose:** Exclude build files, IDE files, OS files

**Location:** Root of repository

```gitignore
# Compiled Arduino files
*.hex
*.elf
*.eep
*.lss
*.map
*.sym
*.o
*.a
*.bin
*.d

# Build directories
build/
*.build/

# Arduino IDE
.arduino/
__vm/

# Visual Studio Code
.vscode/
*.code-workspace

# Arduino CLI
.cli-config.yml

# PlatformIO
.pio/
.pioenvs/
.piolibdeps/

# JetBrains IDEs
.idea/
*.iml
cmake-build-*/

# Eclipse
.cproject
.project
.settings/

# Atmel Studio
*.atsln
*.atsuo
*.atsproj
Debug/
Release/

# macOS
.DS_Store
.AppleDouble
.LSOverride
._*

# Windows
Thumbs.db
ehthumbs.db
Desktop.ini
$RECYCLE.BIN/

# Linux
*~
.directory

# Logs
*.log

# Temporary files
*.tmp
*.temp
*.bak
*.swp

# Documentation build
docs/_build/
docs/.doctrees/

# Python (if using scripts)
__pycache__/
*.py[cod]
venv/
env/

# Personal notes
TODO.txt
NOTES.md
scratch/

# Libraries (document installation instead)
# Uncomment if you want to exclude libraries folder
# libraries/
```

---

## library.properties Template

**Purpose:** Arduino library metadata

**Location:** Root of library repository

```properties
name=LibraryName
version=1.0.0
author=Rajiv Yadav
maintainer=Rajiv Yadav <your.email@example.com>
sentence=Short one-line description of library functionality
paragraph=Longer detailed description explaining what this library does, its key features, and main use cases. Keep it concise but informative.
category=Device Control
url=https://github.com/rajiv8510-arch/Arduino-Library-LibraryName
architectures=*
depends=
```

**Categories:**
- `Device Control` - Relay, motor, actuator control
- `Signal Input/Output` - Digital I/O, buttons, switches
- `Sensors` - Temperature, pressure, level sensors
- `Communication` - Serial, I2C, SPI, WiFi
- `Data Processing` - Algorithms, calculations
- `Timing` - Timers, delays, scheduling
- `Data Storage` - EEPROM, SD card, logging
- `Display` - LCD, LED, OLED displays

**Dependencies:**
```properties
# Single dependency
depends=Wire

# Multiple dependencies
depends=Wire,SPI,Adafruit_GFX

# No dependencies
depends=
```

---

## Library Structure Template

**Purpose:** Standard Arduino library organization

```
LibraryName/
├── src/
│   ├── LibraryName.h           ← Main header
│   ├── LibraryName.cpp         ← Implementation
│   └── config.h                ← Configuration (optional)
├── examples/
│   ├── BasicExample/
│   │   └── BasicExample.ino
│   └── AdvancedExample/
│       └── AdvancedExample.ino
├── docs/
│   ├── README.md
│   └── API.md
├── library.properties
├── README.md
├── LICENSE
└── .gitignore
```

---

## Library Header Template (.h)

**File:** `src/LibraryName.h`

```cpp
#ifndef LIBRARY_NAME_H
#define LIBRARY_NAME_H

#include <Arduino.h>

class LibraryName {
public:
    // Constructor
    LibraryName(uint8_t pin);
    
    // Initialization
    void begin();
    
    // Main functionality
    void doSomething();
    bool checkStatus();
    
    // Getters
    uint8_t getPin() const;
    
    // Setters
    void setPin(uint8_t pin);

private:
    uint8_t _pin;
    bool _initialized;
    
    // Private helper methods
    void _internalHelper();
};

#endif // LIBRARY_NAME_H
```

---

## Library Implementation Template (.cpp)

**File:** `src/LibraryName.cpp`

```cpp
#include "LibraryName.h"

LibraryName::LibraryName(uint8_t pin) 
    : _pin(pin), _initialized(false) {
}

void LibraryName::begin() {
    pinMode(_pin, OUTPUT);
    _initialized = true;
}

void LibraryName::doSomething() {
    if (!_initialized) return;
    digitalWrite(_pin, HIGH);
}

bool LibraryName::checkStatus() {
    return digitalRead(_pin);
}

uint8_t LibraryName::getPin() const {
    return _pin;
}

void LibraryName::setPin(uint8_t pin) {
    _pin = pin;
}

void LibraryName::_internalHelper() {
    // Private implementation
}
```

---

## Library README Template

**File:** `README.md`

```markdown
# LibraryName

Brief description of what this library does.

## Features

- Feature 1 - Brief description
- Feature 2 - Brief description
- Feature 3 - Brief description

## Installation

### Arduino IDE

1. Download ZIP from [Releases](https://github.com/rajiv8510-arch/Arduino-Library-LibraryName/releases)
2. Arduino IDE → Sketch → Include Library → Add .ZIP Library
3. Select downloaded file

### Git Clone

```bash
cd ~/Documents/Arduino/libraries
git clone https://github.com/rajiv8510-arch/Arduino-Library-LibraryName.git
```

Restart Arduino IDE.

## Usage

### Basic Example

```cpp
#include <LibraryName.h>

LibraryName myDevice(13);  // Pin 13

void setup() {
    myDevice.begin();
}

void loop() {
    myDevice.doSomething();
    delay(1000);
}
```

### Advanced Example

See [examples/AdvancedExample](examples/AdvancedExample/AdvancedExample.ino)

## API Reference

### Constructor

```cpp
LibraryName(uint8_t pin)
```
- `pin`: Digital pin number

### Methods

#### `void begin()`
Initialize the library. Call in `setup()`.

#### `void doSomething()`
Perform main action.

#### `bool checkStatus()`
Returns current status.
- Returns: `true` if active, `false` otherwise

## Hardware Requirements

- Arduino Uno, Nano, or compatible
- Component connected to digital pin

## Wiring

```
Component Pin 1 → Arduino Pin X
Component Pin 2 → GND
Component Pin 3 → 5V
```

## Dependencies

- None (or list required libraries)

## Version History

### v1.0.0 (2024-XX-XX)
- Initial release
- Basic functionality

## License

MIT License - see [LICENSE](LICENSE) file

## Author

Rajiv Yadav
- GitHub: [@rajiv8510-arch](https://github.com/rajiv8510-arch)

## Contributing

Issues and pull requests welcome!
```

---

## Project Structure Template

**Purpose:** Arduino project organization

```
ProjectName/
├── ProjectName/
│   ├── ProjectName.ino         ← Main sketch
│   └── config.h                ← Configuration
├── docs/
│   ├── INSTALLATION.md
│   └── CONFIGURATION.md
├── hardware/
│   ├── schematic.png
│   ├── wiring.png
│   └── BOM.txt
├── examples/
│   └── test/
│       └── test.ino
├── README.md
├── CHANGELOG.md
├── LICENSE
└── .gitignore
```

---

## Project README Template

**File:** `README.md`

```markdown
# ProjectName

Brief description of what this project does.

## Features

- Feature 1
- Feature 2
- Feature 3

## Hardware Required

- Arduino Uno (or Nano, Mega, etc.)
- Component 1 - Purpose - [Link if special]
- Component 2 - Purpose
- Component 3 - Purpose
- Resistors, wires, breadboard

## Required Libraries

Install these libraries first:

- [RajivRelay](https://github.com/rajiv8510-arch/Arduino-Library-RajivRelay) - v1.0.0+
- [RajivSensorDI](https://github.com/rajiv8510-arch/Arduino-Library-RajivSensorDI) - v1.0.0+
- Standard libraries (included with Arduino IDE)

## Wiring Diagram

```
Relay Module:
  VCC → 5V
  GND → GND
  IN → Pin 7

Sensor:
  Signal → Pin 5
  VCC → 5V
  GND → GND
```

See [hardware/wiring.png](hardware/wiring.png) for visual diagram.

## Installation

1. **Install libraries** (see Required Libraries above)

2. **Wire hardware** (see Wiring Diagram above)

3. **Upload sketch:**
   - Open `ProjectName/ProjectName.ino` in Arduino IDE
   - Select board: Tools → Board → Arduino Uno
   - Select port: Tools → Port → COMX
   - Click Upload

4. **Configure** (optional):
   - Edit `config.h` for pin assignments
   - Adjust timing constants

## Configuration

Edit `config.h`:

```cpp
// Pin definitions
const int PIN_RELAY = 7;
const int PIN_SENSOR = 5;

// Timing
const int TIMEOUT = 300;  // seconds
```

## Usage

1. Power on Arduino
2. System initializes (LED blinks 3 times)
3. [Explain normal operation]
4. [Explain user interaction]

## Troubleshooting

**Problem:** LED not blinking
**Solution:** Check power supply, verify pin connections

**Problem:** Sensor not responding
**Solution:** Check sensor wiring, test sensor separately

## Bill of Materials (BOM)

| Component | Quantity | Notes |
|-----------|----------|-------|
| Arduino Uno | 1 | Or compatible |
| 5V Relay Module | 1 | SRD-05VDC-SL-C |
| IR Sensor | 1 | FC-51 or similar |
| Resistor 220Ω | 1 | For LED |
| LED | 1 | Any color |
| Jumper wires | 10+ | Male-male |

## Version History

### v1.0.0 (2024-XX-XX)
- Initial release
- Basic functionality
- Sensor integration

## License

MIT License (or your preference)

## Author

Rajiv Yadav
- GitHub: [@rajiv8510-arch](https://github.com/rajiv8510-arch)

## Acknowledgments

- Library X for inspiration
- Tutorial Y for reference
```

---

## CHANGELOG.md Template

**Purpose:** Track version changes

**File:** `CHANGELOG.md`

```markdown
# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- Features planned but not released

## [1.1.0] - 2024-XX-XX

### Added
- New feature description
- Another feature

### Changed
- Modified behavior
- Updated dependency

### Fixed
- Bug fix description
- Another fix

## [1.0.1] - 2024-XX-XX

### Fixed
- Critical bug fix

## [1.0.0] - 2024-XX-XX

### Added
- Initial release
- Core functionality
- Basic documentation
```

---

## LICENSE Template (MIT)

**File:** `LICENSE`

```
MIT License

Copyright (c) 2024 Rajiv Yadav

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Example Sketch Template

**File:** `examples/BasicExample/BasicExample.ino`

```cpp
/*
 * Basic Example - LibraryName
 * 
 * Description: Simple example showing basic library usage
 * 
 * Hardware:
 *   - Arduino Uno (or compatible)
 *   - Component on Pin 13
 * 
 * Author: Rajiv Yadav
 * Date: 2024-XX-XX
 */

#include <LibraryName.h>

// Pin definitions
const int PIN_DEVICE = 13;

// Create instance
LibraryName myDevice(PIN_DEVICE);

void setup() {
    // Initialize serial (optional)
    Serial.begin(9600);
    Serial.println("Starting...");
    
    // Initialize library
    myDevice.begin();
    
    Serial.println("Ready!");
}

void loop() {
    // Use library
    myDevice.doSomething();
    
    // Check status
    if (myDevice.checkStatus()) {
        Serial.println("Active");
    }
    
    delay(1000);
}
```

---

## config.h Template

**Purpose:** Centralize configuration

**File:** `ProjectName/config.h` or `src/config.h`

```cpp
#ifndef CONFIG_H
#define CONFIG_H

// ===== PIN DEFINITIONS =====
const int PIN_RELAY_PUMP = 7;
const int PIN_SENSOR_LEVEL_HIGH = 5;
const int PIN_SENSOR_LEVEL_LOW = 6;
const int PIN_LED_STATUS = 13;

// ===== TIMING CONSTANTS =====
const unsigned long DEBOUNCE_DELAY = 50;      // ms
const unsigned long TIMEOUT_PUMP = 300000;     // ms (5 min)
const unsigned long INTERVAL_CHECK = 1000;     // ms (1 sec)

// ===== BEHAVIOR FLAGS =====
const bool ENABLE_DEBUG = true;
const bool INVERT_SENSOR_LOGIC = false;

// ===== THRESHOLDS =====
const int THRESHOLD_TEMPERATURE = 50;          // Celsius
const int THRESHOLD_VOLTAGE = 45;              // x10 (4.5V)

#endif // CONFIG_H
```

---

## Batch Script Templates

### Update All Libraries (Windows)

**File:** `update-all-libs.bat`

```batch
@echo off
echo ===================================
echo  Updating All Arduino Libraries
echo ===================================
echo.

cd /d F:\ArduinoWorkspace\libraries

for /D %%i in (*) do (
    echo.
    echo [Updating %%i...]
    cd "%%i"
    
    REM Check if it's a git repository
    if exist ".git" (
        git pull origin main
        if errorlevel 1 (
            echo ERROR: Failed to update %%i
        ) else (
            echo SUCCESS: %%i updated
        )
    ) else (
        echo SKIP: %%i is not a git repository
    )
    
    cd ..
)

echo.
echo ===================================
echo  Update Complete
echo ===================================
pause
```

### Check Status of All (Windows)

**File:** `check-all-status.bat`

```batch
@echo off
echo ===================================
echo  Checking Git Status
echo ===================================
echo.

cd /d F:\ArduinoWorkspace\libraries

for /D %%i in (*) do (
    echo.
    echo === %%i ===
    cd "%%i"
    
    if exist ".git" (
        git status -s
        if errorlevel 1 (
            echo No changes
        )
    ) else (
        echo Not a git repository
    )
    
    cd ..
)

echo.
pause
```

---

## Quick Reference

**Copy these templates to:**
- New libraries: Use library templates
- New projects: Use project templates
- Root of repo: `.gitignore`, `LICENSE`, `README.md`
- Examples folder: Example sketch templates

**Customize:**
- Replace `LibraryName` with actual name
- Update pin numbers
- Adjust timing constants
- Modify features list

---

*Use these templates as starting points - customize for your needs*
