# 📊 Git Workflow Visual Guide - Arduino Projects

**Interactive flowcharts for common scenarios**

---

## 🔄 Daily Workflow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    DAILY GIT WORKFLOW                       │
└─────────────────────────────────────────────────────────────┘

    START
      │
      ▼
┌──────────────┐
│  git pull    │  ← Get latest from GitHub
│ origin main  │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Edit Files   │  ← Work in Arduino IDE
│ (Arduino IDE)│
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ git status   │  ← See what changed
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  git add .   │  ← Stage all changes
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ git commit   │  ← Save snapshot locally
│ -m "message" │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  git push    │  ← Upload to GitHub
│ origin main  │
└──────┬───────┘
       │
       ▼
     DONE! ✓
```

---

## 🆕 Creating New Repository

### **Method A: GitHub First**

```
    START
      │
      ▼
┌─────────────────────┐
│ Create repo on      │
│ github.com          │
│ - Click "+"         │
│ - New repository    │
│ - Name it           │
│ - Create            │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ git clone <URL>     │  ← Download to PC
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Add your files      │  ← Copy .ino files
│ (Arduino sketch)    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ git add .           │
│ git commit -m "msg" │
│ git push origin main│
└──────────┬──────────┘
           │
           ▼
         DONE! ✓
```

### **Method B: Local PC First**

```
    START
      │
      ▼
┌─────────────────────┐
│ Your existing       │
│ Arduino folder      │
│ (on PC)             │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ git init            │  ← Initialize Git
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ git add .           │  ← Stage files
│ git commit -m "msg" │  ← First commit
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Create empty repo   │
│ on github.com       │
│ (DON'T add README)  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ git remote add      │  ← Connect
│ origin <URL>        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ git push -u         │  ← Upload
│ origin main         │
└──────────┬──────────┘
           │
           ▼
         DONE! ✓
```

---

## 🔀 Branching Workflow

```
         MAIN BRANCH
              │
              ▼
    ┌─────────────────┐
    │   Stable Code   │
    │   (main)        │
    └────────┬────────┘
             │
             │ git checkout -b new-feature
             │
         ╔═══╩═══╗
         ║       ║
    ┌────▼────┐  ║
    │ Feature │  ║
    │ Branch  │  ║
    └────┬────┘  ║
         │       ║
    ┌────▼────┐  ║
    │  Work   │  ║
    │  Work   │  ║
    │  Work   │  ║
    └────┬────┘  ║
         │       ║
    ┌────▼────┐  ║
    │ Commit  │  ║
    │ Commit  │  ║
    └────┬────┘  ║
         │       ║
         │ git checkout main
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

## 🚨 Conflict Resolution Flow

```
    git pull origin main
         │
         ▼
    ┌─────────┐
    │Conflict?│
    └────┬────┘
         │
    ┌────┴────┐
    │   NO    │   YES
    │    │    │    │
    │    ▼    │    ▼
    │  DONE!  │  ┌──────────────────┐
    │         │  │ Open file with   │
    │         │  │ conflict markers │
    │         │  └────────┬─────────┘
    │         │           │
    │         │           ▼
    │         │  ┌──────────────────┐
    │         │  │ <<<<<<< HEAD     │
    │         │  │ Your changes     │
    │         │  │ =======          │
    │         │  │ Their changes    │
    │         │  │ >>>>>>> branch   │
    │         │  └────────┬─────────┘
    │         │           │
    │         │           ▼
    │         │  ┌──────────────────┐
    │         │  │ Edit file:       │
    │         │  │ Keep what needed │
    │         │  │ Delete markers   │
    │         │  └────────┬─────────┘
    │         │           │
    │         │           ▼
    │         │  ┌──────────────────┐
    │         │  │ git add file.ino │
    │         │  └────────┬─────────┘
    │         │           │
    │         │           ▼
    │         │  ┌──────────────────┐
    │         │  │ git commit -m    │
    │         │  │ "Resolved"       │
    │         │  └────────┬─────────┘
    │         │           │
    └─────────┴───────────┘
              │
              ▼
           DONE! ✓
```

---

## 📂 File Lifecycle States

```
┌─────────────────────────────────────────────────────────────┐
│                FILE STATES IN GIT                           │
└─────────────────────────────────────────────────────────────┘

    UNTRACKED           MODIFIED          STAGED         COMMITTED
   (New File)        (Changed File)    (Added File)    (Saved File)
        │                  │                │               │
        │                  │                │               │
    ┌───▼───┐          ┌───▼───┐       ┌───▼───┐      ┌───▼───┐
    │ New   │          │Changed│       │ Ready │      │Snapshot│
    │ File  │          │ File  │       │  to   │      │ Saved  │
    │ .ino  │          │ .ino  │       │Commit │      │   in   │
    └───┬───┘          └───┬───┘       └───┬───┘      │ History│
        │                  │                │          └────────┘
        │ git add .        │ git add .      │ git commit
        │                  │                │
        └──────────────────┴────────────────┘


COMMANDS:
    git add .       → Moves UNTRACKED/MODIFIED to STAGED
    git commit      → Moves STAGED to COMMITTED
    git reset HEAD  → Moves STAGED back to MODIFIED
    git checkout -- → Discards MODIFIED changes
```

---

## 🔄 Push/Pull Cycle

```
┌─────────────────────────────────────────────────────────────┐
│           YOUR PC  ↔️  GITHUB SERVER                        │
└─────────────────────────────────────────────────────────────┘

    YOUR LOCAL                           GITHUB REMOTE
    REPOSITORY                           REPOSITORY

┌──────────────────┐                 ┌──────────────────┐
│                  │                 │                  │
│  Working Copy    │                 │   main branch    │
│  (Your files)    │                 │   (Online)       │
│                  │                 │                  │
└────────┬─────────┘                 └────────┬─────────┘
         │                                    │
         │ git add .                          │
         │ git commit                         │
         │                                    │
         ▼                                    │
┌──────────────────┐                          │
│                  │                          │
│  Local Commits   │                          │
│  (Staged)        │                          │
│                  │                          │
└────────┬─────────┘                          │
         │                                    │
         │ git push origin main               │
         │ ──────────────────────────────────▶│
         │                                    │
         │                                    │
         │ git pull origin main               │
         │ ◀──────────────────────────────────│
         │                                    │
         ▼                                    ▼
    SYNCHRONIZED ✓                    SYNCHRONIZED ✓
```

---

## 🎯 Decision Tree: What Command Do I Need?

```
                        START
                          │
                          ▼
                 ┌────────────────┐
                 │  What do you   │
                 │  want to do?   │
                 └────────┬───────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
   Get latest      Make changes       Undo mistake
   from GitHub       to code           in code
        │                 │                 │
        ▼                 ▼                 ▼
   git pull         git add .         git checkout --
   origin main      git commit        filename.ino
                    git push

                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
   Start new        Download           Create
   project         someone's         version
                   library           tag
        │                 │                 │
        ▼                 ▼                 ▼
   git init         git clone          git tag
   OR                <URL>              v1.0.0
   git clone

                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
   Check what      See commit         Work on
   changed         history          new feature
        │                 │                 │
        ▼                 ▼                 ▼
   git status      git log            git checkout
                   --oneline          -b feature-name
```

---

## 📥 Installing Arduino Library from GitHub

```
    START: Want to use RajivRelay library
              │
              ▼
    ┌──────────────────────┐
    │ Open CMD/PowerShell  │
    └──────────┬───────────┘
               │
               ▼
    ┌──────────────────────┐
    │ cd C:\Users\YourName │
    │ \Documents\Arduino   │
    │ \libraries           │
    └──────────┬───────────┘
               │
               ▼
    ┌──────────────────────┐
    │ git clone            │
    │ https://github.com/  │
    │ Rajiv/RajivRelay.git │
    └──────────┬───────────┘
               │
               ▼
    ┌──────────────────────┐
    │ Restart Arduino IDE  │
    └──────────┬───────────┘
               │
               ▼
    ┌──────────────────────┐
    │ Library appears in   │
    │ Sketch → Include     │
    │ Library menu ✓       │
    └──────────┬───────────┘
               │
               ▼
             DONE!


    UPDATE LIBRARY LATER:
    ┌──────────────────────┐
    │ cd RajivRelay        │
    │ git pull origin main │
    └──────────────────────┘
```

---

## 🎨 Project Structure Flow

```
NEW ARDUINO PROJECT
         │
         ▼
┌─────────────────────────────────────┐
│  Create folder structure:           │
│                                      │
│  MyProject/                          │
│  ├── MyProject/                      │
│  │   ├── MyProject.ino   ← Sketch   │
│  │   └── config.h        ← Config   │
│  ├── docs/               ← Docs     │
│  ├── hardware/           ← Circuits │
│  ├── .gitignore          ← Exclude  │
│  └── README.md           ← Main doc │
└──────────────┬──────────────────────┘
               │
               ▼
┌──────────────────────────┐
│  Create .gitignore:      │
│  *.hex                   │
│  *.bin                   │
│  build/                  │
│  libraries/              │
└──────────────┬───────────┘
               │
               ▼
┌──────────────────────────┐
│  git init                │
│  git add .               │
│  git commit -m "Initial" │
└──────────────┬───────────┘
               │
               ▼
┌──────────────────────────┐
│  Create repo on GitHub   │
│  git remote add origin   │
│  git push -u origin main │
└──────────────┬───────────┘
               │
               ▼
         PROJECT ON GITHUB! ✓
```

---

## ⏪ Time Machine: Going Back in History

```
    COMMIT HISTORY
         │
    ┌────▼────┐
    │ v3.0    │ ← HEAD (current)
    ├─────────┤
    │ v2.5    │ ← HEAD~1 (previous)
    ├─────────┤
    │ v2.0    │ ← HEAD~2
    ├─────────┤
    │ v1.0    │ ← HEAD~3
    └─────────┘


UNDO COMMANDS:

git reset --soft HEAD~1
    ↓
Undo commit, KEEP changes
(Changes still staged)

git reset HEAD~1
    ↓
Undo commit, KEEP changes
(Changes unstaged)

git reset --hard HEAD~1
    ↓
Undo commit, DISCARD changes
⚠️ DANGEROUS! Can't recover!

git revert HEAD
    ↓
Create NEW commit that
undoes previous commit
(Safe, keeps history)
```

---

## 🌐 Local vs Remote Repositories

```
┌─────────────────────────────────────────────────────────────┐
│                LOCAL vs REMOTE                              │
└─────────────────────────────────────────────────────────────┘

    YOUR COMPUTER              GITHUB.COM
    (Local Repo)               (Remote Repo)
         │                          │
         │                          │
    ┌────▼────────┐           ┌─────▼───────┐
    │ Working Dir │           │   origin    │
    │ (files you  │           │   /main     │
    │  can edit)  │           │  (online)   │
    └────┬────────┘           └─────▲───────┘
         │                          │
         │ git add                  │
         ▼                          │
    ┌────────────┐                  │
    │  Staging   │                  │
    │   Area     │                  │
    │ (prepared) │                  │
    └────┬───────┘                  │
         │                          │
         │ git commit               │
         ▼                          │
    ┌────────────┐                  │
    │   Local    │                  │
    │ Repository │                  │
    │  (saved)   │                  │
    └────┬───────┘                  │
         │                          │
         │ git push origin main     │
         └──────────────────────────┘


REMEMBER:
- Local changes DON'T automatically go to GitHub
- GitHub changes DON'T automatically come to your PC
- You control when to sync with push/pull
```

---

## 🎓 Learning Progression Path

```
    BEGINNER             INTERMEDIATE          ADVANCED
        │                     │                    │
        ▼                     ▼                    ▼
┌───────────────┐     ┌──────────────┐    ┌─────────────┐
│ git clone     │     │ Branching    │    │ Rebasing    │
│ git pull      │     │ Merging      │    │ Cherry-pick │
│ git add       │     │ Resolving    │    │ Submodules  │
│ git commit    │     │ conflicts    │    │ Hooks       │
│ git push      │     │ Tags         │    │ Advanced    │
│ git status    │     │ .gitignore   │    │ workflows   │
└───────────────┘     └──────────────┘    └─────────────┘
        │                     │                    │
    Master these          Then learn            Expert
    FIRST!               these next             level


START HERE ─────────────────────────────────────────────▶
```

---

**Save these diagrams for quick visual reference!** 📊✨
