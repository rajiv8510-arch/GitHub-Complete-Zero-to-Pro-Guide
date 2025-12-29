# Commands Reference - Git for Arduino

**Organized by task - copy-paste ready**

---

## Configuration

### First-Time Setup

```bash
git config --global user.name "Rajiv Yadav"
git config --global user.email "your.email@example.com"

# Verify
git config --list
```

### View Configuration

```bash
git config --list                    # All settings
git config user.name                 # Specific setting
git config --global --edit           # Edit config file
```

---

## Repository Operations

### Initialize New Repository

```bash
# Create new repo
git init

# Connect to GitHub
git remote add origin https://github.com/username/repo.git

# First push
git branch -M main
git push -u origin main
```

### Clone Existing Repository

```bash
# Clone to current directory
git clone https://github.com/username/repo.git

# Clone with custom name
git clone https://github.com/username/repo.git CustomName

# Clone to specific location
cd /d F:\ArduinoWorkspace\libraries
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivButton.git RajivButton
```

---

## Daily Workflow

### Sync & Update

```bash
git pull origin main                 # Get latest from GitHub
git fetch                           # Download without merging
git fetch && git status             # Check if behind
```

### Stage Changes

```bash
git add .                           # All files
git add *.ino *.h                   # Specific extensions
git add filename.ino                # Single file
git add folder/                     # Entire folder
```

### Commit Changes

```bash
git commit -m "Message"             # Commit staged files
git commit -am "Message"            # Add + commit tracked files
git commit --amend -m "New msg"     # Change last commit message
```

### Upload Changes

```bash
git push origin main                # Push to GitHub
git push                           # Push to default remote
git push --force                   # Force push (⚠️ dangerous)
```

### One-Liner Workflow

```bash
# Complete workflow
git add . && git commit -m "Description" && git push origin main

# With pull first
git pull origin main && git add . && git commit -m "Message" && git push origin main
```

---

## Information & Status

### Check Status

```bash
git status                          # Current state
git status -s                       # Short format
git status --ignored                # Show ignored files
```

### View History

```bash
git log                             # Full history
git log --oneline                   # Compact history
git log --oneline --graph           # Visual branch history
git log -n 5                        # Last 5 commits
git log --since="2 weeks ago"       # Recent commits
git log --author="Rajiv"            # By author
```

### View Changes

```bash
git diff                            # Unstaged changes
git diff --staged                   # Staged changes
git diff filename.ino               # Changes in specific file
git diff HEAD~1                     # Compare with previous commit
git diff branch1 branch2            # Compare branches
```

### Show Commit Details

```bash
git show                            # Last commit
git show abc1234                    # Specific commit
git show HEAD~2                     # 2 commits ago
```

---

## Undo Operations

### Discard Uncommitted Changes

```bash
# Single file
git checkout -- filename.ino
git restore filename.ino            # Newer Git syntax

# All files
git checkout -- .
git restore .                       # Newer Git syntax
```

### Unstage Files

```bash
# Single file
git reset HEAD filename.ino
git restore --staged filename.ino   # Newer Git syntax

# All files
git reset HEAD
git restore --staged .              # Newer Git syntax
```

### Undo Commits

```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset HEAD~1

# Undo last commit, discard changes (⚠️ dangerous)
git reset --hard HEAD~1

# Undo last 3 commits
git reset --hard HEAD~3

# Revert commit (creates new commit)
git revert abc1234
git revert HEAD
```

### Clean Working Directory

```bash
git clean -n                        # Show what would be removed
git clean -f                        # Remove untracked files
git clean -fd                       # Remove untracked files & directories
git clean -fX                       # Remove ignored files
```

---

## Branching

### Create & Switch

```bash
git branch feature-name             # Create branch
git checkout feature-name           # Switch to branch
git checkout -b feature-name        # Create + switch
git switch feature-name             # Switch (newer Git)
git switch -c feature-name          # Create + switch (newer Git)
```

### List & Info

```bash
git branch                          # List local branches
git branch -a                       # List all branches
git branch -v                       # Branches with last commit
git branch -r                       # Remote branches
```

### Merge & Delete

```bash
git merge feature-name              # Merge branch into current
git merge --no-ff feature-name      # Force merge commit
git merge --abort                   # Abort merge

git branch -d feature-name          # Delete merged branch
git branch -D feature-name          # Force delete branch
```

---

## Remote Operations

### Remote Management

```bash
git remote                          # List remotes
git remote -v                       # List with URLs
git remote show origin              # Remote details

git remote add origin URL           # Add remote
git remote remove origin            # Remove remote
git remote rename old new           # Rename remote
git remote set-url origin NEW_URL   # Change URL
```

### Fetch & Pull

```bash
git fetch origin                    # Download from remote
git fetch --all                     # Fetch all remotes
git pull origin main                # Fetch + merge
git pull --rebase origin main       # Fetch + rebase
```

---

## Tags & Releases

### Create Tags

```bash
# Lightweight tag
git tag v1.0.0

# Annotated tag (recommended)
git tag -a v1.0.0 -m "Version 1.0 release"

# Tag specific commit
git tag -a v1.0.0 abc1234 -m "Version 1.0"
```

### List & Info

```bash
git tag                             # List all tags
git tag -l "v1.*"                   # List matching tags
git show v1.0.0                     # Tag details
```

### Push Tags

```bash
git push origin v1.0.0              # Push single tag
git push origin --tags              # Push all tags
git push --tags                     # Push all tags (short)
```

### Delete Tags

```bash
git tag -d v1.0.0                   # Delete local tag
git push origin --delete v1.0.0     # Delete remote tag
```

---

## Stash (Temporary Storage)

### Save Work

```bash
git stash                           # Stash changes
git stash save "Description"        # Stash with message
git stash -u                        # Include untracked files
```

### Retrieve Work

```bash
git stash list                      # List stashes
git stash show                      # Show latest stash
git stash show stash@{1}            # Show specific stash

git stash pop                       # Apply + delete latest
git stash apply                     # Apply latest (keep stash)
git stash apply stash@{1}           # Apply specific stash
```

### Manage Stashes

```bash
git stash drop                      # Delete latest stash
git stash drop stash@{1}            # Delete specific stash
git stash clear                     # Delete all stashes
```

---

## Advanced Operations

### Search & Find

```bash
# Search commit messages
git log --grep="feature"

# Search code changes
git log -S "function_name"

# Find file history
git log -- filename.ino

# Who changed line
git blame filename.ino
```

### Cherry-Pick

```bash
# Apply specific commit to current branch
git cherry-pick abc1234
git cherry-pick abc1234 def5678     # Multiple commits
```

### Rebase

```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase (edit history)
git rebase -i HEAD~3

# Abort rebase
git rebase --abort

# Continue after resolving conflicts
git rebase --continue
```

---

## Inspection & Comparison

### Compare Commits

```bash
git diff abc1234 def5678            # Between two commits
git diff main feature               # Between branches
git diff HEAD~2..HEAD               # Last 2 commits
```

### File History

```bash
git log --follow filename.ino       # File history with renames
git log --oneline -- filename.ino   # Compact file history
```

### Show File from Commit

```bash
git show abc1234:filename.ino       # View file version
git show HEAD~2:config.h            # 2 commits ago
```

---

## Submodules (Advanced)

### Add Submodule

```bash
git submodule add https://github.com/user/lib.git lib
git submodule init
git submodule update
```

### Update Submodules

```bash
git submodule update --remote        # Update all
git submodule foreach git pull origin main  # Pull each
```

---

## Aliases (Shortcuts)

### Create Aliases

```bash
# Short status
git config --global alias.st status

# Pretty log
git config --global alias.lg "log --oneline --graph"

# Quick commit
git config --global alias.cm "commit -m"

# Usage
git st                              # Instead of: git status
git lg                              # Instead of: git log --oneline --graph
git cm "Message"                    # Instead of: git commit -m "Message"
```

### Useful Aliases

```bash
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
git config --global alias.visual "log --oneline --graph --all"
git config --global alias.amend "commit --amend --no-edit"
```

---

## Arduino-Specific Commands

### Clone Library

```bash
cd /d F:\ArduinoWorkspace\libraries
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivButton.git RajivButton
```

### Update Library

```bash
cd /d F:\ArduinoWorkspace\libraries\RajivButton
git pull origin main
```

### Upload Project

```bash
cd /d F:\ArduinoWorkspace\projects\MyProject
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/rajiv8510-arch/Arduino-Project-MyProject.git
git push -u origin main
```

---

## Batch Operations

### Update All Libraries (Windows)

Create `update-libs.bat`:
```batch
@echo off
cd /d F:\ArduinoWorkspace\libraries
for /D %%i in (*) do (
    cd %%i
    git pull origin main
    cd ..
)
pause
```

### Check All Status

Create `check-all.bat`:
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

## Emergency Commands

### Forgot to Pull Before Edit

```bash
git stash                           # Save local changes
git pull origin main                # Get latest
git stash pop                       # Restore changes
# Resolve conflicts if any
```

### Committed to Wrong Branch

```bash
git checkout correct-branch         # Switch to correct branch
git cherry-pick abc1234             # Apply the commit
git checkout wrong-branch           # Back to wrong branch
git reset --hard HEAD~1             # Remove commit
```

### Pushed Wrong Code

```bash
git revert HEAD                     # Create reverting commit
git push origin main                # Push fix
```

---

## Quick Reference Card

```bash
# === MOST USED COMMANDS ===

git pull origin main                # Morning sync
git status                          # Check changes
git add .                           # Stage all
git commit -m "Message"             # Commit
git push origin main                # Upload

git log --oneline                   # View history
git diff                            # See changes
git checkout -- file                # Discard changes
git branch                          # List branches

# === ONE-LINERS ===
git add . && git commit -m "Msg" && git push origin main
git pull origin main && git add . && git commit -m "Msg" && git push origin main
```

---

**See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for problem resolution**
