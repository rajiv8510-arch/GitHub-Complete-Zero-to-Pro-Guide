# Troubleshooting - Git & Arduino Development

**Solutions to common problems**

---

## Git Issues

### "Permission denied (publickey)"

**Cause:** SSH key not set up or GitHub doesn't recognize it

**Solution:** Use HTTPS instead
```bash
git remote set-url origin https://github.com/username/repo.git
git push origin main
```

---

### "Please tell me who you are"

**Cause:** Git identity not configured

**Solution:**
```bash
git config --global user.name "Rajiv Yadav"
git config --global user.email "your.email@example.com"
```

---

### "Failed to push - rejected"

**Cause:** Remote has changes you don't have locally

**Solution:**
```bash
# Option 1: Pull first (recommended)
git pull origin main
# Resolve conflicts if any
git push origin main

# Option 2: Force push (⚠️ dangerous - overwrites remote)
git push --force origin main
```

---

### "Merge conflict"

**Cause:** Same file edited in different ways

**Solution:**

1. Open conflicted file - look for:
```
<<<<<<< HEAD
Your changes here
=======
Their changes here
>>>>>>> branch-name
```

2. Edit file - choose which code to keep
3. Remove conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Save file

```bash
git add filename.ino
git commit -m "Resolved merge conflict"
git push origin main
```

**Prevention:**
- Pull before starting work
- Communicate with team about who's editing what

---

### "Large file detected"

**Cause:** GitHub limits files to 100MB

**Solution:**
```bash
# Remove from staging
git rm --cached large_file.bin

# Add to .gitignore
echo "large_file.bin" >> .gitignore

# Commit
git add .gitignore
git commit -m "Remove large file, update .gitignore"
```

**Prevention:** Use .gitignore for compiled files

---

### "Authentication failed"

**Cause:** Wrong credentials or expired token

**Solution (Windows):**

1. Clear credentials:
   - Control Panel → Credential Manager
   - Windows Credentials
   - Find GitHub entries
   - Remove

2. Next `git push` will prompt:
   - Username: Your GitHub username
   - Password: Personal Access Token (not password)

**Get new token:** [github.com/settings/tokens](https://github.com/settings/tokens)

---

### "Repository not found"

**Cause:** Wrong URL, private repo without access, or typo

**Solution:**
```bash
# Check current remote
git remote -v

# Fix URL
git remote set-url origin https://github.com/correct-username/correct-repo.git

# Verify
git remote -v
```

---

### "Your branch is behind 'origin/main'"

**Cause:** Remote has newer commits

**Solution:**
```bash
git pull origin main
```

---

### "Your branch is ahead of 'origin/main'"

**Cause:** You have local commits not pushed

**Solution:**
```bash
git push origin main
```

---

### "fatal: refusing to merge unrelated histories"

**Cause:** Trying to merge repos with no common history

**Solution:**
```bash
git pull origin main --allow-unrelated-histories
# Resolve conflicts
git push origin main
```

---

### Accidentally Committed Wrong Files

**Solution:**
```bash
# Remove file from last commit, keep in working directory
git reset HEAD~1 filename.ino

# Or remove from staging before commit
git reset HEAD filename.ino

# Or remove file completely
git rm --cached filename.ino
git commit --amend -m "Remove wrong file"
```

---

### Committed to Wrong Branch

**Solution:**
```bash
# Move commit to correct branch
git checkout correct-branch
git cherry-pick abc1234  # Commit hash from wrong branch
git checkout wrong-branch
git reset --hard HEAD~1  # Remove from wrong branch
```

---

## Arduino IDE Issues

### Libraries Not Showing

**Cause:** Wrong Sketchbook location or IDE not restarted

**Solution:**

1. Check Sketchbook:
   - File → Preferences
   - Should show: `F:\ArduinoWorkspace`
   - If not, browse and select

2. Restart Arduino IDE

3. Verify libraries exist:
```bash
cd /d F:\ArduinoWorkspace\libraries
dir
# Should show: RajivButton, RajivRelay, etc.
```

4. Check library structure:
```
RajivButton\
├── src\
│   ├── RajivButton.h
│   └── RajivButton.cpp
└── library.properties
```

---

### "Library not found" Error

**Cause:** Library name mismatch or missing

**Solution:**

1. Check `#include` statement matches folder name:
```cpp
#include <RajivButton.h>  // Folder must be "RajivButton"
```

2. Verify library location:
```bash
cd /d F:\ArduinoWorkspace\libraries
dir RajivButton
# Should show: src folder, library.properties
```

3. Reinstall library:
```bash
cd /d F:\ArduinoWorkspace\libraries
git clone https://github.com/rajiv8510-arch/Arduino-Library-RajivButton.git RajivButton
```

---

### Sketch Won't Verify/Compile

**Cause:** Syntax errors, missing libraries, or outdated library

**Solution:**

1. Check error message for line number
2. Verify all `#include` statements
3. Update libraries:
```bash
cd /d F:\ArduinoWorkspace\libraries\LibraryName
git pull origin main
```
4. Restart Arduino IDE

---

### Upload Failed - Port Not Found

**Cause:** Board not connected, wrong driver, or port in use

**Solution:**

1. Check USB cable connected
2. Check board LED is on (power)
3. Tools → Port → Select COMX
4. If no ports shown:
   - Install CH340/CP2102 drivers
   - Try different USB cable
   - Try different USB port
5. Close Serial Monitor before upload

---

## VS Code Issues

### Git Not Recognized in VS Code

**Cause:** Git not in PATH or VS Code started before Git installed

**Solution:**

1. Close VS Code
2. Verify Git works in CMD:
```bash
git --version
```
3. Restart VS Code
4. If still not working, add Git to PATH manually

---

### "Changes not detected"

**Cause:** File outside workspace or .gitignore

**Solution:**

1. Check file in correct location
2. Check `.gitignore` doesn't exclude file:
```bash
git check-ignore -v filename.ino
```
3. Refresh VS Code: `Ctrl+Shift+P` → "Reload Window"

---

### Can't Push from VS Code

**Cause:** Authentication issue

**Solution:**

1. Try from command line first:
```bash
cd /d F:\ArduinoWorkspace\libraries\LibName
git push origin main
```
2. If works, restart VS Code
3. Sign in to GitHub in VS Code:
   - Click account icon (bottom-left)
   - Sign in to Sync Settings

---

## GitHub Issues

### Can't Access Repository

**Cause:** Private repo without access, or deleted

**Solution:**

1. Verify URL in browser
2. Check repo exists: [github.com/username/repo](https://github.com/username/repo)
3. Check permissions if private repo
4. Verify GitHub username correct

---

### Changes Not Showing on GitHub

**Cause:** Not pushed, wrong branch, or wrong repo

**Solution:**

1. Check if pushed:
```bash
git status
# Should say: "Your branch is up to date"
```

2. If not pushed:
```bash
git push origin main
```

3. Verify on correct branch:
```bash
git branch
# Should show: * main
```

---

### Can't Create Release

**Cause:** No tags or permission issue

**Solution:**

1. Create tag first:
```bash
git tag -a v1.0.0 -m "Version 1.0"
git push origin v1.0.0
```

2. On GitHub:
   - Releases → Create new release
   - Choose tag: v1.0.0
   - Fill details
   - Publish

---

## Windows-Specific Issues

### "Filename too long"

**Cause:** Windows path length limit

**Solution:**
```bash
# Enable long paths in Git
git config --system core.longpaths true

# Or move workspace closer to root
# Instead of: C:\Users\Name\Documents\Arduino\...
# Use: F:\ArduinoWorkspace\...
```

---

### Line Ending Issues

**Cause:** Windows vs Unix line endings

**Solution:**
```bash
# Configure Git to handle automatically
git config --global core.autocrlf true
```

---

### "Access denied" on git clone

**Cause:** Antivirus or permissions

**Solution:**

1. Run CMD as Administrator
2. Temporarily disable antivirus
3. Clone to different drive (F: instead of C:)

---

## Network Issues

### Clone/Pull Very Slow

**Cause:** Large repository or slow connection

**Solution:**
```bash
# Shallow clone (faster, no history)
git clone --depth 1 https://github.com/username/repo.git

# Clone only specific branch
git clone --single-branch --branch main https://github.com/username/repo.git
```

---

### Behind Proxy

**Cause:** Corporate network blocks Git

**Solution:**
```bash
# Configure proxy
git config --global http.proxy http://proxy.server:port
git config --global https.proxy https://proxy.server:port

# Remove proxy
git config --global --unset http.proxy
git config --global --unset https.proxy
```

---

## Recovery Operations

### Deleted File by Mistake

**Before commit:**
```bash
git checkout -- filename.ino
```

**After commit:**
```bash
git checkout HEAD~1 -- filename.ino
git commit -m "Restore deleted file"
```

---

### Lost Commits After Reset

**Solution:**
```bash
# Find lost commit
git reflog

# Recover
git cherry-pick abc1234
# Or
git reset --hard abc1234
```

---

### Corrupted Repository

**Solution:**
```bash
# Verify corruption
git fsck

# If corrupt, re-clone
cd ..
mv corrupted-repo corrupted-repo-backup
git clone https://github.com/username/repo.git
```

---

## Performance Issues

### Git Commands Slow

**Solution:**
```bash
# Clean up repository
git gc --aggressive

# Reduce repository size
git prune
```

---

### Large Repository

**Solution:**

1. Use .gitignore properly
2. Remove large files from history:
```bash
git filter-branch --tree-filter 'rm -f large_file.bin' HEAD
```
3. Consider Git LFS for binary files

---

## Diagnostic Commands

### Check Git Installation

```bash
git --version
git config --list
```

### Check Repository Status

```bash
git status
git remote -v
git branch -a
git log --oneline -5
```

### Verify Files

```bash
git ls-files                # Tracked files
git ls-files --others      # Untracked files
git check-ignore -v file   # Why file ignored
```

---

## Emergency Recovery

### Complete Reset to Remote

**⚠️ DANGEROUS - Loses all local changes**

```bash
git fetch origin
git reset --hard origin/main
git clean -fd
```

### Start Fresh

**⚠️ Last resort**

```bash
cd ..
mv project-folder project-folder-backup
git clone https://github.com/username/project.git
# Copy any unsaved work from backup
```

---

## Getting Help

### Git Help

```bash
git help                    # General help
git help commit             # Help for specific command
git commit --help           # Same as above
```

### Community Resources

- **Git Documentation:** [git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Community:** [github.community](https://github.community)
- **Stack Overflow:** [stackoverflow.com/questions/tagged/git](https://stackoverflow.com/questions/tagged/git)

---

## Prevention Tips

**Avoid problems before they happen:**

1. ✅ Always pull before starting work
2. ✅ Commit frequently
3. ✅ Use meaningful commit messages
4. ✅ Keep .gitignore updated
5. ✅ Test before committing
6. ✅ Push at end of day
7. ✅ Don't commit large binaries
8. ✅ Don't force push unless necessary

---

**Still stuck?** Create issue on GitHub or check [git-scm.com/doc](https://git-scm.com/doc)
