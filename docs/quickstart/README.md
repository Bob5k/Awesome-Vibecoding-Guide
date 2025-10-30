# Quickstart 🚀

Welcome to the Awesome Vibecoding Guide! This quickstart will get you up and running with modern AI-powered development workflows, including essential Git/GitHub practices.

## 🎯 Phase 1: Project Setup & Planning

### 1. Define Your Project Vision
- Write a brief Product Requirements Document (PRD)
- Define key features and outcomes
- Set clear success criteria

### 2. Create Specifications
- Use OpenSpec or your preferred format for detailed feature specs
- Break down complex features into manageable tasks
- Define technical requirements and constraints

### 3. Initialize Version Control ⭐ **CRITICAL STEP**

**Never code without Git!** Remote repositories are your safety net and collaboration foundation.

#### Basic Git Setup:
```bash
# Configure Git (first time only)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Create local repository
git init

# Create remote repository on GitHub/GitLab
# Visit github.com → New repository → Clone or add remote
git remote add origin https://github.com/yourusername/yourproject.git
```

#### Push Initial Setup:
```bash
# Add all files
git add .
git commit -m "Initial project setup with specifications"
git push -u origin main
```

## 🛠️ Phase 2: Development Environment Setup

### 4. Set Up Your Tech Stack
- **Editor**: Zed (recommended) or your preferred IDE
- **AI Assistant**: GLM Coding Agent or similar
- **MCP Servers**: Context7 MCP, DevTools MCP
- **Version Control**: Git + GitHub/GitLab

### 5. Project Structure Best Practices
```
your-project/
├── docs/              # Project documentation
├── specs/             # Feature specifications
├── src/               # Source code
├── tests/             # Test files
└── README.md          # Project overview
```

## 🚀 Phase 3: Development Workflow

### 6. Branch Strategy: Safe Development

#### 🟢 For New Projects (No Production Yet)
**Simple Approach - Direct Commits to Main:**
```bash
# Work directly on main branch
git add .
git commit -m "Feature: User authentication system"
git push origin main
```

**Why this works for new projects:**
- No production code to break
- Commits serve as guardrails and checkpoints
- Easy to revert if something goes wrong
- Faster workflow for rapid prototyping

#### 🔴 For Live Projects (Production Environment)
**Safe Approach - Feature Branches:**
```bash
# Create feature branch
git checkout -b feature/user-dashboard
# Develop feature...
git add .
git commit -m "Implement user dashboard UI"
git push origin feature/user-dashboard

# Test thoroughly, then merge
git checkout main
git merge feature/user-dashboard
git push origin main
```

**Why branches are essential for production:**
- Prevents breaking live functionality
- Allows isolated testing and review
- Enables parallel development
- Provides rollback safety net

### 7. Development Process

#### Context Management:
- Load only relevant files into AI context
- Keep focused on current task
- Avoid overwhelming AI with entire codebase

#### Task Implementation:
- Work one feature at a time
- Review AI-generated code before acceptance
- Test using DevTools MCP for automated verification
- Perform manual testing for user experience validation

## 🔄 Phase 4: Commit & Push Workflow

### 8. Commit Best Practices

**Commit Frequency:**
- **Push after each meaningful feature completion**
- **Commit at major milestones** (setup, core features, testing)
- **Don't wait too long** - frequent pushes prevent data loss

**Commit Message Format:**
```bash
git commit -m "Type: Brief description"

# Examples:
git commit -m "feat: Add user registration form"
git commit -m "fix: Resolve authentication token issue"
git commit -m "docs: Update API documentation"
git commit -m "test: Add unit tests for user service"
```

**Commit Types:**
- `feat:` New features
- `fix:` Bug fixes
- `docs:` Documentation changes
- `test:` Test additions/improvements
- `refactor:` Code refactoring
- `chore:` Maintenance tasks

### 9. Push Workflow

#### Basic Workflow (New Projects):
```bash
# After completing a feature:
git add .
git commit -m "feat: Implement user profile page"
git push origin main
```

#### Advanced Workflow (Production Projects):
```bash
# Create feature branch
git checkout -b feature/payment-integration

# Develop and test...
git add .
git commit -m "feat: Add Stripe payment integration"
git push origin feature/payment-integration

# After testing and review:
git checkout main
git merge feature/payment-integration
git push origin main

# Clean up
git branch -d feature/payment-integration
```

## 🛡️ Phase 5: Safety & Recovery

### 10. Git as Your Ultimate Safety Net

**Commits are Your Guardrails:**
- Every commit is a save point you can return to
- No fear of "breaking everything" - you can always revert
- Experimental changes are safe with version control

**Recovery Commands:**
```bash
# View commit history
git log --oneline

# Revert to previous commit (creates new commit)
git revert <commit-hash>

# Reset to previous commit (use with caution)
git reset --hard <commit-hash>

# View changes before committing
git diff
git status
```

### 11. Remote Backup Benefits

**Why Remote Repositories are Essential:**
- **Data Safety**: Code backed up in the cloud
- **Collaboration**: Easy team coordination
- **Deployment**: CI/CD integration
- **Portfolio**: Show your work to potential clients/employers

**GitHub/GitLab Features:**
- **Pull/Merge Requests**: Code review and collaboration
- **Issues**: Bug tracking and feature requests
- **Actions**: Automated testing and deployment
- **Pages**: Free hosting for documentation/demos

## 📋 Quickstart Checklist

### Before You Start Coding:
- [ ] Create GitHub/GitLab account
- [ ] Install and configure Git
- [ ] Create remote repository
- [ ] Write initial project specs
- [ ] Set up development environment

### During Development:
- [ ] Push initial setup to remote
- [ ] Choose appropriate branching strategy
- [ ] Commit frequently with descriptive messages
- [ ] Test thoroughly before pushing
- [ ] Use DevTools MCP for automated testing

### For Production Projects:
- [ ] Always use feature branches
- [ ] Create pull/merge requests for review
- [ ] Test in staging environment
- [ ] Deploy with rollback plan
- [ ] Monitor production closely

## 🚀 Next Steps

You're now ready to start vibecoding! With proper Git workflow and AI assistance, you can develop faster, safer, and more efficiently.

**Recommended Reading:**
- [Tools & Tech Stack 🧰](../tools-and-tech-stack/README.md)
- [Workflow & Process 🔄](../workflow/README.md)
- [Phase 1: Planning](../workflow/phase-1-planning.md)

**Remember:** Git is your best friend in AI-powered development. The combination of version control and AI assistance creates an unstoppable development workflow!

---

Back to index: [Top‑level README](../../README.md)