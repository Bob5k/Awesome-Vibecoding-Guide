# Git Strategies for Vibecoding

A practical, two-phase Git workflow optimized for AI-assisted development. This approach balances speed during initial development with stability during maintenance, proven effective across dozens of commercial projects.

## Overview: Two-Phase Git Workflow

**The Core Principle:**
Your Git strategy should match your project's lifecycle stage.

**Pre-Release (Development Phase):**
- Speed and iteration are critical
- Breaking things is acceptable
- Direct commits to master
- Minimal branching overhead

**Post-Release (Maintenance Phase):**
- Stability is critical
- Breaking production is unacceptable
- Mandatory feature branches
- Test before merging to master

**Why This Works:**
- Saves time during development (no unnecessary merge overhead)
- Provides robustness after release (protect production)
- Matches the actual risk profile of each phase
- Proven in real-world client projects

## Pre-Release Strategy (Development Phase)

### When to Use This Approach

**Project Status:**
- No live users yet
- No production environment
- Building from scratch
- MVP/initial development
- Heavy iteration phase

**Team Size:**
- Solo developer (most common)
- Small team (2-3 people)
- Clear communication channels

**Duration:**
- From project start
- Until first production deployment
- Typically 1-4 weeks

### The Strategy: Push Everything to Master

**Core Workflow:**
```bash
# Daily workflow
git add .
git commit -m "Implement user authentication"
git push origin main

# That's it!
```

**Why This Works:**

**1. Speed**
- No branching overhead
- No merge conflicts
- No context switching
- Iterate faster

**2. Simplicity**
- One branch to track
- Clear progression
- Easy to understand
- Less cognitive load

**3. Safety Net**
- Every commit is a checkpoint
- Easy rollback if needed
- Git history is your backup
- Remote repository protects against data loss

**4. AI-Friendly**
- AI can make commits directly
- No branching complexity
- Clear linear history
- Simple to explain to AI

### When to Use Feature Branches (Even Pre-Release)

**Larger Features Only:**
- Features requiring >3 days of work
- Experimental implementations
- Major architectural changes
- When you want to try multiple approaches

**Example:**
```bash
# Working on a complex authentication system
git checkout -b feat/auth-system

# 3 days of work, multiple commits
git add .
git commit -m "Add JWT token generation"
# ... more commits ...

# When ready to integrate
git checkout main
git merge feat/auth-system
git push origin main
```

**Don't Use Branches For:**
- Small features (<1 day)
- Bug fixes
- Content updates
- Quick iterations

### Commit Message Strategy

**Keep It Simple and Descriptive:**

**Good:**
```bash
git commit -m "Add user registration form with validation"
git commit -m "Fix authentication token expiration bug"
git commit -m "Update homepage hero section"
```

**Bad:**
```bash
git commit -m "stuff"
git commit -m "more changes"
git commit -m "fix"
```

**AI-Generated Commits:**
Let AI suggest commit messages based on changes:
```
Prompt: "Review the changes and suggest a commit message that
describes what was implemented."
```

### Benefits: Speed and Simplicity

**Time Saved:**
- No branch creation: +30 seconds per feature
- No branch switching: +20 seconds per context change
- No merge conflicts: +15 minutes per conflict
- **Total:** 1-2 hours saved per week on small projects

**Complexity Reduced:**
- One branch to remember
- No "which branch am I on?" confusion
- Straightforward git history
- Easier to explain to AI assistants

**Example Timeline:**
```
Traditional Branching (1 week project):
- Create 8 feature branches: 4 minutes
- Switch branches 20 times: 10 minutes
- Resolve 3 merge conflicts: 45 minutes
- PR reviews and merges: 60 minutes
Total overhead: ~2 hours

Direct to Master (1 week project):
- No branching overhead: 0 minutes
Total overhead: 0 minutes

Time saved: 2 hours (12% of a 16-hour project week)
```

### Recovery Strategies

**If Something Breaks:**

**Option 1: Revert Last Commit**
```bash
# See recent commits
git log --oneline

# Revert the bad commit
git revert abc1234

# Push the revert
git push origin main
```

**Option 2: Reset to Last Good State**
```bash
# Find last good commit
git log --oneline

# Reset to that commit (DESTRUCTIVE)
git reset --hard abc1234

# Force push (use with caution)
git push origin main --force
```

**Option 3: Quick Fix Forward**
```bash
# Just fix it and commit
git add .
git commit -m "Fix issue from previous commit"
git push origin main
```

**Best Practice:**
- Commit frequently (every 30-60 minutes)
- Each commit should be a working state
- Test before committing
- Smaller commits = easier recovery

## Post-Release Strategy (Maintenance Phase)

### When to Switch to This Approach

**Triggers:**
- ✅ First production deployment complete
- ✅ Real users accessing the site
- ✅ Client depends on site being live
- ✅ Downtime has real consequences

**Immediate Action:**
Lock master branch and establish branch-based workflow.

### The Strategy: Lock Master, Use Branches

**Protect Main Branch:**

**GitHub Settings:**
```
Settings → Branches → Branch Protection Rules
→ Add rule for "main"

Enable:
☑ Require pull request before merging
☑ Require status checks (if you have CI)
☐ Require approvals (for teams)
```

**Workflow:**
```bash
# 1. Create feature branch
git checkout -b feat/add-services-page

# 2. Develop and test locally
# ... work work work ...

# 3. Commit your changes
git add .
git commit -m "Add services page with contact form"

# 4. Push branch to remote
git push origin feat/add-services-page

# 5. Deploy branch to test environment
# (Cloudflare Pages creates preview automatically)

# 6. Test on live preview URL
# Click around, test on mobile, check forms

# 7. Merge to main when verified
git checkout main
git merge feat/add-services-page

# 8. Push to production
git push origin main

# 9. Clean up branch
git branch -d feat/add-services-page
git push origin --delete feat/add-services-page
```

### Branch Naming Conventions

**Feature Branches:**
```
feat/user-registration
feat/contact-form
feat/image-gallery
feat/blog-section
```

**Bug Fix Branches:**
```
fix/authentication-bug
fix/mobile-layout
fix/form-validation
```

**Hotfix Branches (Urgent Production Issues):**
```
hotfix/critical-security-patch
hotfix/site-down
```

**Content Update Branches:**
```
content/update-pricing
content/new-team-photos
```

**Refactor Branches:**
```
refactor/api-restructure
refactor/component-cleanup
```

### Deploy Branch to Test Environment

**Cloudflare Pages Preview Deployments:**

Every branch pushed to GitHub gets an automatic preview deployment:
```
Branch: feat/add-services-page
Preview URL: feat-add-services-page.project.pages.dev

Changes instantly deployed to preview URL
Test without affecting production
```

**Testing Checklist:**
- [ ] Feature works as intended
- [ ] No console errors
- [ ] Works on mobile
- [ ] Works on desktop
- [ ] Forms submit correctly
- [ ] Links work
- [ ] Images load
- [ ] No broken layouts

**Only After Testing:**
Merge to main and deploy to production.

### Why This Protects Production

**Without Branches:**
```
Commit broken code → Push to main → Production breaks
→ Clients complain → Emergency fix → Stress
```

**With Branches:**
```
Commit broken code → Push to branch → Test on preview
→ See it's broken → Fix on branch → Test again
→ Works → Merge to main → Production stays stable
```

**Real Example:**
"Added a contact form, but forgot to connect the email service. Without branch testing, form would have gone live broken. With preview testing, caught it immediately, fixed it, then deployed."

### Merge to Main Workflow

**Step-by-Step:**

**1. Ensure Branch Is Up-to-Date**
```bash
git checkout main
git pull origin main
git checkout feat/your-feature
git merge main  # Incorporate any changes made to main
```

**2. Test One Final Time**
After merging main into your branch, test again.

**3. Merge to Main**
```bash
git checkout main
git merge feat/your-feature
```

**4. Push to Production**
```bash
git push origin main
```

**5. Monitor**
Watch for:
- Successful deployment
- No errors in logs
- Site loads correctly
- Features work in production

**6. Clean Up**
```bash
git branch -d feat/your-feature
```

### Rollback Strategy

**If Production Breaks:**

**Option 1: Immediate Revert**
```bash
# Find the bad commit
git log --oneline

# Revert it
git revert abc1234

# Push immediately
git push origin main

# Production restored in ~60 seconds
```

**Option 2: Cherry-Pick Fix from Branch**
```bash
# Create hotfix branch
git checkout -b hotfix/critical-fix

# Make fix
git add .
git commit -m "Fix critical production issue"

# Test on preview

# Cherry-pick to main
git checkout main
git cherry-pick xyz5678

# Push
git push origin main
```

**Option 3: Reset to Last Known Good**
```bash
# Nuclear option - use only if necessary
git reset --hard [last-good-commit]
git push origin main --force

# Production immediately restored
```

### Communication with Clients

**Before Maintenance:**
```
"Hi [Client],

I'll be adding the new services page today. There may be a brief
moment where the site is updating, but it should be seamless.

I'll let you know once it's live!

Best,
[Your Name]"
```

**After Deployment:**
```
"Hi [Client],

The new services page is now live! Check it out at [URL].

Everything tested and working smoothly.

Let me know if you'd like any adjustments!

Best,
[Your Name]"
```

**If Something Breaks (Rare):**
```
"Hi [Client],

I discovered an issue after deployment and immediately rolled back
to the stable version. Your site is working normally.

I'm fixing the issue now and will deploy again shortly with proper
testing. No harm done.

Sorry for the brief confusion!

Best,
[Your Name]"
```

## Branch Management

### Creating Branches Per AI Session

**Pattern:**
One AI conversation = One feature branch (usually).

**Workflow:**
```bash
# Start new AI session
# AI: "What are we working on today?"
# You: "Adding user registration"

# Create branch
git checkout -b feat/user-registration

# Work with AI through the feature
# ... multiple commits ...

# When done
git checkout main
git merge feat/user-registration
git push origin main
```

**Benefits:**
- Clear separation of work
- Easy to rollback specific AI-generated changes
- Context isolation per feature
- Safe experimentation

### Branch Naming for AI Context

**Descriptive Names Help AI:**
```bash
# Good - AI understands the goal
feat/add-contact-form-with-validation

# Bad - AI doesn't know context
branch-1
```

**AI Prompt:**
```
"We're working on [feature]. I've created a branch called
feat/[feature-name]. Let's implement this step by step."
```

### When to Merge vs. Rebase

**Use Merge (Recommended for Most):**
```bash
git checkout main
git merge feat/your-feature
```

**Pros:**
- Preserves complete history
- Shows when features were integrated
- Easier to understand
- AI can do this without issues

**When to Use Rebase (Advanced):**
```bash
git checkout feat/your-feature
git rebase main
```

**Pros:**
- Clean, linear history
- No merge commits

**Cons:**
- Rewrites history (dangerous if shared)
- More complex to explain to AI
- Can cause issues if multiple people involved

**Recommendation:** Stick with merge for simplicity.

### Cleaning Up Old Branches

**Local Cleanup:**
```bash
# List all branches
git branch

# Delete merged branches
git branch -d feat/completed-feature

# Force delete unmerged branches (careful!)
git branch -D feat/abandoned-feature
```

**Remote Cleanup:**
```bash
# Delete remote branch
git push origin --delete feat/old-feature
```

**Automated Cleanup (GitHub):**
Enable "Automatically delete head branches" in repository settings.

**Regular Maintenance:**
Monthly review: Delete branches merged >30 days ago.

## Commit Strategies

### AI-Generated Commit Messages

**Let AI Suggest Messages:**
```
Prompt: "Review the git diff and suggest a commit message following
conventional commits format."

AI Response: "feat: add user registration form with email validation"
```

**Format:**
```
<type>: <description>

Types:
- feat: New feature
- fix: Bug fix
- docs: Documentation
- style: Code style (formatting, no logic change)
- refactor: Code refactoring
- test: Adding tests
- chore: Maintenance
```

**Examples:**
```bash
git commit -m "feat: add user registration with email validation"
git commit -m "fix: resolve authentication token expiration issue"
git commit -m "docs: update API documentation with new endpoints"
git commit -m "refactor: simplify database query logic"
```

### Should You Squash Commits?

**During Development (Pre-Release): No**
- Keep all commits
- Easier to debug
- Clear progression
- Can cherry-pick specific changes

**Before Merging to Main (Post-Release): Sometimes**

**Don't Squash:**
- If commits tell a clear story
- If you might need to revert parts
- If commits are well-organized

**Do Squash:**
- If many "WIP" commits
- If commits are "fix typo", "fix typo again", "actually fix typo"
- If you want a clean main branch history

**How to Squash:**
```bash
# Interactive rebase
git rebase -i HEAD~5  # Last 5 commits

# Editor opens, change "pick" to "squash" for commits to combine
# Save and close

# Git prompts for new commit message
# Write clean message

# Force push to branch (before merging to main)
git push origin feat/your-feature --force
```

### Preserving AI Decision History

**Why Keep Commits:**
- Shows AI reasoning progression
- Easier to understand what was tried
- Can review AI decisions later
- Helpful for learning

**In Commit Messages:**
```bash
git commit -m "feat: implement user auth with JWT

- AI suggested bcrypt for password hashing
- Tried argon2 but had dependency issues
- Settled on bcrypt per docs/decisions/auth.md"
```

**Use Extended Commit Messages:**
```bash
git commit -m "feat: add contact form" -m "Generated with Claude Code.
Includes email validation, spam protection via Turnstile, and email
delivery via Resend API."
```

### Meaningful Commit Messages

**Bad:**
```bash
git commit -m "update"
git commit -m "fix stuff"
git commit -m "changes"
```

**Good:**
```bash
git commit -m "Add contact form with email validation and Turnstile"
git commit -m "Fix mobile navbar toggle not closing on link click"
git commit -m "Update homepage hero image and CTA text"
```

**The Test:**
Can someone (including future you) understand what changed by reading the commit message alone?

## Recovery Workflows

### Handling AI-Introduced Bugs

**Scenario:** AI generated code that breaks something.

**Step 1: Identify When It Broke**
```bash
# Check recent commits
git log --oneline

# Identify suspicious commit
```

**Step 2: Review the Changes**
```bash
# See what the commit changed
git show abc1234
```

**Step 3: Decide on Fix**

**Option A: Revert the Entire Commit**
```bash
git revert abc1234
git push origin main
```

**Option B: Fix Forward**
```bash
# Tell AI about the bug
"The code from commit abc1234 has a bug: [describe]. Fix it."

# AI generates fix
git add .
git commit -m "Fix: resolve bug from previous AI implementation"
git push origin main
```

**Option C: Cherry-Pick the Good Parts**
```bash
# Revert the entire commit
git revert abc1234

# Manually reapply only the good changes
# Or use AI to help
"Keep features X and Y from commit abc1234, but remove feature Z
which caused the bug."
```

### Using Git Bisect

**When:** Bug exists, but not sure which commit introduced it.

**Workflow:**
```bash
# Start bisect
git bisect start

# Mark current state as bad
git bisect bad

# Find a commit you know was good
git log --oneline
git bisect good xyz5678

# Git checks out a commit in the middle
# Test if bug exists
# If yes:
git bisect bad
# If no:
git bisect good

# Repeat until Git identifies the bad commit
# Git will say: "abc1234 is the first bad commit"

# End bisect
git bisect reset

# Now you know exactly which commit broke things
```

**With AI:**
```
"Git bisect identified commit abc1234 as introducing the bug.
Here's the commit diff: [paste diff]

What's causing the issue and how do we fix it?"
```

### Rollback Procedures

**Emergency Rollback (Site Down):**

```bash
# 1. Check current state
git log --oneline

# 2. Identify last known good commit
# (before the problem started)

# 3. Reset to that commit
git reset --hard [good-commit]

# 4. Force push to restore production
git push origin main --force

# 5. Notify client (if applicable)
# 6. Fix issue on a branch, test, then deploy properly
```

**Time to Restore:** < 2 minutes

**Safer Rollback (Not Emergency):**
```bash
# Revert the problematic commit
git revert [bad-commit]

# Push
git push origin main

# This creates a new commit that undoes the bad one
# Preserves history
```

### Cherry-Picking Fixes

**Scenario:** Made a fix on wrong branch, need it on main.

```bash
# Find the commit with the fix
git log --oneline feat/wrong-branch

# Switch to correct branch
git checkout main

# Cherry-pick the fix commit
git cherry-pick abc1234

# Push
git push origin main
```

**AI Integration:**
```
"I accidentally committed fix abc1234 to feat/wrong-branch.
Cherry-pick it to main for me."
```

## Git Hooks for AI

### Pre-Commit Validation

**Automate Checks Before Committing:**

**Create `.git/hooks/pre-commit`:**
```bash
#!/bin/bash

# Run linter
npm run lint
if [ $? -ne 0 ]; then
    echo "Linting failed. Please fix errors before committing."
    exit 1
fi

# Run tests
npm run test
if [ $? -ne 0 ]; then
    echo "Tests failed. Please fix before committing."
    exit 1
fi

# Check for console.logs (optional)
if git diff --cached | grep -q "console.log"; then
    echo "Warning: console.log found. Remove before committing."
    # Uncomment to block:
    # exit 1
fi

echo "Pre-commit checks passed!"
```

**Make executable:**
```bash
chmod +x .git/hooks/pre-commit
```

**AI Integration:**
```
"Before each commit, run linter and tests automatically via git hook.
If they fail, prevent the commit."
```

### Automated Testing Hooks

**Pre-Push Hook:**
```bash
#!/bin/bash

echo "Running tests before push..."

npm run test:unit
if [ $? -ne 0 ]; then
    echo "Unit tests failed. Push aborted."
    exit 1
fi

npm run test:integration
if [ $? -ne 0 ]; then
    echo "Integration tests failed. Push aborted."
    exit 1
fi

echo "All tests passed. Pushing..."
```

### Linting Before Commit

**Hook That Fixes Issues:**
```bash
#!/bin/bash

echo "Running auto-fix linter..."

# Run linter with auto-fix
npm run lint:fix

# Stage the fixed files
git add .

echo "Linting complete!"
```

**AI Can Generate These:**
```
"Create a pre-commit git hook that runs 'npm run lint:fix' and
auto-stages the fixed files."
```

## Collaborative Git with Multiple AI Agents

### Managing Parallel Development

**Scenario:** Using multiple AI agents on different features.

**Strategy:**
```bash
# Agent 1: Frontend
git checkout -b feat/frontend-dashboard
# ... work ...

# Agent 2: Backend API
git checkout -b feat/backend-api
# ... work ...

# Merge both when ready
git checkout main
git merge feat/frontend-dashboard
git merge feat/backend-api
```

**Coordination:**
- Use separate branches per agent/feature
- Document dependencies in docs/
- Merge frequently to avoid large conflicts
- Test integrated system before production deployment

### Merge Conflict Resolution

**When Conflicts Happen:**

```bash
# Try to merge
git merge feat/other-feature

# Git says: CONFLICT in src/components/Header.astro

# See conflicts
git status

# Open file, see conflict markers:
<<<<<<< HEAD
Current code
=======
Incoming code
>>>>>>> feat/other-feature
```

**With AI:**
```
"I have a merge conflict in Header.astro between these two versions:

Version A (current):
[paste code]

Version B (incoming):
[paste code]

Resolve the conflict by combining the best of both while maintaining
functionality."
```

**After Resolving:**
```bash
git add src/components/Header.astro
git commit -m "Merge feat/other-feature, resolve Header conflicts"
```

### Context Preservation Across Branches

**Use Docs for Shared Context:**

```
docs/
├── architecture/
│   └── api-design.md          # Both agents reference
├── context/
│   ├── agent1-frontend.md     # Agent 1's current state
│   └── agent2-backend.md      # Agent 2's current state
```

**Agent 1 (Frontend):**
```
"Read docs/architecture/api-design.md for API contracts.
Continue frontend work on feat/frontend-dashboard branch."
```

**Agent 2 (Backend):**
```
"Read docs/architecture/api-design.md for API contracts.
Continue backend work on feat/backend-api branch."
```

**Both Stay Aligned:** Shared documentation keeps agents on same page.

## Key Takeaways

### The Two-Phase Approach
**Pre-Release: Fast and simple**
- Push to main
- Iterate quickly
- No branching overhead

**Post-Release: Stable and safe**
- Mandatory branches
- Test before merge
- Protect production

### Time Investment vs. Risk
**Development Phase:**
- Risk: Low (no users)
- Branching value: Low
- Direct to main: Appropriate

**Maintenance Phase:**
- Risk: High (users depend on site)
- Branching value: High
- Branch workflow: Essential

### Recovery > Prevention
**You will make mistakes:**
- Commit frequently
- Test before pushing
- Have rollback plan
- Don't fear breaking things (you can fix them)

**Git is your safety net:**
- Every commit is a restore point
- Reverting is simple
- History is preserved
- Remote is your backup

### AI Integration
**Git workflows that work well with AI:**
- Simple branching models
- Clear commit messages
- Frequent commits
- Documented processes

**What to avoid:**
- Complex rebasing
- Interactive rebases
- Cherry-picking marathons
- Confusing branch structures

---

**Related Documentation:**
- [Phase 2: Development](./phase-2-development.md) - Development workflows
- [Phase 4: Deployment](./phase-4-deployment.md) - Production deployment
- [Context Management](../context-management/README.md) - Using docs/ for coordination
- [Troubleshooting: Recovery Patterns](../troubleshooting/recovery-patterns.md) - Emergency procedures
- [Client Management](../business-model/client-management.md) - Communicating deployments

**Back to:** [Workflow Overview](./README.md)
