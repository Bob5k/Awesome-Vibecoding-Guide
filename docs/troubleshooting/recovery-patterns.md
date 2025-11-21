# Recovery Patterns

Quick recovery strategies for common AI-assisted development mishaps. When things go wrong, use these patterns to get back on track.

## "Last Known Good State" Recovery

### When to Use
- AI made unexpected changes
- Code broke after following AI suggestion
- Not sure what changed

### Strategy: Git Time Machine

**Step 1: Find last working commit**
```bash
# View recent commits
git log --oneline -10

# Or with details
git log -5 --stat

# See what changed in each commit
git show abc123
```

**Step 2: Create safety branch**
```bash
# Before reverting, save current state
git branch broken-state

# Now safe to experiment with recovery
```

**Step 3: Recovery options**

**Option A: Revert specific commit**
```bash
# Undo one bad commit (creates new commit)
git revert abc123

# Undo multiple commits
git revert abc123 def456

# Result: Original commits stay in history, new commit undoes them
```

**Option B: Reset to good state**
```bash
# Soft reset: Keep changes as uncommitted
git reset --soft abc123

# Review changes
git diff

# Selectively re-apply good changes
git add path/to/good-file.js
git commit -m "Re-apply good changes only"
```

**Option C: Hard reset (nuclear option)**
```bash
# Discard everything, back to commit abc123
git reset --hard abc123

# WARNING: This destroys uncommitted changes!
# Make sure you created safety branch first!
```

**Step 4: Cherry-pick good changes**
```bash
# If broken-state had some good changes:
git checkout broken-state
git log --oneline  # Find good commits

git checkout main
git cherry-pick good-commit-hash
```

### Example: AI Broke Authentication

```bash
# 1. Notice login broken after AI refactored auth code

# 2. Find last working version
git log --oneline --grep="auth"
# Shows: abc123 "Fix login bug" (2 days ago) ← last known good
#        def456 "Refactor authentication" (today) ← broke it

# 3. Create safety branch
git branch auth-broken

# 4. Reset to good state
git reset --hard abc123

# 5. Test - login works again! ✅

# 6. Gradually re-apply good parts of refactor
git checkout auth-broken -- src/utils/jwt.ts  # This file was good
# Test
# Repeat for other good changes

# 7. Document what went wrong
echo "Refactor broke middleware error handling" >> docs/learnings.md
```

## Bisecting to Find AI-Introduced Bugs

### When to Use
- Bug appeared recently but don't know which commit
- Multiple AI changes, one broke something
- Need to identify exact problematic commit

### Strategy: Git Bisect

**How it works:**
Git performs binary search through commits to find the first bad one.

**Step 1: Start bisect**
```bash
git bisect start

# Mark current state as bad
git bisect bad

# Mark last known good commit
git log --oneline -20  # Find good commit
git bisect good abc123

# Git checks out middle commit
```

**Step 2: Test each commit**
```bash
# At each commit Git checks out, test the bug:
npm test  # Or manually test

# If bug exists:
git bisect bad

# If bug doesn't exist:
git bisect good

# Git checkouts next commit to test

# Repeat until Git finds first bad commit
```

**Step 3: Found it!**
```bash
# Git shows: "abc123 is the first bad commit"

# View the bad commit
git show abc123

# End bisect
git bisect reset
```

**Step 4: Fix the issue**
```bash
# Now you know exactly what broke
# Options:
# A) Revert the commit
git revert abc123

# B) Fix the specific issue
# Edit files, then:
git commit -m "Fix issue introduced in abc123"
```

### Automated Bisect

If you have automated tests:

```bash
git bisect start
git bisect bad HEAD
git bisect good abc123

# Let git run tests automatically
git bisect run npm test

# Git will find bad commit automatically!
```

### Example: Performance Regression

```bash
# Page load suddenly slow, but don't know why

# Start bisect
git bisect start
git bisect bad HEAD
git bisect good v1.2.0  # Last release was fast

# Git checks out commit in middle

# Test performance
time curl http://localhost:3000
# Takes 5 seconds (slow)
git bisect bad

# Next commit
time curl http://localhost:3000
# Takes 1 second (fast)
git bisect good

# Continue until...
# Git says: "def456 is first bad commit"

git show def456
# Commit message: "Add comprehensive logging"
# Aha! AI added console.log statements everywhere!

# Fix
git bisect reset
# Remove excessive logging, keep essential
git commit -m "Remove performance-killing debug logs"
```

## Emergency Rollback Procedures

### Production Site is Down

**Scenario:** Deployed AI-generated code, site is broken, losing revenue.

**Priority:** Get site working ASAP, debug later.

**Procedure:**

**Step 1: Rollback immediately (< 2 minutes)**
```bash
# Option A: Cloudflare Pages
# 1. Go to dashboard
# 2. Pages → Your site → Deployments
# 3. Find last working deployment
# 4. Click "..." → Rollback to this deployment
# Done! Site restored.

# Option B: Git-based deploy
git revert HEAD --no-edit
git push
# CI/CD will deploy previous version
```

**Step 2: Notify stakeholders (< 5 minutes)**
```
Status update:
"Site temporarily down, rolled back to previous version.
Site now operational. Investigating issue."
```

**Step 3: Debug safely (after site is stable)**
```bash
# Don't debug on main branch!
git checkout -b debug-production-issue

# Pull broken code
git reset --hard origin/main

# Investigate
# Fix issues
# Test thoroughly
# Create PR

# Never push untested fixes directly to production!
```

### Database Migration Failure

**Scenario:** AI-generated migration ran, broke database schema.

**Immediate actions:**

**Step 1: Stop the application**
```bash
# Prevent further damage
# Stop all instances accessing database
```

**Step 2: Check if reversible**
```bash
# If using migration tool with rollback:
npm run migrate:rollback

# Or manual rollback:
psql -U user -d database < backup.sql
```

**Step 3: Restore from backup**
```bash
# If no rollback available, restore from backup
# (This is why you always backup before migrations!)

# PostgreSQL example:
dropdb database_name
createdb database_name
pg_restore -d database_name backup.dump

# D1 example:
wrangler d1 execute DB --file=backup.sql --remote
```

**Step 4: Fix migration**
```bash
# Review what went wrong
cat migrations/xxxx_broken_migration.sql

# Create corrected migration
npm run migrate:create fix_schema

# Test on local database first!
npm run migrate:up --local

# Verify works
npm run test:db

# Then production
npm run migrate:up --remote
```

**Prevention:**
```markdown
# ALWAYS before production migration:

1. Backup database
2. Test migration on staging
3. Review AI-generated SQL carefully
4. Have rollback plan
5. Run during low-traffic time
6. Monitor for errors
7. Have restoration procedure ready
```

## Context Loss Recovery

### Mid-Project Context Loss

**Scenario:** AI "forgot" project context mid-session, suggestions now don't match your patterns.

**Recovery:**

**Step 1: Recognize context loss**
Signs:
- AI suggests different patterns than before
- AI "forgets" tech stack
- Suggestions contradict earlier advice
- AI asks about things it should know

**Step 2: Reset context explicitly**
```
STOP. Let's reset context.

I'm working on: [project name]
Tech stack: [Astro, D1, Cloudflare, etc.]
Current task: [what you're doing]

Project context:
[Paste relevant .cursorrules or summary]

Now, [continue your request]
```

**Step 3: Progressive context reload**
```
Don't load everything at once. Instead:

"Let's start fresh. Read .cursorrules first."

[AI reads .cursorrules]

"Now, I'm working on authentication. Read src/pages/api/auth/login.ts"

[AI reads file]

"Now help me add rate limiting."
```

**Step 4: Document the session**
```bash
# Save successful interaction pattern
echo "Today's context loss recovered by explicitly loading .cursorrules first" >> docs/ai-sessions.md
```

### Reconstructing from Git History

**Scenario:** Lost track of what you've been building, AI needs context about recent changes.

**Reconstruct context:**

```bash
# Step 1: See what you've been working on
git log --oneline --since="1 week ago"

# Step 2: See file changes
git diff --name-only HEAD~10 HEAD

# Step 3: Get summary of changes
git log --since="1 week ago" --pretty=format:"%h - %s" --graph

# Step 4: Provide to AI
```

```
Here's what I've been working on (from git history):

Recent commits:
[paste git log output]

Files changed:
[paste git diff --name-only output]

Now I need help with: [your request]
```

## AI Confusion Recovery

### AI Giving Contradictory Advice

**Scenario:** AI suggests A, then later suggests opposite of A.

**Recovery:**

**Step 1: Stop and clarify**
```
STOP. You just contradicted earlier advice.

Earlier you said: [quote contradictory advice]
Now you're saying: [quote current advice]

Which is correct for my use case?
[Describe use case clearly]

Please:
1. Explain which approach is right
2. Why the other doesn't apply
3. Commit to one approach moving forward
```

**Step 2: Document decision**
```markdown
# docs/decisions/authentication-approach.md

# Decision: Use JWT, not sessions

Date: 2025-01-15

## Context
AI initially suggested sessions, later suggested JWT.

## Clarification
For serverless (Cloudflare Pages), JWT is correct.
Sessions require persistent storage (K V), adds complexity.

## Decided
Using JWT in httpOnly cookies.

## Never Suggest Again
Don't reconsider sessions for this project.
Serverless architecture determined this.
```

**Step 3: Update .cursorrules**
```markdown
# Add to .cursorrules

## Established Decisions
- Authentication: JWT in httpOnly cookies (not sessions)
  - Reason: Serverless architecture
  - Do not suggest sessions
```

### AI Suggests Wrong Framework Features

**Scenario:** AI suggests React features in Astro, or vice versa.

**Recovery:**

**Immediate correction:**
```
STOP. Wrong framework.

This is Astro, not React.
Astro components use different syntax:
- Props via Astro.props
- No useState/useEffect
- Use client:* directives for interactivity

Please provide Astro component syntax.
```

**Prevent recurrence:**
```markdown
# Add to .cursorrules at top (high priority)

# FRAMEWORK: ASTRO
This is an ASTRO project.
- Use .astro files for components
- Use Astro.props for props
- No useState/useEffect in .astro files
- Use client:load/client:visible for React islands

DO NOT suggest React patterns for Astro components.
```

## Code Quality Recovery

### Large-Scale Refactor Gone Wrong

**Scenario:** AI refactored large section of code, now many tests fail.

**Recovery:**

**Step 1: Assess damage**
```bash
# Run tests
npm test

# How many failed?
# If > 50%, likely large refactor broke patterns

# See what changed
git diff
```

**Step 2: Rollback refactor**
```bash
# Save current state
git stash

# Back to before refactor
git log --oneline -5
git reset --hard abc123  # Before refactor
```

**Step 3: Incremental refactor**
```
Instead of big refactor, let's do incremental:

1. Refactor one file at a time
2. Run tests after each file
3. Commit each successful refactor
4. If tests fail, rollback that file only

Start with: src/utils/auth.ts
Refactor only this file.
```

**Step 4: Create refactor checklist**
```markdown
# Refactor Checklist

For each file:
- [ ] Refactor code
- [ ] Run tests: `npm test`
- [ ] Manual test in browser
- [ ] Review diff
- [ ] Commit if passing
- [ ] If fails, rollback and try different approach

Files to refactor:
- [ ] src/utils/auth.ts
- [ ] src/middleware/auth.ts
- [ ] src/pages/api/auth/login.ts
- [ ] src/pages/api/auth/logout.ts
```

### Salvaging Changes from Failed Branch

**Scenario:** Branch has mix of good and bad changes, don't want to lose good ones.

**Recovery:**

```bash
# Step 1: Identify good changes
git diff main..failed-branch --name-only
# Lists all changed files

# Step 2: Create new clean branch
git checkout main
git checkout -b salvage-good-changes

# Step 3: Cherry-pick good files
git checkout failed-branch -- src/components/GoodComponent.tsx
git add src/components/GoodComponent.tsx
git commit -m "Salvage: GoodComponent"

# Repeat for each good file

# Step 4: Verify
npm test
npm run build

# Step 5: Merge if all good
git checkout main
git merge salvage-good-changes
```

## Dependency Hell Recovery

### Breaking Dependency Update

**Scenario:** AI suggested updating packages, now app won't build/run.

**Recovery:**

**Step 1: Identify problem package**
```bash
# Check what updated
git diff package.json

# Example output shows:
- "astro": "^3.0.0"
+ "astro": "^4.0.0"
```

**Step 2: Check breaking changes**
```bash
# Read changelog
npm info astro

# Or visit
# https://github.com/withastro/astro/releases
```

**Step 3: Rollback package.json**
```bash
git checkout HEAD -- package.json package-lock.json
npm install
```

**Step 4: Update incrementally**
```bash
# Update one major version at a time
npm install astro@^3.5.0
npm test && npm run build

# If works:
npm install astro@^4.0.0
npm test && npm run build

# If breaks, check migration guide
```

**Step 5: Fix breaking changes**
```
AI: I updated to Astro 4, but build fails.

Error:
[paste error]

According to Astro 4 migration guide, what needs changing?

Astro 4 breaking changes:
[paste relevant breaking changes from docs]

Please update my code for Astro 4 compatibility.
```

### Version Lockfile Conflicts

**Scenario:** package-lock.json has conflicts after merge.

**Recovery:**

```bash
# Delete lockfile
rm package-lock.json

# Regenerate from package.json
npm install

# Verify everything works
npm test
npm run build

# Commit new lockfile
git add package-lock.json
git commit -m "Regenerate lockfile after merge"
```

## Prevention Strategies

### Checkpointing

**Create safety checkpoints:**

```bash
# Before major AI-assisted change:
git add .
git commit -m "checkpoint: before [description of change]"

# Make AI changes
# If works:
git add .
git commit -m "feat: [description]"

# If breaks:
git reset --hard HEAD~1  # Back to checkpoint
```

### Frequent Small Commits

**Best practice:**
```bash
# Commit after each working change
git add src/components/NewComponent.tsx
git commit -m "add: NewComponent"

# Not after 10 changes at once!
# Small commits = easy rollback
```

### Branch Protection

**For production:**

```bash
# Never push directly to main
git checkout -b feature/new-feature

# Work here, test thoroughly

# When ready:
git push origin feature/new-feature
# Create PR, review, then merge

# Never:
git checkout main
git push  # ← Don't do this!
```

### Backup Before Migrations

**Always before database changes:**

```bash
# PostgreSQL
pg_dump database_name > backup_$(date +%Y%m%d_%H%M%S).sql

# D1
wrangler d1 execute DB --command="SELECT * FROM table" --json > backup.json

# Then migrate
npm run migrate:up

# Keep backups for 30 days
```

## Summary: Recovery Principles

### 1. Safety First
Always create backup branch before experimenting.

### 2. Small Steps
Recover incrementally, not all at once.

### 3. Test Constantly
After each recovery step, verify it works.

### 4. Document Learnings
Note what went wrong, how you recovered.

### 5. Prevent Recurrence
Update .cursorrules, improve prompts to avoid repeat.

### 6. Git is Your Friend
Commit often, branches are cheap, history is valuable.

### 7. Don't Panic
Almost everything is recoverable with git.

---

**Golden Rule:** If you're not sure, create a branch first. Branches cost nothing, lost work costs everything.
