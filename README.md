# Arduino Development with GitHub

**Professional reference for Arduino development across multiple PCs**

[![GitHub](https://img.shields.io/badge/GitHub-rajiv8510--arch-blue?logo=github)](https://github.com/rajiv8510-arch)

---

## Quick Navigation

| Guide | Purpose | Time |
|-------|---------|------|
| [**SETUP**](SETUP.md) | First-time PC configuration | 60 min |
| [**WORKFLOW**](WORKFLOW.md) | Daily development operations | 5 min |
| [**COMMANDS**](COMMANDS.md) | Git command reference | - |
| [**TROUBLESHOOTING**](TROUBLESHOOTING.md) | Problem resolution | - |
| [**TEMPLATES**](TEMPLATES.md) | Code/config templates | - |
| [**VISUALS**](VISUALS.md) | Workflow diagrams | - |

---

## Quick Start

**New PC (60 min):**
1. Install: [Git](https://git-scm.com/download/windows), [Arduino IDE 2.x](https://www.arduino.cc/en/software), [VS Code](https://code.visualstudio.com/)
2. Configure: `git config --global user.name "Your Name"`
3. Clone libraries: `git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivButton.git`
4. See [SETUP.md](SETUP.md) for details

**Daily Work:**
```bash
git pull origin main      # Morning: sync
# Edit files in Arduino IDE
git add . && git commit -m "Description" && git push origin main  # Evening: upload
```
See [WORKFLOW.md](WORKFLOW.md) for details

---

## Workspace Structure

```
F:\ArduinoWorkspace\
├── libraries\          # Custom libraries (Git repositories)
│   ├── RajivButton\
│   ├── RajivRelay\
│   └── RajivSensorDI\
└── projects\           # Arduino sketches (Git repositories)
    ├── DoorSecurityAlarm\
    └── WaterTankController\
```

---

## GitHub Repositories

**Libraries:**
- [RajivButton](https://github.com/rajiv8510-arch/Arduino-Library-RajivButton)
- [RajivRelay](https://github.com/rajiv8510-arch/Arduino-Library-RajivRelay)
- [RajivSensorDI](https://github.com/rajiv8510-arch/Arduino-Library-RajivSensorDI)
- [RajivDigitalOutput](https://github.com/rajiv8510-arch/Arduino-Library-RajivDigitalOutput)
- [RajivPotFillConfig](https://github.com/rajiv8510-arch/Arduino-Library-RajivPotFillConfig)

**Projects:**
- [DoorSecurityAlarm](https://github.com/rajiv8510-arch/Arduino-Project-DoorSecurityAlarm)

---

## Essential Commands

```bash
# Clone library
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivButton.git RajivButton

# Daily sync
git pull origin main

# Save changes
git add . && git commit -m "Fixed sensor bug" && git push origin main

# Check status
git status
```

See [COMMANDS.md](COMMANDS.md) for complete reference

---

## Notes

- **Workspace:** `F:\ArduinoWorkspace`
- **GitHub:** [@rajiv8510-arch](https://github.com/rajiv8510-arch)
- **Bookmark this:** On all PCs for quick access

---

*Last updated: 2025 | Maintained by Rajiv Yadav*
