# Visual Workflow Guide - Arduino Git

**Diagrams and flowcharts for quick reference**

---

## Daily Workflow

```
┌─────────────────────────────────────────────────┐
│              DAILY GIT WORKFLOW                  │
└─────────────────────────────────────────────────┘

    START (Morning)
         │
         ▼
    ┌─────────────┐
    │  git pull   │  ◄── Sync with GitHub
    │ origin main │
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │ Edit Files  │  ◄── Arduino IDE / VS Code
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │ git status  │  ◄── Check changes
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │  git add .  │  ◄── Stage all
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │ git commit  │  ◄── Save snapshot
    │ -m "message"│
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │  git push   │  ◄── Upload to GitHub
    │ origin main │
    └──────┬──────┘
           │
           ▼
      DONE (Evening)


ONE-LINE VERSION:
git pull origin main && git add . && git commit -m "Msg" && git push origin main
```

---

## Repository Creation

### Method A: GitHub First

```
    START
      │
      ▼
┌──────────────────┐
│ Create repo on   │  ◄── github.com
│ GitHub (web)     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ git clone <URL>  │  ◄── Download to PC
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Add .ino files   │  ◄── Arduino IDE
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ git add .        │
│ git commit       │
│ git push         │
└────────┬─────────┘
         │
         ▼
      DONE
```

### Method B: Local First

```
    START
      │
      ▼
┌──────────────────┐
│ Existing folder  │
│ with .ino files  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ git init         │  ◄── Initialize repo
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ git add .        │
│ git commit       │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Create repo on   │  ◄── GitHub (empty)
│ GitHub (web)     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ git remote add   │  ◄── Connect repos
│ git push         │
└────────┬─────────┘
         │
         ▼
      DONE
```

---

## File Lifecycle

```
┌───────────────────────────────────────────────────┐
│           FILE STATES IN GIT                      │
└───────────────────────────────────────────────────┘

UNTRACKED    MODIFIED     STAGED      COMMITTED
(New file)   (Changed)    (Ready)     (Saved)
    │            │            │            │
    ▼            ▼            ▼            ▼
┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐
│ .ino   │  │Changed │  │ Ready  │  │ Saved  │
│ file   │  │ .ino   │  │  to    │  │   in   │
│created │  │ file   │  │ Commit │  │History │
└───┬────┘  └───┬────┘  └───┬────┘  └────────┘
    │           │            │
    │ git add . │ git add .  │ git commit
    │           │            │
    └───────────┴────────────┘


COMMANDS BY STATE:

Untracked → Staged:      git add filename.ino
Modified → Staged:       git add .
Staged → Committed:      git commit -m "Message"
Staged → Modified:       git reset HEAD filename
Modified → Original:     git checkout -- filename
```

---

## Branch Workflow

```
         MAIN BRANCH (Production)
              │
              │ Stable code
              ▼
        ┌─────────┐
        │ Commit  │
        │ Commit  │
        └────┬────┘
             │
             │ git checkout -b new-feature
             │
         ╔═══╩═══╗
         ║       ║
    ┌────▼───┐   ║         FEATURE BRANCH
    │Feature │   ║              │
    │ Work  │   ║              │ Experimental
    │ Work  │   ║              ▼
    └────┬───┘   ║         ┌────────┐
         │       ║         │ Test   │
         │       ║         │ Test   │
         │ git checkout main        └────────┘
         │       ║
         ╚═══╦═══╝
             │
             │ git merge new-feature
             │
        ┌────▼────┐
        │ Merged  │
        │  Code   │
        └─────────┘
```

---

## Conflict Resolution

```
    git pull origin main
         │
         ▼
    ┌─────────┐
    │Conflict?│
    └────┬────┘
         │
    ┌────┴────┐
    NO         YES
    │          │
    ▼          ▼
  DONE    ┌──────────────┐
          │ Open file    │
          │ See markers: │
          │ <<<<<<<      │
          │ =======      │
          │ >>>>>>>      │
          └──────┬───────┘
                 │
                 ▼
          ┌──────────────┐
          │ Edit file    │
          │ Choose code  │
          │ Remove marks │
          └──────┬───────┘
                 │
                 ▼
          ┌──────────────┐
          │ git add file │
          └──────┬───────┘
                 │
                 ▼
          ┌──────────────┐
          │ git commit   │
          └──────┬───────┘
                 │
                 ▼
               DONE
```

---

## Push/Pull Sync

```
┌─────────────────────────────────────────────────┐
│        YOUR PC  ↔  GITHUB SERVER                │
└─────────────────────────────────────────────────┘

   LOCAL REPOSITORY          REMOTE REPOSITORY

┌────────────────┐          ┌────────────────┐
│                │          │                │
│ Working Files  │          │   main branch  │
│ (F:\Arduino... │          │   (Online)     │
│                │          │                │
└───────┬────────┘          └────────┬───────┘
        │                            │
        │ git add .                  │
        │ git commit                 │
        │                            │
        ▼                            │
┌────────────────┐                   │
│ Local Commits  │                   │
└───────┬────────┘                   │
        │                            │
        │ git push origin main       │
        ├───────────────────────────►│
        │                            │
        │ git pull origin main       │
        │◄───────────────────────────┤
        │                            │
        ▼                            ▼
    SYNCHRONIZED               SYNCHRONIZED
```

---

## Multi-PC Workflow

```
┌─────────────────────────────────────────────────┐
│        WORK FROM ANYWHERE                       │
└─────────────────────────────────────────────────┘

    OFFICE PC                GITHUB               HOME PC
        │                       │                     │
        │ Morning               │                     │
        │ git pull              │                     │
        ├──────────────────────►│                     │
        │                       │                     │
        │ Edit code             │                     │
        │                       │                     │
        │ Evening               │                     │
        │ git push              │                     │
        ├──────────────────────►│                     │
        │                       │                     │
        │                       │  Evening            │
        │                       │  git pull           │
        │                       │◄────────────────────┤
        │                       │                     │
        │                       │  Edit code          │
        │                       │                     │
        │                       │  Night              │
        │                       │  git push           │
        │                       │◄────────────────────┤
        │                       │                     │
        │ Next Morning          │                     │
        │ git pull              │                     │
        ├──────────────────────►│                     │
        │ (gets changes)        │                     │


KEY: Always git pull before starting work!
```

---

## Version History

```
    COMMIT TIMELINE

┌─────────┐
│ v3.0    │ ◄─── HEAD (current)
├─────────┤
│ v2.5    │ ◄─── HEAD~1 (previous)
├─────────┤
│ v2.0    │ ◄─── HEAD~2
├─────────┤
│ v1.0    │ ◄─── HEAD~3
└─────────┘


NAVIGATION:

git reset --soft HEAD~1
    └─► Undo commit, KEEP changes (staged)

git reset HEAD~1
    └─► Undo commit, KEEP changes (unstaged)

git reset --hard HEAD~1
    └─► Undo commit, DISCARD changes ⚠️

git revert HEAD
    └─► Create NEW commit that undoes previous
```

---

## Library Installation Flow

```
INSTALL ARDUINO LIBRARY FROM GITHUB

    START
      │
      ▼
┌─────────────────┐
│ Open CMD        │
└────────┬────────┘
         │
         ▼
┌─────────────────────────────┐
│ cd F:\ArduinoWorkspace\     │
│    libraries                │
└────────┬────────────────────┘
         │
         ▼
┌─────────────────────────────┐
│ git clone                   │
│ https://github.com/         │
│ user/LibName.git            │
└────────┬────────────────────┘
         │
         ▼
┌─────────────────┐
│ Restart         │
│ Arduino IDE     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Library         │
│ Available! ✓    │
└─────────────────┘


UPDATE LATER:

┌─────────────────┐
│ cd LibName      │
│ git pull        │
└─────────────────┘
```

---

## Decision Tree

```
               WHAT DO I NEED?
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
  Get latest    Make changes   Fix mistake
   from repo       to code         │
        │            │             │
        ▼            ▼             ▼
   git pull     git add .     git checkout
   origin      git commit         --
    main        git push       file.ino


               WHAT DO I NEED?
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
   Start new    Download lib   Create tag
   project      from GitHub    (version)
        │            │             │
        ▼            ▼             ▼
   git init     git clone      git tag
      or           <URL>        v1.0.0
   git clone


               WHAT DO I NEED?
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
  Check what     See commit    Work on new
  changed         history        feature
        │            │             │
        ▼            ▼             ▼
   git status    git log      git checkout
                 --oneline    -b feature
```

---

## Project Structure

```
RECOMMENDED ARDUINO PROJECT LAYOUT

MyProject/
├── MyProject/
│   ├── MyProject.ino       ◄── Main sketch
│   └── config.h            ◄── Configuration
├── docs/
│   ├── README.md
│   └── INSTALLATION.md
├── hardware/
│   ├── schematic.png
│   └── wiring.png
├── examples/
│   └── test/
│       └── test.ino
├── .gitignore              ◄── Exclude builds
└── README.md               ◄── Main docs


LIBRARY LAYOUT

MyLibrary/
├── src/
│   ├── MyLibrary.h         ◄── Header
│   ├── MyLibrary.cpp       ◄── Implementation
│   └── config.h
├── examples/
│   ├── Basic/
│   │   └── Basic.ino
│   └── Advanced/
│       └── Advanced.ino
├── library.properties      ◄── Metadata
├── .gitignore
└── README.md
```

---

## Workspace Organization

```
F:\ArduinoWorkspace\
│
├── libraries\                    ◄── Custom libraries
│   ├── RajivButton\              ◄── Git repo
│   │   ├── src\
│   │   ├── examples\
│   │   └── .git\
│   ├── RajivRelay\               ◄── Git repo
│   └── RajivSensorDI\            ◄── Git repo
│
└── projects\                     ◄── Arduino sketches
    ├── DoorSecurityAlarm\        ◄── Git repo
    │   ├── DoorSecurityAlarm\
    │   │   └── DoorSecurityAlarm.ino
    │   ├── .git\
    │   └── README.md
    └── WaterTankController\      ◄── Git repo
        ├── WaterTankController\
        └── .git\


ARDUINO IDE CONFIG:
Sketchbook Location → F:\ArduinoWorkspace
```

---

## Local vs Remote

```
┌─────────────────────────────────────────────────┐
│      LOCAL REPOSITORY vs REMOTE REPOSITORY      │
└─────────────────────────────────────────────────┘

    YOUR COMPUTER              GITHUB.COM
    (Local Repo)               (Remote Repo)
         │                          │
         ▼                          ▼
    ┌──────────┐              ┌──────────┐
    │ Working  │              │  origin  │
    │   Dir    │              │  /main   │
    └────┬─────┘              └────▲─────┘
         │                         │
         │ git add                 │
         ▼                         │
    ┌──────────┐                  │
    │ Staging  │                  │
    │   Area   │                  │
    └────┬─────┘                  │
         │                        │
         │ git commit             │
         ▼                        │
    ┌──────────┐                  │
    │  Local   │                  │
    │   Repo   │                  │
    └────┬─────┘                  │
         │                        │
         │ git push origin main   │
         └────────────────────────┘


NOTE:
- Local changes don't auto-sync to GitHub
- GitHub changes don't auto-sync to PC
- You control sync with push/pull
```

---

## Learning Path

```
    BEGINNER                INTERMEDIATE          ADVANCED
        │                       │                    │
        ▼                       ▼                    ▼
┌───────────────┐       ┌──────────────┐    ┌─────────────┐
│ git clone     │       │ Branching    │    │ Rebasing    │
│ git pull      │       │ Merging      │    │ Cherry-pick │
│ git add       │       │ Conflicts    │    │ Submodules  │
│ git commit    │       │ Tags         │    │ Hooks       │
│ git push      │       │ .gitignore   │    │ Advanced    │
│ git status    │       │ Remotes      │    │ workflows   │
└───────────────┘       └──────────────┘    └─────────────┘
        │                       │                    │
    START HERE!            After mastery          Expert
        │                       │                  level
        └───────────────────────┘
               Learn these next


RECOMMENDED LEARNING SEQUENCE:
Week 1: Basic commands (clone, pull, add, commit, push)
Week 2: Status, log, diff (understanding changes)
Week 3: Undo operations (checkout, reset)
Week 4: Branching basics
Week 5+: Advanced features as needed
```

---

## Quick Command Map

```
┌─────────────────────────────────────────────────┐
│            COMMON GIT OPERATIONS                │
└─────────────────────────────────────────────────┘

SYNC
↓ git pull origin main          Get latest
↑ git push origin main          Upload changes

SAVE
+ git add .                     Stage all
✓ git commit -m "msg"           Commit

INFO
? git status                    Current state
📜 git log --oneline            History
👁 git diff                     Changes

UNDO
↶ git checkout -- file          Discard changes
↩ git reset HEAD file           Unstage
⏪ git reset --soft HEAD~1      Undo commit

START
🆕 git init                     New repo
📦 git clone <url>              Copy repo
```

---

**Save these diagrams for quick visual reference!** 📊
