# Workflow Guide - Daily Arduino Development

**Standard operations for day-to-day development**

---

## Daily Cycle (5 minutes)

```
Morning → PULL → Work → COMMIT → Evening → PUSH
```

---

## Morning: Start Work

**Sync with latest changes from GitHub:**

```bash
# For libraries
cd /d F:\ArduinoWorkspace\libraries\RajivButton
git pull origin main

# For projects
cd /d F:\ArduinoWorkspace\projects\DoorSecurityAlarm
git pull origin main
```

**VS Code alternative:**
1. Open folder
2. Source Control → ... → Pull

---

## During Day: Development

### Editing Libraries

**Use VS Code for `.h` and `.cpp` files:**

1. Open VS Code
2. File → Open Folder → `F:\ArduinoWorkspace\libraries\RajivButton`
3. Edit files
4. Save: `Ctrl+S`
5. Test in Arduino project

**Useful shortcuts:**
- Auto-complete: `Ctrl+Space`
- Jump to definition: `Ctrl+Click`
- Find: `Ctrl+F`
- Replace: `Ctrl+H`

### Editing Projects

**Use Arduino IDE for `.ino` files:**

1. Open Arduino IDE
2. File → Open → `F:\ArduinoWorkspace\projects\DoorSecurityAlarm\DoorSecurityAlarm.ino`
3. Edit code
4. Verify: `Ctrl+R`
5. Upload: `Ctrl+U`
6. Save: `Ctrl+S`

---

## Evening: Save & Upload

### Check What Changed

```bash
git status
```

Output shows:
- Modified files (red)
- New files (red)
- Staged files (green)

### Commit Changes

**Method 1: Command Line (Faster)**

```bash
# Add all changes
git add .

# Commit with message
git commit -m "Fixed sensor timeout bug"

# Push to GitHub
git push origin main
```

**One-liner:**
```bash
git add . && git commit -m "Your message" && git push origin main
```

**Method 2: VS Code (Visual)**

1. Click Source Control icon (left sidebar)
2. Review changes
3. Click + next to files (or + at top for all)
4. Type commit message
5. Click ✓ Commit
6. Click ... → Push

---

## Commit Message Guidelines

**Format:** `Action: Brief description`

**Examples:**
```bash
# Features
git commit -m "Add: Night mode detection"
git commit -m "Feature: Multi-tank support"

# Bug fixes
git commit -m "Fix: Sensor false alarms"
git commit -m "Bugfix: Memory leak in loop"

# Configuration
git commit -m "Update: Detection thresholds"
git commit -m "Config: Pin assignments for Nano"

# Documentation
git commit -m "Docs: Wiring diagram for relay module"
git commit -m "Update: README installation steps"

# Refactor
git commit -m "Refactor: Sensor reading logic"
git commit -m "Cleanup: Remove debug code"
```

**Good messages:**
- ✅ "Fix: Door sensor timeout after 5 minutes"
- ✅ "Add: Temperature monitoring feature"
- ✅ "Update: Pin D5 to D7 for relay"

**Bad messages:**
- ❌ "Update"
- ❌ "Changes"
- ❌ "Fixed stuff"

---

## Multi-PC Workflow

### Office PC (Morning)

```bash
git pull origin main
# Work on code
git add . && git commit -m "Add feature X" && git push origin main
```

### Home PC (Evening)

```bash
git pull origin main  # Gets "Add feature X" changes
# Continue work
git add . && git commit -m "Complete feature X" && git push origin main
```

### Office PC (Next Morning)

```bash
git pull origin main  # Gets "Complete feature X" changes
```

**Key:** Always `pull` before starting work

---

## Working on Multiple Items

### Same Repository

```bash
# Morning
git pull origin main

# Edit library files throughout day
# Edit project files throughout day

# Evening - commit all together
git add .
git commit -m "Updated button debounce and fixed alarm timing"
git push origin main
```

### Multiple Repositories

```bash
# Library
cd /d F:\ArduinoWorkspace\libraries\RajivButton
git add . && git commit -m "Add long-press detection" && git push origin main

# Project
cd /d F:\ArduinoWorkspace\projects\DoorSecurityAlarm
git add . && git commit -m "Use new long-press feature" && git push origin main
```

---

## Creating New Items

### New Library

1. **Create on GitHub:**
   - Visit: [github.com/rajiv8510-arch](https://github.com/rajiv8510-arch)
   - Click: New repository
   - Name: `Arduino-Library-RajivNewLib`
   - Public, Add README
   - Create

2. **Clone locally:**
```bash
cd /d F:\ArduinoWorkspace\libraries
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivNewLib.git RajivNewLib
cd RajivNewLib
```

3. **Create structure:**
```bash
mkdir src examples
# Add files using VS Code
```

4. **Upload:**
```bash
git add . && git commit -m "Initial library structure" && git push origin main
```

See [TEMPLATES.md](TEMPLATES.md) for library structure

### New Project

1. **Create locally:**
```bash
cd /d F:\ArduinoWorkspace\projects
mkdir NewProject
cd NewProject
git init
```

2. **Create `.ino` file in Arduino IDE**

3. **Add files:**
```bash
# Create .gitignore and README (see TEMPLATES.md)
git add .
git commit -m "Initial commit: New Project v1.0"
```

4. **Create on GitHub:**
   - Visit: [github.com/rajiv8510-arch](https://github.com/rajiv8510-arch)
   - New repository: `Arduino-Project-NewProject`
   - Public, **Don't add README** (already have files)
   - Create

5. **Connect & push:**
```bash
git remote add origin https://github.com/rajiv8510-arch/Arduino-Project-NewProject.git
git branch -M main
git push -u origin main
```

---

## Quick Operations

### Update Single Library

```bash
cd /d F:\ArduinoWorkspace\libraries\RajivRelay
git pull origin main
```

### Update All Libraries (Batch)

Create `update-all-libs.bat`:
```batch
@echo off
cd /d F:\ArduinoWorkspace\libraries
for /D %%i in (*) do (
    echo Updating %%i...
    cd %%i
    git pull origin main
    cd ..
)
echo Done!
pause
```

### Check Status of Multiple Repos

Create `check-status.bat`:
```batch
@echo off
cd /d F:\ArduinoWorkspace\libraries
for /D %%i in (*) do (
    echo === %%i ===
    cd %%i
    git status -s
    cd ..
)
pause
```

---

## Best Practices

**DO:**
- ✅ Pull before starting work
- ✅ Commit frequently (small, logical changes)
- ✅ Write clear commit messages
- ✅ Push at end of day
- ✅ Test before committing
- ✅ Use .gitignore for build files

**DON'T:**
- ❌ Forget to pull first
- ❌ Commit untested code
- ❌ Use vague commit messages
- ❌ Commit compiled files (.hex, .bin)
- ❌ Work for days without committing

---

## Workflow Summary

```bash
# === STANDARD DAILY WORKFLOW ===

# 1. Morning sync
git pull origin main

# 2. Work (edit files)

# 3. Evening save
git status                                    # Check changes
git add .                                     # Stage all
git commit -m "Descriptive message"           # Commit
git push origin main                          # Upload

# === ONE-LINE VERSION ===
git add . && git commit -m "Message" && git push origin main
```

---

**Next:** See [COMMANDS.md](COMMANDS.md) for complete command reference
