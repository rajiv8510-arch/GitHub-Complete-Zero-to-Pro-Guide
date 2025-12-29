# ⚡ Git Quick Reference Card - Arduino Projects

**Keep this handy for daily use!**

---

## 🚀 Setup (First Time Only)

```bash
# Install Git, then:
git config --global user.name "YourName"
git config --global user.email "your@email.com"
```

---

## 📋 Daily Workflow (Copy-Paste Ready)

```bash
# 1️⃣ START: Get latest from GitHub
git pull origin main

# 2️⃣ WORK: Edit your files in Arduino IDE

# 3️⃣ CHECK: What changed?
git status

# 4️⃣ STAGE: Add files
git add .                           # All files
git add *.ino *.h                   # Only .ino and .h
git add filename.ino                # Specific file

# 5️⃣ COMMIT: Save snapshot
git commit -m "Fixed door sensor bug"

# 6️⃣ UPLOAD: Push to GitHub
git push origin main
```

---

## 📦 Starting New Project

### **Method A: GitHub First**
```bash
# 1. Create repo on github.com
# 2. Clone to PC:
git clone https://github.com/Username/ProjectName.git
cd ProjectName
# 3. Add files, then:
git add .
git commit -m "Initial commit"
git push origin main
```

### **Method B: Local First**
```bash
# 1. In your project folder:
git init
git add .
git commit -m "Initial commit"
# 2. Create repo on github.com
# 3. Connect:
git remote add origin https://github.com/Username/ProjectName.git
git push -u origin main
```

---

## 🔍 Checking Status

```bash
git status              # What changed?
git log --oneline       # Recent commits
git diff               # Exact changes
git diff filename.ino  # Changes in specific file
```

---

## ↩️ Undo Mistakes

```bash
# Undo file changes (before git add):
git checkout -- filename.ino
git checkout -- .                    # All files

# Unstage file (after git add):
git reset HEAD filename.ino

# Undo last commit (keep changes):
git reset --soft HEAD~1

# Undo last commit (discard changes):
git reset --hard HEAD~1              # ⚠️ DANGEROUS!
```

---

## 🌿 Branches

```bash
git branch                           # List branches
git checkout -b new-feature          # Create + switch
git checkout main                    # Switch to main
git merge new-feature                # Merge branch
git branch -d new-feature            # Delete branch
```

---

## 🔖 Releases/Tags

```bash
# Create version tag:
git tag -a v1.0.0 -m "Version 1.0 release"
git push origin v1.0.0

# List tags:
git tag

# Delete tag:
git tag -d v1.0.0
```

---

## 📥 Working with Libraries

```bash
# Download library to Arduino/libraries/:
cd C:\Users\YourName\Documents\Arduino\libraries
git clone https://github.com/Author/LibraryName.git

# Update library:
cd LibraryName
git pull origin main
```

---

## 🚨 Common Problems

### "Permission denied"
```bash
git remote set-url origin https://github.com/User/Repo.git
```

### "Failed to push"
```bash
git pull origin main      # Pull first
git push origin main      # Then push
```

### "Merge conflict"
```bash
# 1. Open conflicted file
# 2. Edit to resolve
# 3. Save file
git add filename.ino
git commit -m "Resolved conflict"
```

---

## 📝 Commit Message Templates

```bash
# Feature:
git commit -m "Add night mode detection"

# Bug fix:
git commit -m "Fix door sensor false alarms"

# Documentation:
git commit -m "Update README with wiring diagram"

# Refactor:
git commit -m "Refactor sensor reading logic"

# Configuration:
git commit -m "Adjust detection thresholds"

# Initial:
git commit -m "Initial commit - v1.0"
```

---

## 🎯 .gitignore for Arduino

Create `.gitignore` in project root:

```gitignore
# Build files
*.hex
*.elf
*.bin
build/

# Libraries (document instead)
libraries/

# Backups
*.bak
*~

# OS
.DS_Store
Thumbs.db

# IDE
.vscode/
```

---

## 📂 Recommended Project Structure

```
MyArduinoProject/
├── MyArduinoProject/
│   ├── MyArduinoProject.ino    ⭐ Sketch
│   └── config.h                 ⚙️ Configuration
├── docs/
│   ├── README.md
│   └── installation.md
├── hardware/
│   ├── schematic.png
│   └── bom.txt
├── examples/
│   └── BasicExample/
├── .gitignore                   🚫 Exclusions
└── README.md                    📖 Main docs
```

---

## ⌨️ One-Line Commands

```bash
# Quick add + commit + push:
git add . && git commit -m "Quick update" && git push origin main

# Check if up to date:
git fetch && git status

# Discard all local changes:
git reset --hard origin/main     # ⚠️ DANGEROUS!

# View remote URL:
git remote -v

# Change remote URL:
git remote set-url origin https://github.com/User/NewRepo.git

# Clone + enter folder:
git clone https://github.com/User/Repo.git && cd Repo
```

---

## 🎓 Learning Path

1. ✅ Setup (config user.name, user.email)
2. ✅ Clone existing project
3. ✅ Daily workflow (pull → edit → add → commit → push)
4. ✅ Create new repository
5. ⬜ Branching
6. ⬜ Merge conflicts
7. ⬜ Tags/Releases

---

## 💾 Save These 3 Commands

**These handle 90% of your daily Git use:**

```bash
git pull origin main
git add . && git commit -m "Your message here"
git push origin main
```

---

## 📱 GitHub Desktop (Alternative)

**Prefer GUI over command line?**

Download: https://desktop.github.com

- Visual interface
- No commands needed
- Great for beginners
- Works on Windows

---

## 🆘 Emergency Commands

```bash
# Forgot to pull before commit?
git pull --rebase origin main

# Accidentally committed wrong files?
git reset --soft HEAD~1           # Undo commit, keep changes
git reset HEAD filename           # Unstage specific file

# Want to start over?
cd ..
rm -rf ProjectFolder              # Delete folder
git clone https://...             # Re-clone fresh copy
```

---

## ✨ Pro Tips

1. **Commit often** - Small commits are easier to track
2. **Pull before push** - Avoids conflicts
3. **Write clear messages** - "Fix bug" ❌ | "Fix door sensor timeout" ✅
4. **Use .gitignore** - Don't commit build files
5. **Tag releases** - v1.0, v2.0, etc.

---

**Print this and keep near your desk!** 📌
