# Phase 2: Development 🧩

**Tools:** Your preferred IDE/CLI + Coding agent + MCP servers

---

## Prerequisites: Environment Setup

Before starting development, set up your coding environment. This is the bridge between planning (Phase 1) and actual implementation.

### 1. Choose Your Development Environment

Pick the setup that matches your workflow preferences:

#### Option A: IDE-Based Development

**Zed** (Fast and minimalist - my choice)
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

**Droid** (Recommended)
- Alternative CLI coding agent
- Multi-model support
- Good for advanced users
- Customizable workflows

**Claude Code CLI**
- Official Anthropic CLI tool
- Direct Claude integration
- Terminal-based workflow
- Excellent for automation and scripting
- Works with your preferred text editor

### 2. Set Up MCP Servers

MCP (Model Context Protocol) servers extend your coding agent's capabilities.

**Essential MCP Servers:**

**Context7 MCP** - your chosen tech stack documentation and understanding
- [Setup guide](../development-tools/mcp-servers.md)

**DevTools MCP** - Browser automation
- Automated testing in real browsers
- Debug frontend issues automatically
- Essential for web development
- Integrates with Chrome

**Task Manager MCP** - To easily manage tasks and projects
- Organize tasks and projects
- Prioritize tasks
- Track progress

**Sequential Thinking MCP** - To manage knowledge and plan before coding
- Organize thoughts and ideas
- Prioritize tasks
- Develop right things without overengineering the rest
- Track the thinking process and have it saved instead of relying only on Agent's memory

**ShadCN MCP** - UI component library
- Enhance your UI with pre-built components
- Save time and effort
- Integrates with your preferred framework

### 3. Configure Your Coding Agent

Set up your preferred AI model for development:

**GLM** (Great for implementation - my general choice)
- Fast and cost-effective (SUPER cost-effective compared vs others)
- Strong coding capabilities
- Good for rapid prototyping
- Handles most development tasks

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

## Development Troubleshooting

**Common problems during feature implementation and their solutions**

### AI Generates Code That Doesn't Match Spec

**Symptoms:**
- Implements wrong feature
- Missing required functionality
- Different behavior than expected

**Quick fix:**
```
"The code doesn't match the spec. Specifically:

Spec says: [exact requirement from spec]
Your code does: [what was actually implemented]

Expected behavior: [detailed description]
Actual behavior: [what happens]

Please update to match spec exactly."
```

**Prevention:**
- Reference spec file explicitly: "Per docs/plans/feature-x.md, implement..."
- Include examples in spec
- Define success criteria clearly
- Review code against spec before moving on

**Related:** [AI Misunderstands Requirements](../troubleshooting/README.md#ai-misunderstands-requirements)

---

### Code Quality Issues

#### Missing Error Handling

**Symptom:** Code works in happy path but crashes on errors.

**Quick fix:**
```
"Add comprehensive error handling:

```typescript
// Current code
const user = await db.users.findById(id);
return user.name; // Crashes if user is null
```

Add error handling:
- Check if user exists (return 404 if not)
- Try-catch around database calls
- User-friendly error messages
- Log errors for debugging

Follow error pattern from src/api/posts.ts"
```

**Prevention:**
- Always specify error handling in initial prompt
- Use [Error Handling Template](../prompting/template-library.md#template-16-security-fix)
- Reference existing error patterns

---

#### Missing Input Validation

**Symptom:** No validation on user input, potential security issues.

**Quick fix:**
```
"Add input validation:

Required validation:
- Email: valid format, max 255 chars
- Password: min 8 chars, complexity requirements
- Age: number, 18-120 range

Use [your validation library] for validation.
Return 400 with field-specific errors for invalid input."
```

**Prevention:**
- Specify validation in initial prompt
- Use validation library (Zod, Joi, express-validator)
- Create validation template

**Related:** [Missing Input Validation](../troubleshooting/README.md#missing-input-validation)

---

#### Security Vulnerabilities

**Symptom:** Code review reveals SQL injection, XSS, or other vulnerabilities.

**Quick fix:**
```
"Security audit this code:

[paste code]

Fix:
- SQL injection: use parameterized queries
- XSS: sanitize user input before rendering
- Authentication: verify JWT on protected routes
- Authorization: check user permissions
- Secrets: move to environment variables

Follow security patterns from src/api/auth.ts"
```

**Prevention:**
- Mention security in every prompt
- Use [Security Templates](../prompting/template-library.md#security-templates)
- Regular security audits
- Follow OWASP guidelines

**Related:** [Insecure Code Generation](../troubleshooting/README.md#insecure-code-generation)

---

### Integration Problems

#### New Code Breaks Existing Features

**Symptoms:**
- Tests that previously passed now fail
- Features that worked now broken
- Unexpected side effects

**Quick diagnosis:**
```bash
# Run tests to identify breakage
npm test

# Check git diff to see what changed
git diff main...feature-branch

# Identify integration points
grep -r "functionThatChanged" src/
```

**Quick fix:**
```
"The new [feature] breaks [existing feature].

What breaks:
- [Specific test/feature that fails]
- Error: [error message]

Integration points:
- [New code] calls [existing code]
- [Existing code] expects [interface] but gets [different interface]

Fix requirements:
- Maintain backward compatibility
- Update [existing code] if needed
- Ensure all tests pass
- No breaking changes to public API"
```

**Prevention:**
- Always specify: "Don't break existing features"
- Run tests after each change
- Write integration tests
- Review changes carefully

**Related:** [Breaking Changes Flowchart](../troubleshooting/README.md#flowchart-4-breaking-changes)

---

#### API Contract Mismatches

**Symptom:** Frontend expects different response format than backend provides.

**Quick fix:**
```
"API contract mismatch:

Frontend expects:
{ data: { id, name, email }, success: true }

Backend returns:
{ id, name, email }

Update backend to match frontend contract OR update frontend to handle backend format.

Preferred: Update backend (less disruption).
Ensure consistent API response format across all endpoints."
```

**Prevention:**
- Define API contracts upfront (docs/api/endpoints.md)
- Use TypeScript interfaces shared between FE/BE
- Generate types from OpenAPI spec
- Integration tests for API contracts

---

### Context Management Failures During Development

#### AI Loses Track of Architecture

**Symptom:** AI suggests solutions that violate project architecture or patterns.

**Quick fix:**
```
"You suggested [solution] but our architecture uses [different approach].

Our architecture (from docs/architecture/overview.md):
- [Key principle 1]
- [Key principle 2]

Please revise solution to match our architecture.
Specifically: [what needs to change]"
```

**Prevention:**
- Reference architecture docs at session start
- Create .cursorrules with architecture notes
- Remind AI of architecture when it deviates
- Keep architecture docs updated

**Related:** [Context-Aware Prompting](../prompting/advanced-techniques.md#context-aware-prompting)

---

#### Forgets Coding Standards

**Symptom:** Code style inconsistent with project (tabs vs spaces, naming, patterns).

**Quick fix:**
```
"Code style doesn't match project standards.

Your code uses:
- camelCase for file names (we use kebab-case)
- Class components (we use functional only)
- .then() chains (we use async/await)

Please rewrite following our standards in .cursorrules"
```

**Prevention:**
- Create .cursorrules with all conventions
- Reference style guide in prompts
- Use code formatter (Prettier)
- Regular style checks

**Related:** [Code Style Issues](../troubleshooting/README.md#code-style-doesnt-match-project)

---

### Prompt Quality Issues

#### Too Many Iterations

**Symptom:** Takes 5-10 attempts to get working code.

**Root causes:**
- Vague initial prompt
- Missing examples
- No success criteria

**Quick fix:**
Apply 4-component framework:

```
[CLARITY]: Implement user profile update endpoint

[CONTEXT]:
- Pattern: Follow POST /users pattern in src/api/users.ts
- Validation: Use ValidationMiddleware from src/middleware/validation.ts
- Schema: User model in src/models/User.ts

[CONSTRAINTS]:
- User can only update own profile (or admin can update any)
- Updatable fields: name, email, bio (NOT password, role)
- Email must remain unique
- Max bio length: 500 characters

[CRITERIA]:
- PUT /api/users/:id returns updated user (200)
- Returns 403 if user tries to update another user's profile
- Returns 409 if email already exists
- Returns 400 for validation errors
- Tests pass
```

**Prevention:**
- Study [Prompt Foundations](../prompting/foundations.md)
- Use [Prompt Templates](../prompting/template-library.md)
- Always include examples
- Define success criteria

---

#### AI Ignores Requirements

**Symptom:** Generated code missing specified features or violating constraints.

**Quick fix:**
```
"Your code is missing these requirements:

Required but missing:
1. [Requirement 1] - NOT implemented
2. [Requirement 2] - NOT implemented

Please add missing requirements. I'll verify:
- [Check 1]
- [Check 2]
before accepting the code."
```

**Prevention:**
- Use numbered lists for requirements (harder to miss)
- Add "MUST" or "REQUIRED" for critical items
- Request AI confirms understanding before implementing
- Use self-checking prompts

**Related:** [AI Ignores Constraints](../troubleshooting/README.md#ai-ignores-constraints)

---

## Debugging Checklist for Development Phase

When something goes wrong during development:

### Before Asking AI for Help

- [ ] Read error message completely
- [ ] Check file:line from stack trace
- [ ] Verify all required files exist
- [ ] Check for typos in variable/function names
- [ ] Ensure dependencies installed (npm install)
- [ ] Try simplest possible reproduction

### Gathering Context for AI

- [ ] Error message (full text)
- [ ] Stack trace (relevant lines)
- [ ] Code at error location (with context)
- [ ] What you were trying to do
- [ ] What you've already tried
- [ ] Minimal reproduction if possible

### Prompt for Debugging

Use this template:

```
"Debug this error:

ERROR MESSAGE:
[exact error text]

STACK TRACE:
[relevant lines with file:line]

CODE ([file]):
[code snippet around error]

CONTEXT:
- Doing: [action that triggered error]
- Environment: [dev/prod]
- Started when: [recent change]

EXPECTED: [what should happen]
ACTUAL: [what actually happens]

TRIED:
- [Attempt 1] → [result]
- [Attempt 2] → [result]"
```

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

## Pre-requisites & Next Steps

**Requires completion of:**
- [Phase 1: Planning](./phase-1-planning.md) — Feature specifications and project structure
- [Core Technologies setup](../core-technologies.md) — Astro + Tailwind + Cloudflare stack
- [Tool preparation](./phase-0-vibecoder-preparation.md) — Development environment and coding agent

**Prepares for:**
- [Phase 3: Testing & Debugging](./phase-3-testing-debugging.md) — Comprehensive testing and quality assurance
- [Phase 4: Deployment](./phase-4-deployment.md) — Production deployment and CI/CD
- [Business strategy](../introduction/README.md) — Client delivery and maintenance workflows

**Related Reading:**
- [Development Tools](../development-tools/README.md) — Detailed tool configuration and usage
- [AI Model Providers](../ai-model-providers/README.md) — Optimization for different development tasks
- [Context Management](../context-management/README.md) — Efficient context handling during development

## Next Steps

Once you've implemented your features:

1. ✅ All features are implemented
2. ✅ Code is committed to version control
3. ✅ Manual testing shows core functionality works
4. ✅ Context management practices followed
5. → **Next**: [Comprehensive testing and debugging](./phase-3-testing-debugging.md)

---

Next: [Phase 3 → Testing & Debugging](./phase-3-testing-debugging.md)

Back: [Workflow overview](./README.md)
