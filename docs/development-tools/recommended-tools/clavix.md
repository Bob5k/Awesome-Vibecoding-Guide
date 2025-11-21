# Clavix — CLEAR-Based PRD Generator 📋

Clavix is an open-source prompt engineering framework that transforms rough ideas into polished prompts, complete PRDs (Product Requirements Documents), and ready-to-implement task lists. Built on the academically-validated CLEAR methodology, it bridges the gap between initial concepts and production-ready implementation.

## 🎯 Core Value Proposition

### CLEAR-Based Approach

Clavix leverages the **CLEAR framework** for systematic prompt optimization:
- **C**oncise — Eliminates ambiguity and noise
- **L**ogical — Ensures structured, rational flow
- **E**xplicit — Makes requirements and expectations crystal clear
- **A**daptive — Adjusts to context and specific needs
- **R**eflective — Incorporates feedback and iteration

This methodology ensures consistency and quality across all AI interactions, from simple prompts to complex project specifications.

### Seamless PRD Generation

Transform vague ideas into production-ready documentation:

1. **Rough Idea** → Describe what you want to build in plain language
2. **CLEAR Optimization** → Framework refines and structures your input
3. **Complete PRD** → Get comprehensive Product Requirements Document
4. **Task List** → Ready-to-implement tasks with clear acceptance criteria
5. **Progress Tracking** → Monitor implementation and mark tasks complete

**The result:** From concept to actionable implementation plan in minutes, not hours.

## 🚀 Main Use Cases

### 1. Feature Planning & Specification

**Workflow:**
```
User: "I want to add user authentication with social login"

Clavix Output:
→ Optimized prompt with CLEAR framework
→ Complete PRD with scope, requirements, constraints
→ Implementation tasks broken down by priority
→ Ready for AI coding assistant execution
```

### 2. Project Kickoff & Documentation

Perfect for starting new projects or features:
- **MVP Planning** → Define scope and requirements clearly
- **Technical Specifications** → Document architecture and decisions
- **Task Breakdown** → Generate actionable implementation steps
- **Team Alignment** → Share clear, structured documentation

### 3. Prompt Optimization for AI Assistants

Enhance your interactions with AI coding tools:
```bash
# Quick optimization
/clavix:fast "add dark mode to dashboard"

# Deep analysis with comprehensive refinement
/clavix:deep "build real-time collaborative editing"

# Full PRD workflow
/clavix:prd
```

### 4. Implementation Progress Tracking

Built-in task management (v2.8+):
```bash
# List all tasks from PRD
clavix tasks list

# Mark task complete with auto-commit
clavix task-complete <taskId>

# View progress across project
clavix tasks status
```

## 💡 Key Features

### 1. Dual Optimization Modes

- **Fast Mode** → Quick refinement for immediate use
- **Deep Mode** → Comprehensive analysis and restructuring

Both modes automatically save outputs to `.clavix/outputs/prompts/` for version control and review.

### 2. PRD Generation Engine

Complete Product Requirements Documents include:
- **Executive Summary** → High-level overview
- **Scope Definition** → What's in and out of scope
- **Technical Requirements** → Detailed specifications
- **Implementation Tasks** → Ready-to-execute checklist
- **Acceptance Criteria** → Clear success metrics

### 3. Task Management System

Track implementation progress seamlessly:
- **Task Generation** → Auto-create tasks from PRDs
- **Progress Tracking** → Monitor completion status
- **Auto-Commit** → Generate commits when marking tasks complete
- **Status Updates** → Real-time view of project progress

### 4. Prompt Lifecycle Management (v2.7+)

Intelligent prompt storage and hygiene:
- **Status Tracking** → NEW → EXECUTED → STALE
- **Age Warnings** → >7 days = OLD, >30 days = STALE
- **Organized Storage** → Structured in `.clavix/outputs/prompts/`
- **Easy Retrieval** → List, view, and execute saved prompts

### 5. Universal AI Agent Integration

Works seamlessly with 15+ coding assistants:
- **Claude Code** (via slash commands)
- **Cursor** (built-in support)
- **Windsurf** (native integration)
- **Droid CLI** (custom instructions)
- **Any AI agent** supporting slash commands or file-based instructions

## 🔧 Practical Implementation

### Installation & Setup

```bash
# Install globally
npm install -g clavix

# Initialize in your project
clavix init
```

**Requirements:** Node.js ≥ 16.0.0 (ESM support)

### Quick Start Workflow

1. **Generate PRD**
   ```bash
   /clavix:prd
   # Or via CLI: clavix prd
   ```

2. **Review & Refine**
   - Open generated PRD in `.clavix/outputs/`
   - Edit as needed to match your requirements
   - Share with team for alignment

3. **Generate Implementation Tasks**
   ```bash
   clavix tasks generate
   ```

4. **Execute with AI Assistant**
   ```bash
   # View saved prompts
   clavix prompts list

   # Execute optimized prompt
   /clavix:execute
   ```

5. **Track Progress**
   ```bash
   # Mark tasks complete (auto-commits)
   clavix task-complete <taskId>

   # View status
   clavix tasks status
   ```

### Slash Commands

For supported AI agents (Claude Code, Cursor, Windsurf):
- `/clavix:fast "description"` — Quick optimization
- `/clavix:deep "description"` — Comprehensive analysis
- `/clavix:prd` — Full PRD workflow
- `/clavix:execute` — Run saved prompts

### Best Practices

1. **Start with Deep Mode for Complex Features**
   - Use `/clavix:deep` for new features or major changes
   - Let CLEAR framework identify edge cases and requirements
   - Review and refine before execution

2. **Leverage PRD Generation**
   - Generate PRDs at project start for alignment
   - Use as living documentation during development
   - Update PRD as requirements evolve

3. **Maintain Task Hygiene**
   - Mark tasks complete as you finish them
   - Use auto-commit feature for consistent history
   - Review task status regularly

4. **Version Control Your .clavix Directory**
   - Track PRDs and prompts alongside code
   - Share optimizations across team
   - Maintain project history and decisions

## 🎭 Real-World Example

**Input:** "I want to build a real-time notification system"

**Clavix Fast Mode:**
```
Optimized Prompt:
"Design and implement a real-time notification system with:
- WebSocket connection management
- User preference handling
- Notification persistence
- Rate limiting and priority queuing
- Cross-device synchronization
Include error handling, reconnection logic, and offline queue."
```

**Clavix PRD Mode:**
```
Generated PRD includes:
- Executive Summary
- Technical Architecture (WebSocket, Redis, Database)
- User Stories (15 scenarios)
- Implementation Tasks (23 tasks across 4 phases)
- Success Metrics
- Security Considerations

Ready-to-implement tasks:
1. Set up WebSocket server infrastructure
2. Implement connection manager with reconnect logic
3. Design notification data model
4. Build user preference service
... (and 19 more detailed tasks)
```

## 🆚 Why Clavix Over Alternatives

### vs. OpenSpec CLI
- **Faster** → CLEAR optimization is near-instantaneous
- **Simpler** → No complex CLI commands to memorize
- **Integrated** → Works natively with 15+ AI agents
- **Task Management** → Built-in progress tracking
- **Free & Open Source** → No licensing costs

### vs. Manual Prompting
- **Consistency** → CLEAR framework ensures quality
- **Completeness** → Never miss edge cases or requirements
- **Efficiency** → Generate PRDs in minutes, not hours
- **Best Practices** → Validated methodology built-in

### vs. Traditional PRD Tools
- **AI-Native** → Designed for AI assistant workflows
- **Executable** → PRDs become implementation tasks automatically
- **Integrated** → No context switching between tools
- **Version Controlled** → Markdown files in your repo

## 🎯 Bottom Line

Clavix transforms the way you plan and execute development work by combining academic rigor (CLEAR framework) with practical implementation (PRDs + task lists). Instead of struggling with vague prompts or spending hours writing specifications, you get optimized, actionable documentation that seamlessly integrates with your AI coding workflow. The result: faster planning, clearer requirements, and more reliable implementation—all while maintaining the natural, conversational vibecoding experience.

**Official Resources:**
- [GitHub Repository](https://github.com/ClavixDev/Clavix)
- [Documentation](https://github.com/ClavixDev/Clavix/tree/main/docs)

See also: [Droid CLI](./droid-cli.md), [Claude Code CLI](./claude-code-cli.md), [Mastering AI Prompts](../../prompting/README.md)

Back: [Tools & Tech Stack](../README.md)
