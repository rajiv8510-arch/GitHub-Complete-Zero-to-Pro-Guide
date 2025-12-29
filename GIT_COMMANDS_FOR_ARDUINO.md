# 🚀 Git Commands for Arduino Projects - Complete Guide

**Easy Interactive Guide for Windows PC ↔️ GitHub**

---

## 📋 Table of Contents

1. [Initial Setup (One-Time)](#initial-setup)
2. [Creating New Repository](#creating-new-repository)
3. [Cloning Existing Repository](#cloning-existing-repository)
4. [Basic Workflow (Daily Use)](#basic-workflow)
5. [Working with Arduino Projects](#working-with-arduino-projects)
6. [Common Scenarios](#common-scenarios)
7. [Troubleshooting](#troubleshooting)
8. [Cheat Sheet](#cheat-sheet)

---

## 🔧 Initial Setup (One-Time)

### **Step 1: Install Git on Windows**

1. Download Git: https://git-scm.com/download/win
2. Run installer (accept defaults)
3. Verify installation:

```bash
# Open CMD or PowerShell and type:
git --version
```

**Expected output:**
```
git version 2.42.0.windows.1
```

---

### **Step 2: Configure Git (Your Identity)**

```bash
# Set your name (appears in commits)
git config --global user.name "Rajiv"

# Set your email (must match GitHub email)
git config --global user.email "rajiv@example.com"

# Verify configuration
git config --list
```

**Expected output:**
```
user.name=Rajiv
user.email=rajiv@example.com
```

---

### **Step 3: Create GitHub Account**

1. Go to https://github.com
2. Sign up (free account)
3. Verify email
4. Done! ✓

---

### **Step 4: Connect Git to GitHub (Authentication)**

#### **Method A: Personal Access Token (Recommended)**

1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token
3. Select scopes: `repo` (full control)
4. Copy token (save it - you won't see it again!)

**When prompted for password, paste token instead!**

#### **Method B: SSH Key (Advanced)**

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "rajiv@example.com"

# Copy public key
cat ~/.ssh/id_ed25519.pub

# Add to GitHub: Settings → SSH and GPG keys → New SSH key
```

---

## 📦 Creating New Repository

### **Scenario 1: Start on GitHub, Clone to PC**

```bash
# 1. Create repository on GitHub website
#    - Go to github.com
#    - Click "+" → New repository
#    - Name: DoorSecurityAlarm_v4.2_ULTIMATE
#    - Public/Private
#    - ✓ Add README
#    - Create repository

# 2. Clone to your PC
cd C:\Users\YourName\Documents\Arduino
git clone https://github.com/YourUsername/DoorSecurityAlarm_v4.2_ULTIMATE.git

# 3. Navigate into folder
cd DoorSecurityAlarm_v4.2_ULTIMATE

# 4. Add your files
# (copy your Arduino project files here)

# 5. Commit and push (see Basic Workflow below)
```

---

### **Scenario 2: Start on PC, Push to GitHub**

```bash
# 1. Navigate to your existing project folder
cd C:\Users\YourName\Documents\Arduino\DoorSecurityAlarm_v4.2_ULTIMATE

# 2. Initialize Git repository
git init

# 3. Add all files
git add .

# 4. First commit
git commit -m "Initial commit - v4.2 ULTIMATE"

# 5. Create repository on GitHub (via website)
#    - github.com → New repository
#    - Name: DoorSecurityAlarm_v4.2_ULTIMATE
#    - DO NOT add README (already have files)
#    - Create repository

# 6. Connect local repo to GitHub
git remote add origin https://github.com/YourUsername/DoorSecurityAlarm_v4.2_ULTIMATE.git

# 7. Push to GitHub
git branch -M main
git push -u origin main
```

**Done! Your project is now on GitHub!** ✓

---

## 📥 Cloning Existing Repository

### **Clone Someone Else's Project:**

```bash
# 1. Navigate to where you want the project
cd C:\Users\YourName\Documents\Arduino

# 2. Clone repository
git clone https://github.com/SomeUser/ArduinoLibrary.git

# 3. Enter folder
cd ArduinoLibrary

# 4. Open in Arduino IDE
# Double-click the .ino file
```

---

### **Clone Your Own Project (Different PC):**

```bash
# Same as above, just use your GitHub URL
git clone https://github.com/YourUsername/DoorSecurityAlarm_v4.2_ULTIMATE.git
```

---

## 🔄 Basic Workflow (Daily Use)

### **The Golden Workflow:**

```
1. PULL (get latest from GitHub)
2. WORK (edit files)
3. ADD (stage changes)
4. COMMIT (save snapshot)
5. PUSH (upload to GitHub)
```

---

### **Step-by-Step Commands:**

```bash
# === STEP 1: PULL (Get latest changes from GitHub) ===
git pull origin main

# === STEP 2: WORK ===
# Edit your files in Arduino IDE, text editor, etc.

# === STEP 3: CHECK STATUS (See what changed) ===
git status

# Expected output:
# Modified: DoorSecurityAlarm_v4_2_ULTIMATE.ino
# Untracked: config.h

# === STEP 4: ADD FILES (Stage for commit) ===

# Add specific file:
git add DoorSecurityAlarm_v4_2_ULTIMATE.ino

# OR add all changed files:
git add .

# OR add all .ino and .h files:
git add *.ino *.h

# === STEP 5: COMMIT (Save snapshot with message) ===
git commit -m "Fixed door switch logic"

# === STEP 6: PUSH (Upload to GitHub) ===
git push origin main
```

**Done! Changes are now on GitHub!** ✓

---

## 🎯 Working with Arduino Projects

### **Typical Arduino Project Structure:**

```
MyArduinoProject/
├── MyArduinoProject/
│   ├── MyArduinoProject.ino     ← Main sketch
│   └── config.h                  ← Configuration
├── docs/
│   ├── README.md
│   └── installation_guide.md
├── hardware/
│   └── schematic.png
├── libraries/                    ← DON'T commit (use .gitignore)
├── .gitignore                    ← Important!
└── README.md
```

---

### **Create .gitignore File:**

**Why?** Exclude temporary files, compiled binaries, libraries

```bash
# Create .gitignore in project root
cd C:\Users\YourName\Documents\Arduino\DoorSecurityAlarm_v4.2_ULTIMATE

# Create file (Windows PowerShell):
New-Item -Path .gitignore -ItemType File

# Or create file (Git Bash):
touch .gitignore
```

**Add this content to .gitignore:**

```gitignore
# Arduino IDE files
*.hex
*.elf
*.eep
*.bin
*.lss
*.map
*.sym

# Build directories
build/
*.build/

# Libraries (use library manager instead)
libraries/

# Backup files
*~
*.bak
*.tmp
*.swp

# OS files
.DS_Store
Thumbs.db
desktop.ini

# IDE files
.vscode/
.idea/
*.code-workspace

# Compiled Python
__pycache__/
*.pyc

# Personal notes
notes.txt
TODO.txt
```

**Commit .gitignore:**

```bash
git add .gitignore
git commit -m "Add .gitignore for Arduino project"
git push origin main
```

---

### **Arduino Libraries - Best Practice:**

**DON'T** commit libraries to project repo!

**DO** provide installation instructions:

Create `LIBRARIES.md`:

```markdown
# Required Libraries

Install these in Arduino IDE:

1. RajivRelay v1.0.0
2. RajivSensorDI v1.0.0
3. RajivWatchDog v1.0.0

## Installation:
Copy library folders to:
`Documents\Arduino\libraries\`
```

---

## 🎭 Common Scenarios

### **Scenario A: I Made Changes, Push to GitHub**

```bash
# 1. Check what changed
git status

# 2. Add changes
git add .

# 3. Commit with message
git commit -m "Updated detection thresholds in config.h"

# 4. Push to GitHub
git push origin main
```

---

### **Scenario B: My Friend Updated GitHub, I Want Latest**

```bash
# Pull latest changes
git pull origin main

# If conflicts occur (rare):
# 1. Git will mark conflicts in files
# 2. Open files, resolve conflicts
# 3. Add resolved files: git add .
# 4. Commit: git commit -m "Resolved merge conflicts"
```

---

### **Scenario C: Create New Version (Release)**

```bash
# 1. Make sure everything is committed
git status

# 2. Create tag (version)
git tag -a v4.2.0 -m "Version 4.2 ULTIMATE release"

# 3. Push tag to GitHub
git push origin v4.2.0

# 4. OR push all tags
git push --tags
```

**On GitHub:** Go to Releases → Create new release from tag

---

### **Scenario D: Made Mistake, Undo Changes**

#### **Case 1: File not yet added (before `git add`)**

```bash
# Undo changes to single file
git checkout -- filename.ino

# Undo ALL changes
git checkout -- .
```

#### **Case 2: File added but not committed (after `git add`)**

```bash
# Unstage file
git reset HEAD filename.ino

# Then undo changes
git checkout -- filename.ino
```

#### **Case 3: Already committed (after `git commit`)**

```bash
# Undo last commit, keep changes
git reset --soft HEAD~1

# Undo last commit, discard changes (DANGEROUS!)
git reset --hard HEAD~1
```

#### **Case 4: Already pushed to GitHub**

```bash
# Revert specific commit (creates new commit)
git revert <commit-hash>
git push origin main

# Find commit hash:
git log --oneline
```

---

### **Scenario E: Work on New Feature (Branching)**

```bash
# 1. Create new branch
git checkout -b feature-night-mode

# 2. Make changes, commit
git add .
git commit -m "Add night mode detection"

# 3. Push branch to GitHub
git push origin feature-night-mode

# 4. Switch back to main
git checkout main

# 5. Merge feature when ready
git merge feature-night-mode

# 6. Delete branch (optional)
git branch -d feature-night-mode
```

---

### **Scenario F: Download Libraries from GitHub**

```bash
# 1. Clone library repository
cd C:\Users\YourName\Documents\Arduino\libraries
git clone https://github.com/SomeUser/RajivRelay.git

# 2. Restart Arduino IDE
# Library now available!

# 3. Update library later
cd RajivRelay
git pull origin main
```

---

## 🐛 Troubleshooting

### **Problem: "Permission denied (publickey)"**

**Solution:**
```bash
# Use HTTPS instead of SSH
git remote set-url origin https://github.com/YourUsername/YourRepo.git
```

---

### **Problem: "Please tell me who you are"**

**Solution:**
```bash
git config --global user.name "Rajiv"
git config --global user.email "rajiv@example.com"
```

---

### **Problem: "Failed to push - rejected"**

**Cause:** GitHub has changes you don't have locally

**Solution:**
```bash
# Pull first, then push
git pull origin main
git push origin main
```

---

### **Problem: "Merge conflict"**

**Solution:**
```bash
# 1. Open conflicted file
# 2. Look for markers:
#    <<<<<<< HEAD
#    Your changes
#    =======
#    Their changes
#    >>>>>>> branch-name

# 3. Manually edit to keep what you want
# 4. Remove conflict markers
# 5. Save file

# 6. Add resolved file
git add filename.ino

# 7. Commit
git commit -m "Resolved merge conflict"
```

---

### **Problem: "Large file detected"**

**Cause:** GitHub limits file size to 100MB

**Solution:**
```bash
# Remove large file from staging
git rm --cached large_file.bin

# Add to .gitignore
echo "large_file.bin" >> .gitignore

# Commit
git add .gitignore
git commit -m "Remove large file"
```

---

### **Problem: "Authentication failed"**

**Solution (Windows):**
```bash
# Clear saved credentials
Control Panel → Credential Manager → Windows Credentials
# Remove GitHub entries

# Next push will prompt for username + token
git push origin main
# Username: YourGitHubUsername
# Password: <paste your Personal Access Token>
```

---

## 📝 Cheat Sheet

### **First Time Setup:**

```bash
git config --global user.name "Rajiv"
git config --global user.email "rajiv@example.com"
```

---

### **Starting New Project:**

```bash
# On PC first:
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/User/Repo.git
git push -u origin main

# OR clone from GitHub:
git clone https://github.com/User/Repo.git
```

---

### **Daily Workflow:**

```bash
git pull origin main          # Get latest
# ... edit files ...
git status                    # See changes
git add .                     # Stage all changes
git commit -m "Description"   # Commit
git push origin main          # Upload
```

---

### **Check Status:**

```bash
git status                    # What changed?
git log                       # Commit history
git log --oneline             # Short history
git diff                      # See exact changes
git diff filename.ino         # Changes in specific file
```

---

### **Branches:**

```bash
git branch                    # List branches
git checkout -b new-feature   # Create + switch
git checkout main             # Switch to main
git merge new-feature         # Merge branch
git branch -d new-feature     # Delete branch
```

---

### **Undo Mistakes:**

```bash
git checkout -- file.ino      # Undo uncommitted changes
git reset HEAD file.ino       # Unstage file
git reset --soft HEAD~1       # Undo last commit (keep changes)
git revert <commit-hash>      # Undo old commit
```

---

### **Remote Repositories:**

```bash
git remote -v                          # Show remotes
git remote add origin <url>            # Add remote
git remote set-url origin <new-url>    # Change URL
git push origin main                   # Push to GitHub
git pull origin main                   # Pull from GitHub
```

---

## 🎯 Quick Start Examples

### **Example 1: Upload Existing Arduino Project**

```bash
cd C:\Users\Rajiv\Documents\Arduino\DoorAlarm
git init
git add .
git commit -m "Initial commit - Door Alarm v1.0"
# Create repo on GitHub website
git remote add origin https://github.com/Rajiv/DoorAlarm.git
git push -u origin main
```

---

### **Example 2: Download Arduino Library**

```bash
cd C:\Users\Rajiv\Documents\Arduino\libraries
git clone https://github.com/Rajiv/RajivRelay.git
# Restart Arduino IDE
```

---

### **Example 3: Update Your Code**

```bash
cd C:\Users\Rajiv\Documents\Arduino\DoorAlarm
git pull origin main
# Edit files in Arduino IDE
git add .
git commit -m "Fixed sensor bug"
git push origin main
```

---

## 🚀 Best Practices

### ✅ **DO:**

- Commit often (small, logical changes)
- Write clear commit messages
- Pull before you push
- Use .gitignore for Arduino builds
- Create releases/tags for versions
- Document your projects (README.md)

### ❌ **DON'T:**

- Commit compiled files (.hex, .bin)
- Commit libraries (document installation instead)
- Make huge commits (100+ files)
- Force push (`git push -f`) unless you know what you're doing
- Commit sensitive info (passwords, API keys)

---

## 📚 Learn More

- **Official Git Docs:** https://git-scm.com/doc
- **GitHub Guides:** https://guides.github.com
- **Interactive Tutorial:** https://learngitbranching.js.org
- **GitHub Desktop (GUI):** https://desktop.github.com

---

## 🎓 Practice Exercise

**Try this complete workflow:**

```bash
# 1. Create new repository on GitHub (via website)
#    Name: TestArduino

# 2. Clone to PC
cd C:\Users\YourName\Documents\Arduino
git clone https://github.com/YourUsername/TestArduino.git
cd TestArduino

# 3. Create simple sketch
New-Item -Path TestArduino.ino -ItemType File
# Add code: void setup(){} void loop(){}

# 4. Add, commit, push
git add .
git commit -m "Add basic sketch"
git push origin main

# 5. Check GitHub - file should be there! ✓

# 6. Edit file locally
# Change code

# 7. Update GitHub
git add .
git commit -m "Updated sketch"
git push origin main

# 8. Check GitHub - changes should be there! ✓
```

**Congratulations! You're now using Git + GitHub!** 🎉

---

## 💡 Tips for Arduino Developers

1. **Separate sketch from libraries**
   - Sketch in Git repository
   - Libraries in `Arduino/libraries/` (documented, not committed)

2. **Version your releases**
   - Use Git tags: `git tag v1.0.0`
   - Create GitHub releases for downloads

3. **Document hardware**
   - Add wiring diagrams to `hardware/`
   - BOM (Bill of Materials) in README

4. **Example structure:**
   ```
   MyProject/
   ├── MyProject/
   │   ├── MyProject.ino
   │   └── config.h
   ├── docs/
   ├── hardware/
   ├── examples/
   ├── .gitignore
   └── README.md
   ```

5. **Use GitHub Issues**
   - Track bugs
   - Plan features
   - Collaborate with others

---

**Happy Coding & Version Controlling!** 🚀✨
