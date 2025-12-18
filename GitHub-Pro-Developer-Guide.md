# GitHub Pro-Level Developer Guide 🚀

A comprehensive guide to mastering GitHub as a professional developer.

## Table of Contents

1. [Git Fundamentals](#1-git-fundamentals)
2. [Repository Management](#2-repository-management)
3. [Branching Strategies](#3-branching-strategies)
4. [Commit Best Practices](#4-commit-best-practices)
5. [Pull Requests & Code Review](#5-pull-requests--code-review)
6. [GitHub Actions & CI/CD](#6-github-actions--cicd)
7. [Collaboration Workflows](#7-collaboration-workflows)
8. [Advanced Git Techniques](#8-advanced-git-techniques)
9. [Security & Best Practices](#9-security--best-practices)
10. [GitHub Features](#10-github-features)
11. [Troubleshooting](#11-troubleshooting)
12. [Pro Tips & Tricks](#12-pro-tips--tricks)

---

## 1. Git Fundamentals

### Understanding Git

Git is a **distributed version control system** - every developer has a full copy of the repository.

#### Key Concepts

**Repository (Repo)**
- Complete project history and files
- Local (on your machine) and Remote (on GitHub)

**Commit**
- Snapshot of your changes
- Has unique SHA hash
- Contains author, timestamp, message

**Branch**
- Pointer to a commit
- Independent line of development
- Default branch usually `main` or `master`

**HEAD**
- Pointer to current branch/commit
- Where you are right now in repository

### Essential Git Commands

#### Setup & Configuration

```bash
# Set your identity (do this once)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default editor
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim

# Set default branch name
git config --global init.defaultBranch main

# View all settings
git config --list

# Edit global config
git config --global --edit
```

#### Repository Operations

```bash
# Initialize new repository
git init

# Clone existing repository
git clone https://github.com/username/repo.git
git clone git@github.com:username/repo.git  # SSH

# Clone to specific directory
git clone https://github.com/username/repo.git my-folder

# Shallow clone (faster, less history)
git clone --depth 1 https://github.com/username/repo.git

# View remote repositories
git remote -v

# Add remote
git remote add origin https://github.com/username/repo.git

# Change remote URL
git remote set-url origin https://github.com/username/new-repo.git

# Remove remote
git remote remove origin
```

#### Basic Workflow

```bash
# Check status of working directory
git status

# Add files to staging area
git add filename.txt              # Single file
git add *.js                      # All JS files
git add .                         # All files
git add -p                        # Interactive staging

# Commit changes
git commit -m "Brief description"
git commit -m "Title" -m "Detailed description"

# Add and commit in one step (tracked files only)
git commit -am "Message"

# Amend last commit (before pushing!)
git commit --amend -m "New message"
git commit --amend --no-edit      # Keep same message

# Push to remote
git push origin main
git push                          # If upstream is set

# Pull from remote
git pull origin main
git pull                          # If upstream is set

# Fetch without merging
git fetch origin
```

### The Three States of Git

```
Working Directory → Staging Area → Repository
      ↓                  ↓              ↓
   (modified)        (staged)      (committed)
      ↓                  ↓              ↓
   git add          git commit      git push
```

---

## 2. Repository Management

### Creating a Repository

#### On GitHub

1. **Via Web Interface**
   - Click "+" → "New repository"
   - Choose name, description, visibility
   - Initialize with README (optional)
   - Add .gitignore and license

2. **Via GitHub CLI**
```bash
# Install GitHub CLI
# https://cli.github.com/

# Authenticate
gh auth login

# Create repository
gh repo create my-project --public
gh repo create my-project --private --source=.
```

#### Locally Then Push

```bash
# Method 1: Start locally
mkdir my-project
cd my-project
git init
git add .
git commit -m "Initial commit"

# Create on GitHub (via CLI or web), then:
git remote add origin https://github.com/username/my-project.git
git branch -M main
git push -u origin main

# Method 2: Clone from GitHub
gh repo create my-project --public
git clone https://github.com/username/my-project.git
cd my-project
# Start working...
```

### Repository Structure Best Practices

```
my-project/
├── .github/                    # GitHub specific files
│   ├── workflows/             # GitHub Actions
│   ├── ISSUE_TEMPLATE/        # Issue templates
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── CODEOWNERS            # Code ownership
├── docs/                      # Documentation
├── src/                       # Source code
├── tests/                     # Test files
├── .gitignore                # Git ignore rules
├── .editorconfig             # Editor config
├── README.md                 # Project readme
├── LICENSE                   # License file
├── CONTRIBUTING.md           # Contribution guide
├── CHANGELOG.md              # Version history
└── package.json              # Project metadata
```

### .gitignore Best Practices

```gitignore
# Operating System
.DS_Store
Thumbs.db
desktop.ini

# IDE/Editor
.vscode/
.idea/
*.swp
*.swo
*~

# Dependencies
node_modules/
vendor/
venv/
*.egg-info/

# Build outputs
build/
dist/
*.o
*.so
*.exe

# Environment variables
.env
.env.local
secrets.yml

# Logs
*.log
logs/

# Temporary files
tmp/
temp/
*.tmp

# Test coverage
coverage/
.coverage
htmlcov/
```

**Pro Tip:** Use https://gitignore.io to generate .gitignore files

---

## 3. Branching Strategies

### Why Branch?

- **Isolation**: Work independently on features
- **Collaboration**: Multiple developers simultaneously
- **Safety**: Don't break main/production code
- **Review**: Code review before merging

### Common Branching Models

#### 1. GitHub Flow (Simple, Recommended)

```
main (production-ready)
  ├── feature/new-feature
  ├── bugfix/fix-bug
  └── hotfix/urgent-fix
```

**Workflow:**
```bash
# 1. Create branch from main
git checkout main
git pull origin main
git checkout -b feature/user-authentication

# 2. Make changes and commit
git add .
git commit -m "Add user login functionality"

# 3. Push to GitHub
git push -u origin feature/user-authentication

# 4. Open Pull Request on GitHub

# 5. After review and merge, delete branch
git checkout main
git pull origin main
git branch -d feature/user-authentication
```

#### 2. Git Flow (Complex, Enterprise)

```
main (production)
  ├── develop (integration)
  │   ├── feature/feature-1
  │   ├── feature/feature-2
  │   └── feature/feature-3
  ├── release/v1.2.0
  └── hotfix/critical-bug
```

**Workflow:**
```bash
# Initialize Git Flow
git flow init

# Start new feature
git flow feature start new-feature
# Work on feature...
git flow feature finish new-feature

# Start release
git flow release start 1.2.0
# Prepare release...
git flow release finish 1.2.0

# Emergency hotfix
git flow hotfix start critical-fix
# Fix bug...
git flow hotfix finish critical-fix
```

#### 3. Trunk-Based Development (Modern, CI/CD)

```
main (always deployable)
  ├── short-lived-feature-1 (< 2 days)
  └── short-lived-feature-2 (< 2 days)
```

**Principles:**
- Small, frequent commits to main
- Feature flags for incomplete features
- Strong automated testing
- Continuous integration

### Branch Naming Conventions

```bash
# Feature branches
feature/user-authentication
feature/add-payment-gateway
feat/implement-search

# Bug fixes
bugfix/fix-login-error
fix/correct-calculation
bug/header-alignment

# Hotfix (urgent production fix)
hotfix/security-patch
hotfix/critical-crash

# Release branches
release/v1.2.0
release/2024-01-15

# Documentation
docs/update-readme
docs/api-documentation

# Refactoring
refactor/database-layer
refactor/cleanup-tests

# Experimental
experiment/new-algorithm
spike/performance-test
```

### Branch Operations

```bash
# List branches
git branch                    # Local branches
git branch -r                # Remote branches
git branch -a                # All branches

# Create branch
git branch feature-name
git checkout -b feature-name  # Create and switch
git switch -c feature-name    # Modern syntax

# Switch branches
git checkout main
git switch main              # Modern syntax

# Rename branch
git branch -m old-name new-name
git branch -m new-name       # Rename current branch

# Delete branch
git branch -d feature-name   # Safe delete (merged only)
git branch -D feature-name   # Force delete

# Delete remote branch
git push origin --delete feature-name

# Track remote branch
git branch --set-upstream-to=origin/main main
git push -u origin feature-name  # Set upstream while pushing

# List merged branches
git branch --merged
git branch --no-merged

# View branch history
git log --oneline --graph --all --decorate
```

---

## 4. Commit Best Practices

### Commit Message Format

#### Conventional Commits (Industry Standard)

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style (formatting, missing semicolons)
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks
- `perf`: Performance improvement
- `ci`: CI/CD changes
- `build`: Build system changes
- `revert`: Revert previous commit

**Examples:**

```bash
# Simple commit
git commit -m "feat: add user login functionality"

# With scope
git commit -m "fix(auth): correct password validation"

# With body
git commit -m "feat: implement payment gateway" -m "
- Add Stripe integration
- Create payment processing module
- Add error handling for failed transactions
- Update database schema
"

# Breaking change
git commit -m "feat!: redesign API endpoints" -m "
BREAKING CHANGE: API v1 endpoints are deprecated.
Migrate to v2 endpoints before June 2024.
"

# Reference issue
git commit -m "fix: resolve login timeout issue

Fixes #123
"
```

### Commit Best Practices

#### DO ✅

```bash
# 1. Atomic commits (one logical change)
git commit -m "fix: correct email validation regex"

# 2. Present tense
git commit -m "add user profile page"  # ✅
git commit -m "added user profile"     # ❌

# 3. Descriptive but concise (50 chars title)
git commit -m "feat: implement JWT authentication"

# 4. Use body for complex changes
git commit -m "refactor: restructure database layer" -m "
- Extract database operations into separate service
- Add connection pooling
- Implement retry logic
- Add comprehensive error handling
"

# 5. Reference issues/tickets
git commit -m "fix: resolve memory leak in upload handler

The issue was caused by event listeners not being properly
cleaned up after file upload completion.

Fixes #456
Closes #457
"
```

#### DON'T ❌

```bash
# Vague messages
git commit -m "fix bug"
git commit -m "update"
git commit -m "changes"

# Multiple unrelated changes
git commit -m "fix login and add dashboard and update readme"

# Past tense
git commit -m "fixed the login bug"

# Too long titles
git commit -m "this commit fixes the bug where users couldn't login when their session expired because the token refresh wasn't working properly"
```

### Managing Commits

```bash
# View commit history
git log
git log --oneline
git log --graph --oneline --all
git log --author="John Doe"
git log --since="2 weeks ago"
git log --grep="login"

# Show specific commit
git show commit-hash
git show HEAD
git show HEAD~2  # 2 commits before HEAD

# Compare commits
git diff commit1 commit2
git diff HEAD HEAD~1

# Amend last commit (before pushing!)
git commit --amend -m "New message"
git add forgotten-file
git commit --amend --no-edit

# Interactive rebase (rewrite history - use carefully!)
git rebase -i HEAD~3

# Cherry-pick (apply specific commit)
git cherry-pick commit-hash

# Revert commit (creates new commit)
git revert commit-hash

# Reset (dangerous - rewrites history)
git reset --soft HEAD~1   # Keep changes staged
git reset --mixed HEAD~1  # Keep changes unstaged (default)
git reset --hard HEAD~1   # Discard changes completely
```

### Signing Commits (Security)

```bash
# Generate GPG key
gpg --full-generate-key

# List keys
gpg --list-secret-keys --keyid-format=long

# Configure Git to use GPG
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true

# Sign a commit
git commit -S -m "feat: add secure feature"

# Verify signature
git log --show-signature
```

---

## 5. Pull Requests & Code Review

### Creating Pull Requests

#### Via GitHub Web Interface

1. Push branch to GitHub
2. Navigate to repository
3. Click "Compare & pull request"
4. Fill in title and description
5. Select reviewers
6. Add labels, milestone, projects
7. Create pull request

#### Via GitHub CLI

```bash
# Create PR
gh pr create --title "Add user authentication" \
             --body "Implements login and registration"

# Create PR with template
gh pr create --fill

# Create draft PR
gh pr create --draft

# Create PR and assign reviewers
gh pr create --reviewer username1,username2

# Set base branch
gh pr create --base develop
```

### PR Template

Create `.github/PULL_REQUEST_TEMPLATE.md`:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Refactoring
- [ ] Performance improvement

## How Has This Been Tested?
Describe the tests that you ran to verify your changes.

- [ ] Unit tests
- [ ] Integration tests
- [ ] Manual testing

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review of my code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
- [ ] Any dependent changes have been merged and published

## Screenshots (if applicable)
Add screenshots to help explain your changes

## Related Issues
Closes #123
Relates to #456

## Additional Notes
Any additional information
```

### Code Review Best Practices

#### As a Reviewer

**DO ✅**

```markdown
# Be constructive
"Consider extracting this logic into a separate function for better readability."

# Ask questions
"Can you explain why you chose this approach over using the built-in method?"

# Praise good work
"Nice refactoring! This is much cleaner."

# Be specific
"Line 45: This variable name is unclear. Consider renaming to `userEmailAddress`"

# Suggest alternatives
"Have you considered using async/await here instead of promises?"

# Focus on code, not person
"This function could be simplified" ✅
"You're making this too complicated" ❌
```

**Review Checklist:**

- [ ] Code works as intended
- [ ] No obvious bugs or logic errors
- [ ] Follows coding standards
- [ ] No security vulnerabilities
- [ ] Performance considerations addressed
- [ ] Edge cases handled
- [ ] Tests are adequate
- [ ] Documentation is updated
- [ ] No unnecessary complexity
- [ ] Readable and maintainable

#### As a PR Author

**Before Creating PR:**

```bash
# Self-review checklist
1. Run tests locally
2. Check for console errors/warnings
3. Review your own diff
4. Update documentation
5. Write clear PR description
6. Link related issues
7. Add screenshots if UI changes
8. Ensure CI passes
```

**Responding to Reviews:**

```markdown
# Acknowledge feedback
"Good catch! Fixed in commit abc123"

# Explain decisions
"I chose this approach because..."

# Ask for clarification
"Could you elaborate on what you mean by...?"

# Thank reviewers
"Thanks for the thorough review!"
```

### PR Management

```bash
# List PRs
gh pr list
gh pr list --state open
gh pr list --author username

# View PR
gh pr view 123
gh pr view --web

# Check out PR locally
gh pr checkout 123
git fetch origin pull/123/head:pr-123
git checkout pr-123

# Review PR
gh pr review 123 --approve
gh pr review 123 --request-changes
gh pr review 123 --comment

# Merge PR
gh pr merge 123
gh pr merge 123 --squash
gh pr merge 123 --rebase
gh pr merge 123 --merge

# Close PR
gh pr close 123

# Reopen PR
gh pr reopen 123
```

---

## 6. GitHub Actions & CI/CD

### Understanding GitHub Actions

**Workflow** → **Jobs** → **Steps** → **Actions**

### Basic Workflow Example

Create `.github/workflows/ci.yml`:

```yaml
name: CI

# Trigger conditions
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:  # Manual trigger

# Environment variables
env:
  NODE_VERSION: 18

# Jobs
jobs:
  test:
    name: Run Tests
    runs-on: ubuntu-latest
    
    steps:
      # Checkout code
      - name: Checkout repository
        uses: actions/checkout@v3
      
      # Setup Node.js
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      
      # Install dependencies
      - name: Install dependencies
        run: npm ci
      
      # Run tests
      - name: Run tests
        run: npm test
      
      # Upload coverage
      - name: Upload coverage
        uses: codecov/codecov-action@v3
        if: success()

  lint:
    name: Code Quality
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Check formatting
        run: npm run format:check

  build:
    name: Build Application
    needs: [test, lint]  # Run after test and lint
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
      
      - name: Install dependencies
        run: npm ci
      
      - name: Build
        run: npm run build
      
      - name: Upload artifact
        uses: actions/upload-artifact@v3
        with:
          name: build
          path: dist/
```

### Common Workflow Patterns

#### 1. **Multi-Platform Testing**

```yaml
name: Cross-Platform Tests

on: [push, pull_request]

jobs:
  test:
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        node: [16, 18, 20]
    
    runs-on: ${{ matrix.os }}
    
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js ${{ matrix.node }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node }}
      - run: npm ci
      - run: npm test
```

#### 2. **Docker Build & Push**

```yaml
name: Docker Build

on:
  push:
    branches: [ main ]
    tags: [ 'v*' ]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Docker meta
        id: meta
        uses: docker/metadata-action@v4
        with:
          images: username/myapp
          tags: |
            type=ref,event=branch
            type=semver,pattern={{version}}
      
      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      
      - name: Build and push
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
```

#### 3. **Automated Release**

```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Build project
        run: |
          npm ci
          npm run build
      
      - name: Create Release
        uses: softprops/action-gh-release@v1
        with:
          files: |
            dist/*.zip
            dist/*.tar.gz
          generate_release_notes: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

#### 4. **Deploy to GitHub Pages**

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
      
      - name: Build
        run: |
          npm ci
          npm run build
      
      - name: Setup Pages
        uses: actions/configure-pages@v3
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: './dist'
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

### Secrets Management

```bash
# Via GitHub CLI
gh secret set SECRET_NAME

# Via web interface
Settings → Secrets and variables → Actions → New repository secret
```

**Using secrets in workflow:**

```yaml
- name: Deploy
  env:
    API_KEY: ${{ secrets.API_KEY }}
    DATABASE_URL: ${{ secrets.DATABASE_URL }}
  run: npm run deploy
```

### Workflow Debugging

```yaml
# Enable debug logging
- name: Debug
  run: |
    echo "Event: ${{ github.event_name }}"
    echo "Ref: ${{ github.ref }}"
    echo "Actor: ${{ github.actor }}"
    echo "SHA: ${{ github.sha }}"

# Use tmate for interactive debugging
- name: Setup tmate session
  if: failure()
  uses: mxschmitt/action-tmate@v3
```

---

## 7. Collaboration Workflows

### Forking Workflow

Used for open-source contributions.

```bash
# 1. Fork repository on GitHub (via web or CLI)
gh repo fork original-owner/repo

# 2. Clone your fork
git clone https://github.com/your-username/repo.git
cd repo

# 3. Add upstream remote
git remote add upstream https://github.com/original-owner/repo.git

# 4. Create feature branch
git checkout -b feature/my-contribution

# 5. Make changes and commit
git add .
git commit -m "feat: add new feature"

# 6. Push to your fork
git push origin feature/my-contribution

# 7. Create pull request (fork → original)
gh pr create --repo original-owner/repo

# 8. Keep your fork synced
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Feature Branch Workflow

Used within teams.

```bash
# 1. Update main
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/new-feature

# 3. Work on feature
# ... make changes ...
git add .
git commit -m "feat: implement new feature"

# 4. Keep branch updated with main
git checkout main
git pull origin main
git checkout feature/new-feature
git rebase main  # or git merge main

# 5. Push feature branch
git push -u origin feature/new-feature

# 6. Create pull request
gh pr create

# 7. After PR is merged, cleanup
git checkout main
git pull origin main
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

### Resolving Merge Conflicts

```bash
# Conflict occurs during merge/rebase
git merge feature-branch
# CONFLICT (content): Merge conflict in file.txt

# View conflicted files
git status

# Open file and resolve conflicts
# Look for conflict markers:
<<<<<<< HEAD
Current branch content
=======
Incoming branch content
>>>>>>> feature-branch

# After resolving, stage files
git add file.txt

# Complete merge
git commit -m "merge: resolve conflicts with feature-branch"

# Or abort merge
git merge --abort

# For rebase conflicts
git add file.txt
git rebase --continue
# Or abort
git rebase --abort
```

### Pair Programming with GitHub

```bash
# Method 1: Co-authoring commits
git commit -m "feat: add feature

Co-authored-by: Partner Name <partner@email.com>"

# Method 2: VS Code Live Share
# Install Live Share extension
# Share session link with partner

# Method 3: GitHub Codespaces
gh codespace create
gh codespace code  # Opens in VS Code
```

---

## 8. Advanced Git Techniques

### Interactive Rebase

Rewrite commit history (use before pushing!).

```bash
# Rebase last 3 commits
git rebase -i HEAD~3

# Interactive rebase menu:
# pick   = keep commit
# reword = keep commit, edit message
# edit   = keep commit, pause to amend
# squash = combine with previous commit
# fixup  = like squash, discard message
# drop   = remove commit

# Example: Squash commits
pick abc123 feat: add login
squash def456 fix: typo in login
squash ghi789 refactor: clean up login

# Result: 1 commit with all changes
```

### Git Stash

Temporarily save changes without committing.

```bash
# Stash changes
git stash
git stash save "WIP: working on feature"

# List stashes
git stash list

# Apply stash
git stash apply           # Keep stash
git stash pop            # Apply and remove
git stash apply stash@{2}  # Apply specific stash

# View stash content
git stash show
git stash show -p  # Show diff

# Drop stash
git stash drop
git stash drop stash@{1}

# Clear all stashes
git stash clear

# Create branch from stash
git stash branch new-branch stash@{0}
```

### Git Worktrees

Work on multiple branches simultaneously.

```bash
# Add worktree
git worktree add ../project-feature feature-branch
cd ../project-feature
# Work on feature branch

# List worktrees
git worktree list

# Remove worktree
git worktree remove ../project-feature

# Prune deleted worktrees
git worktree prune
```

### Git Submodules

Include external repositories.

```bash
# Add submodule
git submodule add https://github.com/user/lib.git lib/

# Clone repo with submodules
git clone --recurse-submodules https://github.com/user/repo.git

# Initialize submodules (if not cloned with --recurse-submodules)
git submodule init
git submodule update

# Update all submodules
git submodule update --remote

# Remove submodule
git submodule deinit lib/
git rm lib/
rm -rf .git/modules/lib/
```

### Git Hooks

Automate tasks on git events.

Located in `.git/hooks/` or use tools like Husky.

```bash
# Example: pre-commit hook
# File: .git/hooks/pre-commit
#!/bin/sh
npm test
npm run lint

# Make executable
chmod +x .git/hooks/pre-commit

# Using Husky (recommended)
npm install --save-dev husky
npx husky init

# Add hook
npx husky add .husky/pre-commit "npm test"
```

Common hooks:
- `pre-commit`: Before commit
- `commit-msg`: Validate commit message
- `pre-push`: Before push
- `post-merge`: After merge

### Git Bisect

Find bug-introducing commit.

```bash
# Start bisect
git bisect start

# Mark current as bad
git bisect bad

# Mark known good commit
git bisect good v1.0.0

# Git checks out middle commit
# Test if bug exists
git bisect bad  # or git bisect good

# Repeat until bug is found
# Git will identify exact commit

# End bisect
git bisect reset
```

### Git Reflog

Recover "lost" commits.

```bash
# View reflog
git reflog

# Output:
abc123 HEAD@{0}: commit: latest commit
def456 HEAD@{1}: commit: previous commit
ghi789 HEAD@{2}: reset: moving to HEAD~1

# Recover lost commit
git checkout ghi789
git cherry-pick ghi789
# or
git reset --hard ghi789
```

### Git Blame

Find who changed each line.

```bash
# Show who modified each line
git blame filename.txt

# Blame specific lines
git blame -L 10,20 filename.txt

# Blame with email
git blame -e filename.txt

# Ignore whitespace changes
git blame -w filename.txt

# Better blame (VS Code extension)
# GitLens shows inline blame
```

---

## 9. Security & Best Practices

### Protecting Sensitive Data

#### 1. Never Commit Secrets

```bash
# Add to .gitignore BEFORE committing
echo ".env" >> .gitignore
echo "secrets.yml" >> .gitignore
echo "*.pem" >> .gitignore

# Use environment variables
# .env file:
API_KEY=your-secret-key
DATABASE_URL=postgres://...

# Load in application
const apiKey = process.env.API_KEY;
```

#### 2. Remove Committed Secrets

```bash
# If secret was committed:

# Option 1: BFG Repo-Cleaner (faster)
brew install bfg  # or download
bfg --delete-files secrets.yml
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# Option 2: git filter-branch
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch secrets.yml' \
  --prune-empty --tag-name-filter cat -- --all

# Force push (warning: rewrites history!)
git push origin --force --all
git push origin --force --tags

# Change the exposed secret immediately!
```

#### 3. Git Secrets Tool

```bash
# Install git-secrets
brew install git-secrets

# Setup hooks
git secrets --install
git secrets --register-aws  # For AWS keys

# Scan repository
git secrets --scan

# Scan history
git secrets --scan-history
```

### Branch Protection Rules

On GitHub: Settings → Branches → Add rule

**Recommended settings:**

```
✓ Require pull request reviews before merging
  ✓ Require approvals: 1-2
  ✓ Dismiss stale reviews
  ✓ Require review from Code Owners

✓ Require status checks to pass before merging
  ✓ Require branches to be up to date
  ✓ Status checks: CI, tests, linting

✓ Require conversation resolution before merging

✓ Require signed commits

✓ Include administrators

✗ Allow force pushes

✗ Allow deletions
```

### Code Owners

Create `.github/CODEOWNERS`:

```
# Global owners
* @team-leads

# Specific directories
/docs/ @doc-team
/src/ @dev-team
/tests/ @qa-team

# Specific files
*.js @javascript-team
*.py @python-team
package.json @tech-lead

# Multiple owners
/critical/* @security-team @tech-lead
```

### Signed Commits

```bash
# Setup GPG (already covered in section 4)
git config --global commit.gpgsign true

# Verify on GitHub
Settings → SSH and GPG keys → New GPG key
# Paste your public key

# Commits will show "Verified" badge
```

### Dependency Security

```bash
# GitHub Dependabot
# Automatically creates PRs for dependency updates
# Enable: Settings → Security & analysis → Dependabot

# npm audit
npm audit
npm audit fix
npm audit fix --force

# GitHub Security Advisories
# View: Security tab → Advisories

# CodeQL scanning
# Enable: Security tab → Code scanning
```

### Repository Security Checklist

- [ ] `.gitignore` configured properly
- [ ] No secrets in code
- [ ] Branch protection enabled
- [ ] Required reviews configured
- [ ] CI/CD tests pass before merge
- [ ] Dependabot enabled
- [ ] Security scanning enabled
- [ ] CODEOWNERS file present
- [ ] Signed commits enforced
- [ ] Two-factor authentication enabled

---

## 10. GitHub Features

### Issues

```bash
# Create issue
gh issue create --title "Bug: Login fails" \
                --body "Description..."

# List issues
gh issue list
gh issue list --state open
gh issue list --label bug
gh issue list --assignee @me

# View issue
gh issue view 123

# Close issue
gh issue close 123

# Reopen issue
gh issue reopen 123

# Comment on issue
gh issue comment 123 --body "Fixed in PR #456"
```

**Issue Template** (`.github/ISSUE_TEMPLATE/bug_report.md`):

```markdown
---
name: Bug Report
about: Create a report to help us improve
title: '[BUG] '
labels: bug
assignees: ''
---

## Bug Description
A clear and concise description of what the bug is.

## Steps To Reproduce
1. Go to '...'
2. Click on '....'
3. See error

## Expected Behavior
What you expected to happen.

## Screenshots
If applicable, add screenshots.

## Environment
- OS: [e.g. Windows 10]
- Browser: [e.g. Chrome 96]
- Version: [e.g. 1.2.3]

## Additional Context
Any other context about the problem.
```

### Projects

GitHub Projects = Kanban boards

```bash
# Via CLI (beta)
gh project create --owner @me --title "My Project"
gh project list --owner @me
gh project item-add PROJECT_NUMBER --owner @me --url ISSUE_URL

# Via Web
Projects tab → New project → Board/Table/Roadmap
```

**Project Automation:**
- Auto-add new issues
- Auto-move to "Done" when PR merged
- Auto-close when issue resolved

### Discussions

Enable: Settings → General → Features → Discussions

```bash
# Create discussion
gh api repos/:owner/:repo/discussions \
  -f title="RFC: New Feature" \
  -f body="Proposal..."

# Categories:
- Announcements
- Q&A
- Ideas
- Show and tell
- General
```

### GitHub Pages

```bash
# Deploy via GitHub Actions (see section 6)

# Or configure in Settings → Pages
- Source: Deploy from a branch
- Branch: gh-pages / main
- Folder: / (root) or /docs

# Custom domain
- Add CNAME file with domain
- Configure DNS records

# Your site will be at:
https://username.github.io/repository/
```

### GitHub Packages

```yaml
# .github/workflows/publish.yml
name: Publish Package

on:
  release:
    types: [created]

jobs:
  publish:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    
    steps:
      - uses: actions/checkout@v3
      
      - uses: actions/setup-node@v3
        with:
          node-version: 18
          registry-url: 'https://npm.pkg.github.com'
      
      - run: npm ci
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### GitHub CLI Power Features

```bash
# Aliases
gh alias set co 'pr checkout'
gh alias set pv 'pr view --web'

# Browse repository
gh browse

# Clone all repos from org
gh repo list orgname --limit 1000 | \
  awk '{print $1}' | \
  xargs -n1 gh repo clone

# Create gist
gh gist create file.txt --public

# Run workflow
gh workflow run ci.yml

# View workflow runs
gh run list
gh run watch

# SSH to codespace
gh codespace ssh
```

---

## 11. Troubleshooting

### Common Issues

#### 1. **Merge Conflicts**

```bash
# View conflicted files
git status

# Resolve and stage
git add resolved-file.txt

# Continue merge/rebase
git commit  # for merge
git rebase --continue  # for rebase

# Or abort
git merge --abort
git rebase --abort
```

#### 2. **Accidentally Committed to Wrong Branch**

```bash
# Move last commit to new branch
git branch new-branch
git reset HEAD~ --hard
git checkout new-branch

# Or cherry-pick to correct branch
git checkout correct-branch
git cherry-pick wrong-branch
git checkout wrong-branch
git reset HEAD~ --hard
```

#### 3. **Need to Undo Last Commit**

```bash
# Keep changes (unstaged)
git reset HEAD~

# Keep changes (staged)
git reset --soft HEAD~

# Discard changes
git reset --hard HEAD~

# Already pushed? Create revert commit
git revert HEAD
git push
```

#### 4. **Pushed to Wrong Remote**

```bash
# View remotes
git remote -v

# Change remote URL
git remote set-url origin correct-url

# Force push to correct remote
git push origin main --force
```

#### 5. **Large Files Causing Issues**

```bash
# Remove large file from history
git filter-branch --tree-filter 'rm -f large-file.zip' HEAD

# Or use BFG
bfg --strip-blobs-bigger-than 100M

# Consider Git LFS for large files
git lfs install
git lfs track "*.zip"
git add .gitattributes
```

#### 6. **Authentication Issues**

```bash
# For HTTPS (use personal access token, not password)
# Generate token: Settings → Developer settings → Personal access tokens

# For SSH (recommended)
ssh-keygen -t ed25519 -C "your_email@example.com"
cat ~/.ssh/id_ed25519.pub  # Add to GitHub

# Test SSH
ssh -T git@github.com

# Switch HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git
```

### Git Commands for Recovery

```bash
# See all references
git reflog

# Recover deleted branch
git checkout -b recovered-branch commit-hash

# Recover deleted file
git checkout commit-hash -- deleted-file.txt

# Undo all local changes
git restore .
git reset --hard HEAD

# Clean untracked files
git clean -fd
git clean -fdx  # including ignored files
```

### Performance Issues

```bash
# Repository too large? Clone shallow
git clone --depth 1 https://github.com/user/repo.git

# Optimize repository
git gc --aggressive --prune=now

# Reduce repository size
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# Check repository size
du -sh .git
```

---

## 12. Pro Tips & Tricks

### Git Aliases

Add to `~/.gitconfig`:

```ini
[alias]
    # Status
    st = status
    s = status -s
    
    # Commit
    c = commit
    cm = commit -m
    ca = commit --amend
    
    # Checkout/Branch
    co = checkout
    br = branch
    
    # Log
    l = log --oneline
    lg = log --oneline --graph --all --decorate
    ll = log --pretty=format:'%C(yellow)%h%Creset %C(cyan)%ad%Creset | %s %C(green)%d%Creset %C(bold blue)[%an]%Creset' --date=short
    
    # Diff
    d = diff
    ds = diff --staged
    
    # Stash
    ss = stash save
    sl = stash list
    sp = stash pop
    
    # Remote
    pu = push
    pl = pull
    f = fetch
    
    # Undo
    undo = reset HEAD~1
    unstage = reset HEAD --
    
    # Others
    last = log -1 HEAD
    visual = log --oneline --graph --all --decorate --color
    aliases = config --get-regexp alias
```

### Keyboard Shortcuts (GitHub Web)

```
? - Show all shortcuts

Repository:
t - File finder
w - Switch branches
y - Permalink to file
. - Open in github.dev

Issues/PRs:
c - Create issue/PR
/ - Focus search
e - Edit
o - Open

Code Review:
c - Comment
@ - Mention user
> - Quote
r - Reply
```

### Useful Git Configuration

```bash
# Better diff algorithm
git config --global diff.algorithm histogram

# Reuse recorded conflict resolution
git config --global rerere.enabled true

# Push current branch by default
git config --global push.default current

# Prune on fetch
git config --global fetch.prune true

# Colorful output
git config --global color.ui auto

# Default branch name
git config --global init.defaultBranch main

# Pull strategy
git config --global pull.rebase false  # merge (default)
git config --global pull.rebase true   # rebase
git config --global pull.ff only       # fast-forward only
```

### Power User Workflows

#### 1. **Squash Commits on Merge**

```bash
# Local squash before PR
git rebase -i HEAD~5  # Last 5 commits
# Mark commits as 'squash' or 'fixup'

# Or merge with --squash
git merge --squash feature-branch
git commit -m "feat: complete feature"

# Or use GitHub's "Squash and merge" button
```

#### 2. **Cherry-pick Range**

```bash
# Cherry-pick multiple commits
git cherry-pick commit1^..commit5
```

#### 3. **Patch Workflow**

```bash
# Create patch
git format-patch HEAD~3  # Last 3 commits

# Apply patch
git am 0001-commit-message.patch
```

#### 4. **Bisect with Script**

```bash
# Automated bisect
git bisect start bad-commit good-commit
git bisect run ./test-script.sh
```

### GitHub Search Operators

```
# In repository
repo:username/repo language:javascript

# By user/org
user:username
org:orgname

# File content
filename:.gitignore

# Issues/PRs
is:issue is:open label:bug
is:pr is:closed author:username

# Code search
extension:js "function login"
path:src/ "TODO"

# Commits
author:username
committer:username
author-date:2024-01-01..2024-12-31

# Combine
repo:username/repo is:issue is:open label:bug,help-wanted
```

### Productivity Tools

**CLI Tools:**
- `gh` - GitHub CLI
- `hub` - GitHub wrapper for git
- `lazygit` - Terminal UI for git
- `tig` - Text-mode interface for git
- `gita` - Manage multiple repositories

**VS Code Extensions:**
- GitLens
- GitHub Pull Requests
- Git Graph
- Git History
- GitHub Copilot

**Desktop Apps:**
- GitHub Desktop
- GitKraken
- Sourcetree
- Tower

---

## Summary: Essential Commands Cheat Sheet

```bash
# Setup
git config --global user.name "Name"
git config --global user.email "email"

# Start
git init
git clone url

# Daily work
git status
git add .
git commit -m "message"
git push
git pull

# Branching
git branch
git branch name
git checkout name
git checkout -b name
git merge name

# Collaboration
git fetch
git rebase main
git cherry-pick hash

# Undo
git reset HEAD~
git revert hash
git restore file

# Advanced
git stash
git reflog
git bisect
git rebase -i

# GitHub
gh repo create
gh pr create
gh pr merge
gh issue create
```

---

## Next Steps

1. **Practice** - Create test repositories
2. **Read** - Pro Git book (free: https://git-scm.com/book)
3. **Explore** - GitHub's official guides
4. **Contribute** - Make open-source contributions
5. **Automate** - Setup CI/CD for your projects
6. **Collaborate** - Work on team projects

---

**Remember:** The best way to learn Git and GitHub is by using them daily. Make mistakes in test repositories, experiment, and gradually adopt advanced features as you become comfortable with the basics.

Happy coding! 🚀
