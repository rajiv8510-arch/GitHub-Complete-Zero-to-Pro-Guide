# Setup Guide - Arduino Development with GitHub

**One-time configuration for new PCs**

Time required: 60 minutes

---

## Prerequisites

- Windows PC with internet
- GitHub account (create at [github.com](https://github.com))
- Admin rights to install software

---

## Phase 1: Software Installation (30 min)

### 1. Git

**Download:** [git-scm.com/download/windows](https://git-scm.com/download/windows)

**Installation:**
- Run installer
- Accept defaults except:
  - ✅ Use Vim as default editor
  - ✅ Git from command line and 3rd-party software
  - ✅ Use bundled OpenSSH
  - ✅ Use OpenSSL library
  - ✅ Checkout Windows-style, commit Unix-style line endings
  - ✅ Use MinTTY
  - ✅ Enable file system caching

**Verify:**
```bash
git --version
# Expected: git version 2.x.x
```

**Configure:**
```bash
git config --global user.name "Rajiv Yadav"
git config --global user.email "your.email@example.com"

# Verify
git config --list
```

---

### 2. Arduino IDE 2.x

**Download:** [arduino.cc/en/software](https://www.arduino.cc/en/software)

**Installation:**
- Install to: `C:\Program Files\Arduino IDE`
- ✅ Create desktop shortcut

**First Launch:**
1. File → Preferences
2. Configure:
   - ✅ Enable Auto Save
   - ✅ Enable Auto Complete
   - ✅ Editor Quick Suggestions
   - ☐ Send anonymous statistics (uncheck)
   - Font Size: 14

---

### 3. VS Code

**Download:** [code.visualstudio.com](https://code.visualstudio.com/)

**Installation - Check these:**
- ✅ Add "Open with Code" to file context menu
- ✅ Add "Open with Code" to directory context menu
- ✅ Register Code as editor for supported files
- ✅ Add to PATH
- ✅ Launch Visual Studio Code

**Extensions:**
1. Press `Ctrl+Shift+X`
2. Search: "C/C++"
3. Install by Microsoft

---

## Phase 2: Workspace Setup (10 min)

### Create Directory Structure

```bash
cd /d F:\
mkdir ArduinoWorkspace
cd ArduinoWorkspace
mkdir libraries
mkdir projects

# Verify
dir
# Should show: libraries, projects
```

### Configure Arduino IDE

1. Open Arduino IDE
2. File → Preferences → Sketchbook location
3. Browse to: `F:\ArduinoWorkspace`
4. Click OK
5. **RESTART Arduino IDE**

**Verify:** File → Preferences should show `F:\ArduinoWorkspace`

---

## Phase 3: GitHub Authentication (10 min)

### Method A: Personal Access Token (Recommended)

1. Visit: [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click: "Generate new token (classic)"
3. Settings:
   - Note: `Arduino-Development-PC`
   - Expiration: `No expiration` or `1 year`
   - Scopes: ✅ **repo** (check all sub-items)
4. Generate token
5. **COPY TOKEN IMMEDIATELY** (won't see again)
6. Save in password manager

**Usage:** When Git asks for password, paste token instead

### Method B: SSH Key (Advanced)

```bash
# Generate key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Copy public key
cat ~/.ssh/id_ed25519.pub

# Add to GitHub: Settings → SSH and GPG keys → New SSH key
```

---

## Phase 4: Clone Libraries (10 min)

```bash
cd /d F:\ArduinoWorkspace\libraries

# Clone each library
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivButton.git RajivButton
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivRelay.git RajivRelay
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivSensorDI.git RajivSensorDI
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivDigitalOutput.git RajivDigitalOutput
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivPotFillConfig.git RajivPotFillConfig
```

**When prompted:**
- Username: `rajiv8510-arch`
- Password: `[paste your Personal Access Token]`

**Verify in Arduino IDE:**
1. Restart Arduino IDE
2. Sketch → Include Library
3. Scroll down - should see: RajivButton, RajivRelay, RajivSensorDI, etc.

---

## Phase 5: Clone Projects (Optional)

```bash
cd /d F:\ArduinoWorkspace\projects

git clone https://github.com/rajiv8510-arch/Arduino-Project-DoorSecurityAlarm.git DoorSecurityAlarm
# Repeat for other projects
```

**Verify:**
- File → Open → `F:\ArduinoWorkspace\projects\DoorSecurityAlarm\DoorSecurityAlarm.ino`

---

## VS Code GitHub Integration (Optional)

1. Click Account icon (bottom-left)
2. "Sign in to Sync Settings"
3. Choose "Sign in with GitHub"
4. Authorize in browser
5. Verify: Username shows in bottom-left

---

## Setup Complete ✓

**You now have:**
- ✅ Git version control
- ✅ Arduino IDE configured
- ✅ VS Code with C/C++ support
- ✅ Workspace at `F:\ArduinoWorkspace`
- ✅ Libraries cloned
- ✅ GitHub authentication

**Next:** See [WORKFLOW.md](WORKFLOW.md) for daily operations

---

## Quick Commands Summary

```bash
# Git identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Clone library template
git clone https://github.com/rajiv8510-arch/Arduino-Library-LibName.git LibName

# Clone project template
git clone https://github.com/rajiv8510-arch/Arduino-Project-ProjName.git ProjName

# Verify workspace
cd /d F:\ArduinoWorkspace
dir
```

---

## Troubleshooting Setup

**Git not recognized:**
- Close and reopen CMD
- Restart PC if needed

**Arduino IDE doesn't show libraries:**
- Verify Sketchbook location: `F:\ArduinoWorkspace`
- Restart Arduino IDE
- Check libraries are in `F:\ArduinoWorkspace\libraries\`

**Permission denied on git clone:**
- Use HTTPS URL (not SSH)
- Check Personal Access Token
- Verify GitHub username

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for more

---

*Time invested: 60 min | Benefit: Lifetime of organized development*
