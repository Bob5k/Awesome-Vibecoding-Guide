# Phase 2: Development 🧩

**Tools:** Your preferred IDE/CLI + Coding agent + MCP servers

---

## Prerequisites: Environment Setup

Before starting development, set up your coding environment. This is the bridge between planning (Phase 1) and actual implementation.

### 1. Choose Your Development Environment

Pick the setup that matches your workflow preferences:

#### Option A: IDE-Based Development

**Cursor** (Recommended for beginners)
- Built-in AI coding assistant
- Excellent Claude integration
- VSCode-compatible extensions
- Great for visual development

**Zed** (Fast and minimalist)
- Lightning-fast performance
- Native AI integration
- Great for experienced developers
- Minimal configuration needed

**VS Code + Extensions**
- Most flexible and customizable
- Wide extension ecosystem
- Use with Claude Code extension
- Perfect if you're already familiar with VS Code

#### Option B: CLI-Based Development

**Claude Code CLI** (Recommended)
- Official Anthropic CLI tool
- Direct Claude integration
- Terminal-based workflow
- Excellent for automation and scripting
- Works with your preferred text editor

**Droid**
- Alternative CLI coding agent
- Multi-model support
- Good for advanced users
- Customizable workflows

### 2. Set Up MCP Servers

MCP (Model Context Protocol) servers extend your coding agent's capabilities.

**Essential MCP Servers:**

**Context7 MCP** - Codebase understanding
- Provides intelligent context about your codebase
- Helps AI understand project structure
- Required for large codebases
- [Setup guide](../tools-and-tech-stack/mcp-servers.md)

**DevTools MCP** - Browser automation
- Automated testing in real browsers
- Debug frontend issues automatically
- Essential for web development
- Integrates with Chrome/Firefox

**Web Search MCP** - Internet access
- Search documentation and Stack Overflow
- Find solutions to errors
- Check latest package versions
- Stay updated on best practices

**Optional but Useful:**
- **File System MCP** - Enhanced file operations
- **Database MCP** - Direct database queries
- **GitHub MCP** - Repository management
- **Terminal MCP** - Shell command execution

### 3. Configure Your Coding Agent

Set up your preferred AI model for development:

**GLM** (Great for implementation)
- Fast and cost-effective
- Strong coding capabilities
- Good for rapid prototyping
- Handles most development tasks

**Claude** (Best for architecture)
- Excellent reasoning
- Great for complex problems
- Strong refactoring abilities
- Best for code review

**GPT** (Balanced option)
- Good all-around performance
- Wide knowledge base
- Reliable for most tasks
- Good documentation understanding

**Gemini** (Alternative)
- Strong analytical skills
- Good for debugging
- Handles large contexts well
- Cost-effective option

### 4. Verify Your Setup

Before starting development, ensure:
- ✅ IDE/CLI is installed and configured
- ✅ Coding agent is connected and working
- ✅ Essential MCP servers are running
- ✅ You can access project documentation
- ✅ Git is configured for commits

---

## Development Workflow

Once your environment is ready, follow this systematic approach:

### 1. Load Project Context

Open the project in your development environment.

Load the relevant feature specification into context:
```bash
# Read the feature spec and tasks
"Load feature-1-spec.md and feature-1-tasks.md into context"
```

### 2. Feature-by-Feature Implementation

Work on **one feature at a time** to maintain focus and manage context efficiently.

**For each feature:**

**a. Review the tasks**
```
"Show me all tasks for the authentication feature"
```

**b. Implement task by task**
```
"Implement task 1: Set up user schema in database"
```

**c. Manual review after each task**
- Check the generated code
- Test the functionality
- Verify it matches the spec
- Make adjustments if needed

**d. Comprehensive review after the feature**
- Test all feature components together
- Check integration with existing code
- Verify all acceptance criteria are met
- Run automated tests if available

**e. Commit the completed feature**
```bash
git add .
git commit -m "feat: implement user authentication"
```

### 3. Context Management

Keep context clean and relevant:

**Do:**
- ✅ Load only the current feature spec
- ✅ Reference related code files as needed
- ✅ Clear old context when switching features
- ✅ Use MCP servers for codebase queries

**Don't:**
- ❌ Load all specs at once
- ❌ Keep completed features in context
- ❌ Mix multiple features in one session
- ❌ Ignore context size limits

---

## Development Rules

**One Feature at a Time**
- Don't mix features in the same session
- Complete one feature before starting another
- Keeps context manageable
- Easier to debug and review

**Modular Code**
- Write self-contained components
- Clear interfaces between modules
- Easier to understand and modify
- Better context management

**Commit Frequently**
- Commit after each completed task (optional)
- Always commit after completing a feature
- Write clear commit messages
- Makes rollback easier if needed

**Review Manually**
- Never merge without reviewing
- AI can make mistakes
- Verify logic and edge cases
- Test before committing

---

## Example Development Session

### Session 1: User Authentication Feature

**Setup**
```bash
"Load feature: user-authentication
Read: feature-1-spec.md, feature-1-tasks.md"
```

**Task 1: Database Schema**
```bash
"Implement Task 1: Create user schema with email, password hash, and timestamps"
# Review code
# Test schema
git add .
git commit -m "feat(auth): add user database schema"
```

**Task 2: Registration Endpoint**
```bash
"Implement Task 2: Create POST /api/register endpoint with validation"
# Review implementation
# Test endpoint manually
git add .
git commit -m "feat(auth): add user registration endpoint"
```

**Task 3: Login Endpoint**
```bash
"Implement Task 3: Create POST /api/login endpoint with JWT generation"
# Review code
# Test login flow
git add .
git commit -m "feat(auth): add login endpoint with JWT"
```

**Task 4: Auth Middleware**
```bash
"Implement Task 4: Create JWT verification middleware for protected routes"
# Review middleware
# Test protected routes
git add .
git commit -m "feat(auth): add JWT authentication middleware"
```

**Feature Review**
```bash
# Test entire authentication flow
# Verify all acceptance criteria
# Check integration with app
git checkout -b feature/user-auth
# Merge to main after review
```

### Session 2: Dashboard UI Feature

Start fresh with new feature context...

---

## Tips for Effective Development

✅ **Take breaks between features** - Fresh mind catches more issues

✅ **Use descriptive commit messages** - Future you will thank you

✅ **Test incrementally** - Don't wait until everything is "done"

✅ **Leverage MCP servers** - Let AI explore codebase structure

✅ **Ask for alternatives** - If stuck, request different approaches

✅ **Keep tasks small** - Easier to implement and review

✅ **Document as you go** - Add comments for complex logic

---

## Common Pitfalls to Avoid

❌ **Starting without environment setup** - Wastes time during development

❌ **Mixing multiple features** - Creates context chaos and bugs

❌ **Skipping manual reviews** - AI can miss edge cases

❌ **Large commits** - Hard to review and debug

❌ **Ignoring MCP capabilities** - Makes context management harder

❌ **Not testing incrementally** - Issues compound and become hard to fix

---

## Next Steps

Once you've implemented your features:

1. ✅ All features are implemented
2. ✅ Code is committed to version control
3. ✅ Manual testing shows core functionality works
4. → **Next**: [Comprehensive testing and debugging](./phase-3-testing-debugging.md)

---

Next: [Phase 3 → Testing & Debugging](./phase-3-testing-debugging.md)

Back: [Workflow overview](./README.md)
