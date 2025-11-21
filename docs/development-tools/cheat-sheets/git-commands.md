# Git Commands Cheat Sheet

Quick reference for essential git commands organized by workflow.

## Daily Commands

### Check Status
```bash
# See what's changed
git status

# Short format
git status -s

# Show branch and tracking info
git status -sb
```

### Stage Changes
```bash
# Stage all changes
git add .

# Stage specific file
git add path/to/file.js

# Stage specific files by pattern
git add "*.js"

# Stage interactively (choose what to stage)
git add -p

# Stage modified and deleted files (not new files)
git add -u
```

### Commit Changes
```bash
# Commit with message
git commit -m "Add feature X"

# Commit with multi-line message
git commit -m "Add feature X" -m "Detailed description here"

# Commit with message using heredoc (better formatting)
git commit -m "$(cat <<'EOF'
Add user authentication feature

- Implement login/logout
- Add password hashing
- Create session management
EOF
)"

# Commit all modified files (skip staging)
git add . && git commit -m "message"

# Amend last commit (change message or add files)
git commit --amend -m "New message"

# Amend without changing message
git commit --amend --no-edit
```

### Push to Remote
```bash
# Push current branch
git push

# Push and set upstream
git push -u origin branch-name

# Force push (dangerous! use with caution)
git push --force-with-lease

# Push all branches
git push --all

# Push tags
git push --tags
```

### Pull from Remote
```bash
# Pull current branch
git pull

# Pull specific branch
git pull origin main

# Pull with rebase instead of merge
git pull --rebase

# Pull all branches
git fetch --all
```

### View Changes
```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# See changes in specific file
git diff path/to/file.js

# See changes between branches
git diff main..feature-branch

# See changes between commits
git diff abc123..def456

# Word-level diff (better for prose)
git diff --word-diff
```

### View History
```bash
# See commit history
git log

# One line per commit
git log --oneline

# Last 5 commits
git log -5

# Commits by author
git log --author="John"

# Commits since date
git log --since="2 weeks ago"

# Commits with file changes
git log --stat

# Pretty format
git log --oneline --graph --decorate --all

# Search commit messages
git log --grep="bug fix"

# Show commits that modified a file
git log --follow path/to/file.js
```

## Branching

### Create Branch
```bash
# Create new branch
git branch feature-name

# Create and switch to new branch
git checkout -b feature-name

# Modern: create and switch
git switch -c feature-name

# Create branch from specific commit
git branch feature-name abc123

# Create branch from remote branch
git checkout -b feature-name origin/feature-name
```

### Switch Branch
```bash
# Switch to existing branch
git checkout branch-name

# Modern: switch branch
git switch branch-name

# Switch to previous branch
git checkout -

# Switch and create if doesn't exist
git checkout -b branch-name
```

### List Branches
```bash
# List local branches
git branch

# List all branches (local + remote)
git branch -a

# List remote branches only
git branch -r

# List with last commit message
git branch -v

# List merged branches
git branch --merged

# List unmerged branches
git branch --no-merged
```

### Delete Branch
```bash
# Delete local branch (safe, prevents if unmerged)
git branch -d feature-name

# Force delete local branch
git branch -D feature-name

# Delete remote branch
git push origin --delete feature-name

# Delete multiple branches
git branch -d branch1 branch2 branch3
```

### Merge Branch
```bash
# Merge branch into current branch
git merge feature-name

# Merge without fast-forward (create merge commit)
git merge --no-ff feature-name

# Merge and squash all commits
git merge --squash feature-name

# Abort merge if conflicts
git merge --abort
```

## Undo and Recovery

### Unstage Files
```bash
# Unstage specific file
git restore --staged path/to/file.js

# Old syntax (still works)
git reset HEAD path/to/file.js

# Unstage all files
git restore --staged .
```

### Discard Changes
```bash
# Discard changes in specific file
git restore path/to/file.js

# Old syntax (still works)
git checkout -- path/to/file.js

# Discard all changes
git restore .

# Discard untracked files
git clean -fd

# Preview what will be deleted
git clean -n
```

### Undo Commits
```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset HEAD~1

# Undo last commit, discard changes (DANGEROUS!)
git reset --hard HEAD~1

# Undo last 3 commits
git reset --soft HEAD~3

# Undo to specific commit
git reset --soft abc123
```

### Revert Commits (Safe Undo)
```bash
# Create new commit that undoes last commit
git revert HEAD

# Revert specific commit
git revert abc123

# Revert range of commits
git revert abc123..def456

# Revert without committing (stage changes only)
git revert --no-commit HEAD
```

### Stash Changes
```bash
# Stash current changes
git stash

# Stash with message
git stash save "WIP: feature X"

# Stash including untracked files
git stash -u

# List stashes
git stash list

# Apply most recent stash
git stash apply

# Apply and remove stash
git stash pop

# Apply specific stash
git stash apply stash@{2}

# Drop stash
git stash drop stash@{0}

# Clear all stashes
git stash clear

# Show stash contents
git stash show -p stash@{0}
```

## Advanced Operations

### Cherry-Pick
```bash
# Apply commit from another branch
git cherry-pick abc123

# Cherry-pick multiple commits
git cherry-pick abc123 def456

# Cherry-pick range of commits
git cherry-pick abc123..def456

# Cherry-pick without committing
git cherry-pick --no-commit abc123
```

### Rebase
```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase (edit history)
git rebase -i HEAD~5

# Continue rebase after resolving conflicts
git rebase --continue

# Skip commit during rebase
git rebase --skip

# Abort rebase
git rebase --abort

# Rebase and preserve merge commits
git rebase --preserve-merges main
```

**Interactive rebase options:**
```
pick abc123  # Use commit
reword abc123  # Use commit, edit message
edit abc123  # Use commit, stop to amend
squash abc123  # Merge into previous commit
fixup abc123  # Merge, discard message
drop abc123  # Remove commit
```

### Bisect (Find Bug-Introducing Commit)
```bash
# Start bisect
git bisect start

# Mark current commit as bad
git bisect bad

# Mark last known good commit
git bisect good abc123

# Git will checkout middle commit, test it, then:
git bisect good  # If works
git bisect bad   # If broken

# Repeat until bug found

# End bisect
git bisect reset

# Automate bisect with script
git bisect run npm test
```

### Reflog (Recovery)
```bash
# View all HEAD movements
git reflog

# View reflog for specific branch
git reflog show branch-name

# Recover "lost" commit
git checkout abc123

# Recover "lost" branch
git branch recovered-branch abc123

# Clean old reflog entries
git reflog expire --expire=90.days.ago --all
```

## Remote Repositories

### Add/Remove Remotes
```bash
# Add remote
git remote add origin https://github.com/user/repo.git

# View remotes
git remote -v

# Remove remote
git remote remove origin

# Rename remote
git remote rename origin upstream

# Change remote URL
git remote set-url origin https://new-url.git
```

### Fetch
```bash
# Fetch from origin
git fetch origin

# Fetch all remotes
git fetch --all

# Fetch and prune deleted branches
git fetch --prune

# Fetch specific branch
git fetch origin main
```

### Track Remote Branch
```bash
# Set upstream for current branch
git branch --set-upstream-to=origin/main

# Short form
git branch -u origin/main

# Push and set upstream
git push -u origin branch-name
```

## Tags

### Create Tags
```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag (recommended)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Tag specific commit
git tag -a v1.0.0 abc123 -m "Release 1.0.0"
```

### List and View Tags
```bash
# List all tags
git tag

# List tags matching pattern
git tag -l "v1.*"

# Show tag details
git show v1.0.0
```

### Push Tags
```bash
# Push specific tag
git push origin v1.0.0

# Push all tags
git push --tags

# Push commits and tags
git push --follow-tags
```

### Delete Tags
```bash
# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0
```

## Configuration

### Set User Info
```bash
# Set name globally
git config --global user.name "John Smith"

# Set email globally
git config --global user.email "john@example.com"

# Set for current repo only (no --global)
git config user.name "John Smith"
git config user.email "john@example.com"
```

### Set Editor
```bash
# Set default editor
git config --global core.editor "code --wait"

# VS Code
git config --global core.editor "code --wait"

# Nano
git config --global core.editor "nano"

# Vim
git config --global core.editor "vim"
```

### Aliases
```bash
# Create shortcut commands
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --decorate --all'

# Now use as:
git st  # Instead of git status
git co main  # Instead of git checkout main
```

### View Configuration
```bash
# List all config
git config --list

# List global config
git config --global --list

# List local config (current repo)
git config --local --list

# Get specific config value
git config user.name
```

## Troubleshooting

### Fix Mistakes

#### Committed to wrong branch
```bash
# On wrong branch:
git reset --soft HEAD~1  # Undo commit, keep changes
git stash

# Switch to correct branch:
git checkout correct-branch
git stash pop
git add .
git commit -m "message"
```

#### Accidentally committed secrets
```bash
# Remove from last commit
git rm --cached path/to/secret-file
git commit --amend --no-edit

# Remove from history (use BFG or git-filter-repo)
# https://rtyley.github.io/bfg-repo-cleaner/
```

#### Need to undo pushed commit
```bash
# Create reverting commit (safe)
git revert abc123
git push

# Force push (DANGEROUS, only if no one else pulled)
git reset --hard HEAD~1
git push --force-with-lease
```

#### Merge conflicts
```bash
# During merge:
git status  # See conflicted files

# Edit files, remove conflict markers:
# <<<<<<< HEAD
# your changes
# =======
# their changes
# >>>>>>> branch-name

# After resolving:
git add resolved-file.js
git commit  # Complete merge

# Or abort merge:
git merge --abort
```

#### Detached HEAD state
```bash
# You're in detached HEAD (not on a branch)
# To create branch from current state:
git checkout -b new-branch-name

# To return to a branch:
git checkout main
```

### Common Errors

#### "fatal: not a git repository"
```bash
# Initialize git in current directory
git init
```

#### "error: failed to push some refs"
```bash
# Someone else pushed first, pull first
git pull --rebase
git push
```

#### "fatal: refusing to merge unrelated histories"
```bash
# Force merge unrelated repositories
git pull origin main --allow-unrelated-histories
```

#### "Updates were rejected"
```bash
# Pull first, then push
git pull
# Resolve any conflicts
git push
```

## Git Workflows

### Feature Branch Workflow
```bash
# 1. Create feature branch
git checkout -b feature/add-user-auth

# 2. Make changes and commit
git add .
git commit -m "Implement user authentication"

# 3. Push to remote
git push -u origin feature/add-user-auth

# 4. Create pull request (via GitHub/GitLab UI)

# 5. After PR approved, merge via UI or:
git checkout main
git pull
git merge --no-ff feature/add-user-auth
git push

# 6. Delete branch
git branch -d feature/add-user-auth
git push origin --delete feature/add-user-auth
```

### Hotfix Workflow
```bash
# 1. Create hotfix branch from main
git checkout main
git checkout -b hotfix/critical-bug

# 2. Fix and commit
git add .
git commit -m "Fix critical authentication bug"

# 3. Merge to main
git checkout main
git merge --no-ff hotfix/critical-bug
git push

# 4. Merge to develop (if you have one)
git checkout develop
git merge --no-ff hotfix/critical-bug
git push

# 5. Delete hotfix branch
git branch -d hotfix/critical-bug
```

### Sync Fork Workflow
```bash
# 1. Add upstream remote (once)
git remote add upstream https://github.com/original/repo.git

# 2. Fetch upstream
git fetch upstream

# 3. Merge upstream changes
git checkout main
git merge upstream/main

# 4. Push to your fork
git push origin main
```

## Useful Git Aliases

Add these to your global config:

```bash
# Shortcuts
git config --global alias.st 'status -sb'
git config --global alias.co 'checkout'
git config --global alias.br 'branch'
git config --global alias.cm 'commit -m'
git config --global alias.ca 'commit --amend'
git config --global alias.unstage 'restore --staged'

# Logs
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.last 'log -1 HEAD --stat'
git config --global alias.ls 'log --pretty=format:"%C(yellow)%h %C(blue)%ad%C(red)%d %C(reset)%s%C(green) [%cn]" --decorate --date=short'

# Diffs
git config --global alias.df 'diff --color --word-diff'
git config --global alias.ds 'diff --staged'

# Operations
git config --global alias.undo 'reset --soft HEAD~1'
git config --global alias.amend 'commit --amend --no-edit'
git config --global alias.save 'stash save'
git config --global alias.pop 'stash pop'
git config --global alias.branches 'branch -a'
git config --global alias.tags 'tag -l'
git config --global alias.remotes 'remote -v'
```

## Git Best Practices

### Commit Messages
```bash
# Good commit message structure:
# <type>: <subject> (max 50 chars)
#
# <body> (wrap at 72 chars)
#
# <footer>

# Types:
# feat: New feature
# fix: Bug fix
# docs: Documentation
# style: Formatting
# refactor: Code restructuring
# test: Adding tests
# chore: Maintenance

# Examples:
git commit -m "feat: add user authentication"
git commit -m "fix: resolve memory leak in image processing"
git commit -m "docs: update API documentation"
```

### Branch Naming
```bash
# Good patterns:
feature/add-user-auth
fix/memory-leak
hotfix/critical-bug
release/v1.2.0
docs/update-readme

# Bad patterns:
johns-branch
test
fix
new-feature
```

### Before Committing
```bash
# Always check what you're committing
git status
git diff
git diff --staged

# Run tests
npm test

# Lint code
npm run lint
```

### Keep History Clean
```bash
# Squash work-in-progress commits before merging
git rebase -i HEAD~5

# Use meaningful commit messages
# Commit logical units of work
# Don't commit commented-out code
# Don't commit secrets/credentials
```

---

**Quick Tips:**
- Commit often, push regularly
- Write descriptive commit messages
- Keep commits focused (one logical change per commit)
- Don't commit generated files (add to .gitignore)
- Always pull before pushing
- Use branches for features
- Test before committing
