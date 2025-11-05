# Droid CLI — The Ultimate Coding Agent 🤖

> **Get Started with Droid CLI:** [Sign up here with my referral link](https://app.factory.ai/r/VAH64803) to support the guide and get access to this powerful coding assistant.

## Why Droid CLI is a Game-Changer

Droid CLI isn't just another coding assistant—it's a comprehensive development environment that combines intelligent planning with safe, controlled execution. It stands out with features that fundamentally change how you approach software development.

## 🎯 Killer Feature: Autonomous Spec Generation

### The Magic of Plan Mode

**Traditional workflow:**
1. Write detailed specs manually
2. Break down into tasks
3. Hope AI understands your vision

**Droid CLI workflow:**
1. Describe what you want to achieve in plain English
2. Set Droid to "plan mode"
3. Let it create comprehensive, spec-like plans automatically
4. Review and approve the generated plan
5. Watch as the agent executes the approved plan perfectly

**Example:**
```
User: "I want to build a task management app with user authentication, 
real-time updates, and mobile responsiveness"

Droid (Plan Mode): Creates detailed 15-step plan including:
- Database schema design
- Authentication flow
- API endpoint structure
- Frontend component architecture
- Real-time features implementation
- Testing strategy
- Deployment configuration
```

### Plan Persistence and Reusability

- **Automatic .md file saving** - Every approved plan is saved as a markdown file
- **Plan versioning** - Track changes and iterations of your development plans
- **Template creation** - Reuse successful plans for similar projects
- **Team collaboration** - Share plans with team members for consistency

**Pro Tip:** You can disable .md saving if you prefer a more streamlined workflow, but keeping plans creates a valuable knowledge base over time.

## 🛡️ Revolutionary Permission System

### The "Not Total Yolo" Approach

Unlike other coding agents that run wild with unrestricted access, Droid introduces a sophisticated permission system that prevents disasters while maintaining productivity.

**Permission Levels:**

**🟢 Low Permission Mode - Read & Write Only**
- Can read and modify files
- Cannot execute system commands
- Cannot install dependencies
- Cannot modify system configuration
- **Perfect for:** Simple code changes, file refactoring, content updates

**🟡 Medium Permission Mode - Reversible Commands Only**
- Can read/write files
- Can execute reversible commands (npm install, git operations)
- Cannot perform destructive system changes
- Cannot modify system-level configurations
- **Perfect for:** Feature development, dependency management, version control

**🔴 High Permission Mode - Full Access**
- All system capabilities
- Use with caution for complex infrastructure changes
- **Perfect for:** Advanced DevOps, system configuration (when absolutely necessary)

### Real-World Safety Benefits

**Prevents Regrettable Actions:**
- No accidental `rm -rf` disasters
- No system configuration corruption
- No irreversible dependency conflicts
- No AI "hallucination" damage

**Builds Trust:**
- Start with low permissions, escalate as needed
- Review each permission elevation
- Maintain control over what the agent can do
- Peace of mind for production environments

## 🔄 Workflow Integration Excellence

### Replacing OpenSpec for Most Use Cases

**When Droid CLI alone is sufficient:**
- Most feature development
- Standard web applications
- API development
- Frontend implementations
- Routine maintenance tasks

**When to supplement with OpenSpec:**
- Extremely complex enterprise systems
- Multi-team project coordination
- Projects requiring extensive documentation
- Client-facing specification requirements

### Seamless Development Workflow

**Daily Development Cycle:**
1. **Morning Planning Session**
   ```
   "I want to implement user role-based access control for the admin dashboard"
   → Droid generates comprehensive plan
   → Review and approve
   → Plan saved as rbac-implementation.md
   ```

2. **Development Execution**
   ```
   Droid follows the approved plan step by step
   → Real-time progress updates
   → Automatic error handling
   → Quality checkpoints
   ```

3. **Integration with DevTools MCP**
   ```
   "Test the role-based permissions we just implemented"
   → Droid coordinates with DevTools MCP
   → Automated testing of all user roles
   → Bug fixes and refinements
   ```

## 🚀 Advanced Features

### Model Routing Intelligence

Droid CLI intelligently routes different types of tasks to the most suitable AI models:

- **GPT-4/Claude** for general coding tasks
- **Codex** for complex algorithm implementations
- **GPT-5-high** for large-scale architectural decisions
- **Specialized models** for specific frameworks/languages

### Context Management

- **Persistent project context** - Maintains understanding of your codebase
- **Cross-session memory** - Remembers previous work and decisions
- **Incremental learning** - Gets better at understanding your coding style
- **Dependency tracking** - Understands how changes affect other parts

### Error Recovery

- **Automatic retry mechanisms** - Handles temporary failures gracefully
- **Rollback capabilities** - Reverts problematic changes
- **Alternative approach suggestions** - When initial attempts fail
- **Learning from failures** - Improves future suggestions

## 💡 Pro Tips for Maximum Productivity

### 1. Start Conservative
Begin with Low Permission mode and only escalate when necessary. You'll be surprised how much can be accomplished safely.

### 2. Plan First, Execute Second
Always use Plan mode for new features. The quality of AI-generated plans is often better than manual spec writing.

### 3. Leverage Plan Persistence
Keep the generated .md files as documentation. They become valuable project artifacts and onboarding materials.

### 4. Combine with DevTools MCP
Use DevTools MCP for testing while Droid handles the implementation. This combination is incredibly powerful.

### 5. Iterate on Plans
Don't accept the first generated plan. Ask for modifications, add your constraints, and perfect it before execution.

## 🎯 The Bottom Line

Droid CLI represents a fundamental shift in how we interact with AI for software development. Instead of being a simple code completion tool, it becomes a development partner that:

- **Thinks before it acts** (Planning mode)
- **Respects your boundaries** (Permission system)
- **Learns from your project** (Context management)
- **Executes with precision** (Agent coordination)

The combination of autonomous planning and safety-first execution makes Droid CLI not just another tool, but a complete development environment that can replace multiple tools in your workflow while providing unprecedented control and safety.

See also: [OpenSpec CLI](./openspec-cli.md), [DevTools MCP](../mcp-servers/devtools-mcp.md)

Back: [Tools & Tech Stack](../README.md)