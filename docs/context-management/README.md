# Context Management 🧠

**TL;DR:** Conversation is ephemeral, files are forever. Externalize knowledge to .md files early and often. Keep conversations small and focused. Use MCP servers for external data retrieval.

---

## Table of Contents

1. [Foundation](#foundation)
2. [Core Principles](#core-principles)
3. [Agent-Specific Strategies](#agent-specific-strategies)
4. [The .md-Based Workflow Pattern](#the-md-based-workflow-pattern)
5. [Context Management by Task Type](#context-management-by-task-type)
6. [Techniques & Patterns](#techniques--patterns)
7. [File Organization](#file-organization-for-context-management)
8. [Advanced Strategies](#advanced-strategies)
9. [Monitoring & Troubleshooting](#monitoring--troubleshooting)
10. [MCP Servers](#mcp-servers-for-context-management)
11. [Best Practices Checklist](#best-practices-checklist)
12. [Real-World Scenarios](#real-world-scenarios)

---

## Foundation

### Context as Resource Management

Think of context like RAM or budget:
- **Limited capacity** - Every model has a context window limit
- **Performance impact** - More context = slower responses, higher costs
- **Degrades when full** - AI quality drops near limits
- **Must be managed deliberately** - Not automatic

**The golden rule:** Context is your most valuable resource in Vibecoding. Manage it like you manage memory in performance-critical systems.

### The Markdown Memory Pattern ⭐

**Core insight:** What lives in .md files doesn't consume your conversation context.

Traditional approach:
```
Conversation: Plan → Discuss → Implement → Explain → Debug → Repeat
Context used: 200k tokens (hitting limits)
```

Markdown-based approach:
```
Write plan.md → Conversation: "Implement plan.md" → Update plan.md
Context used: 20k tokens (90% savings)
```

**Why .md files are superior:**
- ✅ Persistent across sessions
- ✅ Version controlled (git)
- ✅ Human-editable
- ✅ Agent can reference without re-reading conversation
- ✅ Multiple agents can share the same knowledge
- ✅ Zero context cost after initial read

**Examples in the wild:**
- **openspec tool**: Writes feature proposals to .md files
- **droid CLI**: Plan mode → creates .md → Act mode reads it
- **Claude Code**: Plan mode can output to .md before execution
- **All agents**: Can read/write .md for persistent memory

### The Context Hierarchy

Not all context is equal. Organize by access pattern:

| Level | What | Where | Cost |
|-------|------|-------|------|
| **Active** | Current work | Conversation | High (in RAM) |
| **Retrievable** | Project knowledge | .md files in docs/ | Low (read on demand) |
| **External** | Framework docs, APIs | MCP servers | Zero (pulled as needed) |

**Decision tree:**
```
Is this needed right now for current task?
├─ YES → Keep in conversation (active context)
└─ NO → Is it project-specific knowledge?
    ├─ YES → Write to .md file (retrievable context)
    └─ NO → Use MCP server (external context)
```

### Mental Models

**How agents process context:**

1. **Recency bias** - Recent messages have more weight
2. **Attention limits** - Can't equally focus on all context
3. **Pattern matching** - Looks for relevant chunks
4. **Completion pressure** - Near token limit = rushed responses

**What this means for you:**
- Put critical info near the end of context
- Remove irrelevant files/messages
- Structure information clearly
- Don't hit 100% of context window

---

## Core Principles

### 1. Externalize, Don't Memorize

**Bad pattern:**
```
You: "Remember we decided to use PostgreSQL with UUID primary keys"
Agent: "Got it, I'll remember that"
[200 messages later]
Agent: *Suggests integer IDs*
```

**Good pattern:**
```
You: "Document this in docs/decisions/database.md"
Agent: *Writes decision to file*
[200 messages later]
You: "Check docs/decisions/database.md"
Agent: *Reads file, follows decision*
```

### 2. Strategic vs. Tactical Context

**Strategic** (belongs in .md files):
- Architecture decisions
- Project conventions
- Feature specifications
- API designs
- Long-term plans

**Tactical** (belongs in conversation):
- Current implementation details
- Immediate debugging steps
- Quick clarifications
- Active file edits

### 3. Quality Over Quantity

**Don't:**
- Include entire src/ folder "just in case"
- Add all tests when implementing a feature
- Keep old conversation threads active

**Do:**
- Include only files directly relevant to current task
- Add test files only when writing tests
- Compress or externalize completed work

### 4. Context Debt

Like technical debt, context debt accumulates:

**Signs of context debt:**
- Agent forgets recent decisions
- Repeated questions
- Contradictory suggestions
- Slower response times

**How to pay it down:**
- Externalize to .md files
- Start new session with summary
- Remove completed work from context
- Clean up redundant messages

### 5. The 60-85% Rule

**Context window strategy:**

- **0-60%**: Optimal zone - agent is "smart" and thorough
- **60-85%**: Working zone - usable but monitor closely
- **85-95%**: Danger zone - quality degrades, start compressing
- **95-100%**: Red zone - agent rushes to finish, makes mistakes

**Pro tip:** If you have 1M context window (Claude Sonnet 4.5, Qwen3 Coder), you can fill it more but plan to compress around ~200k. This prevents "end-of-context" pressure.

**Practice:**
```
Check your context usage regularly:
- Claude Code: Monitor token count in UI
- Windsurf: Check cascade context indicator
- Zed: Automatic compression triggers
- API usage: Track via provider dashboard
```

---

## Agent-Specific Strategies

### Claude Code

**Best practices:**

1. **Use TodoWrite proactively**
   - Break work into trackable tasks
   - Helps agent maintain focus
   - You can see progress in real-time

2. **Leverage Task agents**
   - Use Explore agent for codebase understanding
   - Offload research to background agents
   - Parallel exploration when possible

3. **Plan Mode workflow**
   ```
   1. Enter plan mode
   2. Discuss approach
   3. Write plan to docs/plans/feature-name.md
   4. Exit plan mode
   5. Execute: "Implement docs/plans/feature-name.md"
   ```

4. **Parallel tool calls**
   - Claude Code can read multiple files simultaneously
   - Request multiple independent file reads in one message
   - Saves round-trip time and context

5. **Reference format**
   - Use `file_path:line_number` for precise references
   - Agent can jump directly to relevant code
   - Example: "Check auth.ts:145 for the issue"

### Windsurf

**Context management with Cascade:**

1. **Flows for repeated patterns**
   - Document common workflows
   - Cascade references flow instead of re-explaining
   - Saves context on repetitive tasks

2. **Documentation patterns**
   - Keep architecture docs in docs/
   - Cascade can pull relevant docs on demand
   - Update docs as project evolves

### Zed

**Auto-compression features:**

1. **Automatic summarization**
   - When context fills → Zed creates summary
   - Dialog compresses automatically
   - Essential context preserved
   - Continue without manual reset

2. **Workflows**
   - Define reusable workflows
   - Reference instead of re-explaining
   - Reduces conversation overhead

### Droid CLI

**The plan/act split pattern:**

```bash
# Planning mode - creates strategy
droid plan "Implement user authentication"
# Output: .tasks/auth-feature.md

# Act mode - executes from plan
droid act .tasks/auth-feature.md
# Agent reads plan, implements step by step
```

**Why this works:**
- Planning uses context to create comprehensive plan
- Plan gets written to .md file
- Act mode reads plan (small context cost)
- Can resume/restart without re-planning
- Multiple execution attempts from same plan

### General IDE Agents

**Universal patterns:**

1. **Start with .cursorrules or .clauderules**
   - Project-wide instructions
   - Loaded automatically
   - Don't repeat yourself in every conversation

2. **Keep active file count low**
   - Most agents track "open" or "included" files
   - Close files when done with them
   - Re-open when needed (reading is cheap)

3. **Use comments for persistence**
   - Add TODOs in code for future work
   - Agent can grep for TODOs
   - Better than remembering in conversation

---

## The .md-Based Workflow Pattern

### Planning Phase

**Step 1: Create comprehensive plan**

Use planning tools or manual writing:
```
Options:
- openspec tool → generates proposal.md
- droid CLI → plan mode creates .tasks/*.md
- Claude Code → plan mode, then save to .md
- Manual → write docs/plans/feature.md yourself
```

**Step 2: Structure your plan**

Template structure:
```markdown
# Feature: [Name]

## Problem
What are we solving?

## Approach
How will we solve it?

## Tasks
- [ ] Task 1
- [ ] Task 2
- [ ] Task 3

## Success Criteria
How do we know it's done?

## Technical Decisions
- Decision 1: ...
- Decision 2: ...
```

**Step 3: Save to appropriate location**

```
docs/
├── plans/           # Feature plans (openspec output)
├── proposals/       # Design proposals
├── decisions/       # ADRs (Architecture Decision Records)
└── tasks/           # Active work breakdown
```

### Execution Phase

**Step 1: Reference the plan**

Instead of:
```
You: "Implement user auth with JWT tokens, refresh tokens, role-based
access control, password hashing with bcrypt, email verification, and..."
[Uses 500 tokens]
```

Do this:
```
You: "Implement docs/plans/auth.md"
[Uses 10 tokens, agent reads plan which uses 50 tokens]
Total: 60 tokens vs 500 tokens
```

**Step 2: Agent reads and executes**

Agent workflow:
1. Read plan.md (one-time cost)
2. Execute task 1
3. Refer back to plan if needed (cheap read)
4. Execute task 2
5. Update plan.md with progress
6. Continue...

**Step 3: Update as you go**

```markdown
## Tasks
- [x] Task 1 ✅
- [x] Task 2 ✅
- [ ] Task 3 🔄 In progress
- [ ] Task 4

## Notes
- Task 2: Had to use bcrypt instead of argon2 (dependency issue)
- Task 3: Discovered we need migration for user table
```

### Benefits

**1. Session persistence**
```
Day 1: Plan feature → implement 50%
[Close laptop]
Day 2: "Continue docs/plans/feature.md" → picks up where you left off
```

**2. Multiple agents, same plan**
```
Agent 1: Implement backend (reads plan)
Agent 2: Implement frontend (reads same plan)
Both aligned without synchronization overhead
```

**3. Version control**
```bash
git log docs/plans/auth.md
# See evolution of plan
git diff docs/plans/auth.md
# Review changes to approach
```

**4. Human oversight**
```
Agent: "I've created docs/plans/refactor.md for review"
You: *Read, edit, improve*
Agent: "Implement updated docs/plans/refactor.md"
```

**5. Zero context cost scaling**
```
Small feature: Plan = 100 tokens in .md, reference 10 times = 100 tokens total
Large feature: Plan = 2000 tokens in .md, reference 10 times = 2000 tokens total
Same cost whether you reference once or 100 times!
```

### Tools That Support This

| Tool | How It Uses .md |
|------|----------------|
| **openspec** | Generates proposals in .md format |
| **droid CLI** | Plan mode → .md → Act mode |
| **Claude Code** | Manual .md writing, plan mode output |
| **Windsurf** | Cascade references documentation |
| **Zed** | Workflow definitions in files |
| **All agents** | Can read/write .md files |

---

## Context Management by Task Type

### Feature Development

**Approach: Write-first workflow**

```
1. Write feature spec to docs/plans/feature-name.md
2. Break into subtasks in the .md
3. Conversation: "Implement docs/plans/feature-name.md"
4. Update .md as you progress
5. Document decisions in docs/decisions/ if architectural
```

**Context usage:**
- Spec: ~500 tokens (one-time read)
- Implementation conversations: ~5k tokens per subtask
- Total: ~20k tokens for large feature

vs. traditional approach: ~150k tokens

### Debugging

**Approach: Narrow and focused**

```
1. Minimal context: error message + relevant file
2. Don't include entire codebase
3. Add files incrementally as needed
4. Document solution in docs/fixes/ if non-obvious
```

**Example:**
```
Bad:  Include all files, full logs, entire stack trace
Good: Error message + auth.ts + minimal stack trace
      Add more files only if needed
```

### Refactoring

**Approach: Document architecture first**

```
1. Write docs/decisions/refactor-rationale.md
   - Current state
   - Problems
   - Proposed solution
   - Migration plan
2. Conversation: "Execute refactor per docs/decisions/..."
3. Update .md with actual changes made
```

**Why this matters:**
- Refactoring decisions need to be persistent
- Future you/agents need to understand why
- Easy to pause/resume large refactors

### Code Review

**Approach: Checklist-driven**

```
1. Create docs/reviews/pr-123.md with checklist
2. Agent reviews code against checklist
3. Findings written to the .md
4. Conversation stays focused on current file
```

**Benefits:**
- Review criteria is consistent
- Findings are documented
- Can review large PRs in multiple sessions

### Documentation

**Approach: Knowledge preservation**

```
As you build:
- docs/architecture/ ← system design
- docs/guides/ ← how-tos
- docs/decisions/ ← ADRs
- docs/api/ ← API documentation

Agent references these instead of asking you to explain
```

---

## Techniques & Patterns

### 1. Selective File Inclusion

**Modular structure:**

```
project/
├── src/
│   ├── components/   # Only when working with UI
│   ├── api/          # Only when working on backend
│   ├── utils/        # Only when tools are needed
│   └── database/     # Only when working with DB
```

**Practice:**
- Add only relevant folders to the prompt
- Don't let AI scan the entire codebase every time
- You know best what's needed—not AI

**Example conversation:**
```
Bad:  "Here's my entire src/ folder [includes everything]"
Good: "Working on user auth. Including src/api/auth.ts and src/database/users.ts"
```

### 2. MCP as Context Savings

**The problem:**
Without MCP, you manually fetch and paste external data into conversation.

**Example without MCP:**
```
You: *Copy-paste React docs about useEffect*
    *Copy-paste Stack Overflow answers*
    *Paste API response from Postman*
    "Here's the context, now help me debug"
[Uses 5000 tokens just for context]
```

**Example with MCP:**
```
You: "Use Context7 MCP to check React useEffect best practices,
     then use DevTools MCP to find the error"
Agent: *Retrieves data via MCP, analyzes, fixes*
[Uses 500 tokens, 90% savings]
```

**Key MCPs for context savings:**

| MCP | Saves Context By |
|-----|-----------------|
| **Context7** | Retrieving framework/library docs instead of pasting |
| **DevTools** | Reading browser console/network instead of screenshots |
| **Database** | Querying DB directly instead of manual exports |
| **API clients** | Fetching API data instead of copy-paste |
| **Filesystem** | Reading logs/files without manual inclusion |

**Best practice:**
- Use MCPs for external data retrieval
- Don't run too many MCPs simultaneously (adds overhead)
- Know when MCP helps vs. when manual is faster

### 3. Dialog Compression

**When conversation gets long:**

**Option 1: Automatic (Zed)**
- Agent creates summary when context fills
- Dialog compressed automatically
- Continue seamlessly

**Option 2: Manual externalization (Better)**
```
You: "Write a summary of what we've done to docs/context/session-summary.md"
Agent: *Writes summary*
You: "Start new conversation, read docs/context/session-summary.md to continue"
[New session with minimal context]
```

**Option 3: Manual compression**
- Periodically ask agent to summarize
- Start fresh conversation with summary
- Don't trust tools to manage this automatically

**Pro tip:** Externalize to .md instead of compressing when possible. Compression loses detail; files keep everything.

### 4. Avoiding Bloat

**Don't:**
- ❌ Add `node_modules` to context
- ❌ Include all files "just in case"
- ❌ Repeat the same instructions multiple times
- ❌ Run too many MCP servers at once
- ❌ Keep completed work in active conversation
- ❌ Paste entire log files

**Do:**
- ✅ Include only relevant files
- ✅ Use `.cursorrules` or `.clauderules` for persistent instructions
- ✅ Use MCPs for external data
- ✅ Favor modular architecture
- ✅ Externalize completed work to .md files
- ✅ Grep logs for errors, include only relevant lines

### 5. Context Priming

**Start sessions effectively:**

**Good session start:**
```
You: "Read docs/architecture/overview.md and docs/context/last-session.md,
     then continue implementing docs/plans/auth-feature.md"

Agent: *Reads 3 small files, has full context, starts work*
[Total context: ~1000 tokens]
```

**Bad session start:**
```
You: "So we're building this auth system, remember we talked about JWT,
     and there was that thing with refresh tokens, and we need to handle
     role-based access, and we discussed bcrypt vs argon2..."

Agent: "I don't have previous context, can you provide details?"
[Repeat everything, use 5000+ tokens]
```

### 6. Semantic Chunking

**Organize information for AI comprehension:**

**Bad .md structure:**
```markdown
# Feature
Everything in one giant paragraph with implementation details mixed
with architecture decisions mixed with TODOs mixed with notes...
```

**Good .md structure:**
```markdown
# Feature Name

## Overview
[High-level summary]

## Architecture
[Design decisions]

## Implementation Tasks
- [ ] Task 1
- [ ] Task 2

## Technical Notes
- Note 1
- Note 2

## References
- Link 1
- Link 2
```

**Why this matters:**
- Agent can scan headings to find relevant sections
- Can read only what's needed for current task
- Clear structure = better comprehension

### 7. Task Decomposition

**Large task → many small tasks**

**Example: "Build user authentication"**

Bad approach:
```
Conversation: Implement entire auth system
[Overwhelms context with all files, all decisions, all edge cases]
```

Good approach:
```
docs/plans/auth.md:
  - [ ] Database schema
  - [ ] Password hashing
  - [ ] JWT generation
  - [ ] Refresh tokens
  - [ ] Middleware
  - [ ] Tests

Conversation 1: "Implement task 1 from docs/plans/auth.md"
Conversation 2: "Implement task 2 from docs/plans/auth.md"
...
```

**Benefits:**
- Each conversation stays small
- Clear progress tracking
- Easy to pause/resume
- Can parallelize with multiple agents

### 8. Multi-file Workflows

**Working across large codebases:**

**Strategy: Progressive context loading**

```
Phase 1: Architecture understanding
- Read docs/architecture/overview.md
- Read high-level structure files only

Phase 2: Focused implementation
- Load only files for current feature
- Keep architecture .md in context for reference

Phase 3: Integration
- Load interface files
- Keep implementation details external

Phase 4: Testing
- Load test files + minimal implementation
- Reference implementation via file paths
```

**Example workflow:**
```
You: "Read docs/architecture/api-design.md, then implement
     POST /users endpoint per docs/api/endpoints.md"

Agent:
1. Reads architecture (200 tokens)
2. Reads endpoint spec (300 tokens)
3. Loads src/api/users.ts (500 tokens)
4. Implements
[Total: ~1000 tokens vs. loading entire API codebase: ~50k tokens]
```

### 9. Documentation-Driven Development

**Use docs/ as agent memory:**

**Pattern:**
```
Before coding:
1. Write docs/architecture/design.md
2. Write docs/api/endpoints.md
3. Write docs/database/schema.md

During coding:
- Agent references these docs
- No need to explain architecture repeatedly
- Decisions are preserved

After coding:
- Update docs with actual implementation
- Add docs/guides/how-to-X.md for future reference
```

**This creates a virtuous cycle:**
```
Good docs → Less context needed → Faster development → Better docs
```

---

## File Organization for Context Management

### Recommended Structure

```
project/
├── docs/
│   ├── architecture/          # System design, patterns
│   │   ├── overview.md
│   │   ├── api-design.md
│   │   └── database-design.md
│   │
│   ├── plans/                 # Feature plans (openspec output)
│   │   ├── auth-feature.md
│   │   └── payment-integration.md
│   │
│   ├── proposals/             # Design proposals for review
│   │   └── refactor-proposal.md
│   │
│   ├── decisions/             # ADRs (Architecture Decision Records)
│   │   ├── 001-database-choice.md
│   │   └── 002-auth-strategy.md
│   │
│   ├── context/               # Session summaries, handoffs
│   │   ├── 2024-01-session.md
│   │   └── current-state.md
│   │
│   ├── guides/                # How-tos, runbooks
│   │   ├── setup.md
│   │   └── deployment.md
│   │
│   └── api/                   # API documentation
│       └── endpoints.md
│
├── .tasks/                    # Active task breakdowns (droid style)
│   └── current-sprint.md
│
├── .cursorrules               # Or .clauderules, persistent instructions
│
└── src/                       # Actual code
    └── ...
```

### Why This Structure Works

**1. Clear separation of concerns**
- Architecture → strategic decisions
- Plans → tactical execution
- Context → session continuity
- Guides → operational knowledge

**2. Easy for agents to navigate**
```
Agent needs architecture info → reads docs/architecture/
Agent needs task list → reads docs/plans/ or .tasks/
Agent needs past context → reads docs/context/
```

**3. Scales with project growth**
- Start with minimal docs/
- Add directories as needed
- Never bloats conversation context

**4. Git-friendly**
- All documentation versioned
- Can see decision evolution
- Easy to rollback bad docs

### File Naming Conventions

**Use descriptive, action-oriented names:**

```
Good:
- docs/plans/user-authentication-feature.md
- docs/decisions/001-why-postgresql.md
- docs/context/2024-01-15-auth-implementation.md

Bad:
- docs/stuff.md
- docs/notes.md
- docs/temp.md
```

**For numbered sequences (ADRs):**
```
docs/decisions/
├── 001-database-choice.md
├── 002-api-framework.md
└── 003-deployment-strategy.md
```

**For date-based entries:**
```
docs/context/
├── 2024-01-session.md
├── 2024-02-session.md
└── current-state.md  # ← Always current state
```

---

## Advanced Strategies

### 1. Context Refresh Patterns

**Decision matrix: When to reset vs compress vs externalize**

```
Is conversation quality degrading?
├─ YES → Are there important decisions/context to preserve?
│   ├─ YES → Externalize to .md, start fresh
│   └─ NO → Start completely fresh session
│
└─ NO → Is context > 80% full?
    ├─ YES → Externalize future work to .md, continue with current task
    └─ NO → Continue as-is
```

**Patterns:**

**Pattern 1: Externalize and continue**
```
You: "Write summary of our architecture decisions to docs/decisions/api-design.md"
Agent: *Writes file*
You: [Continue in same session, reference .md instead of conversation]
```

**Pattern 2: Session handoff**
```
You: "Write complete session summary to docs/context/session-1.md including
     what we built, decisions made, and next steps"
Agent: *Writes comprehensive summary*
[Start new session]
You: "Read docs/context/session-1.md and continue with next steps"
```

**Pattern 3: Hard reset**
```
When: Exploratory work done, ready for clean implementation
You: [Start new session]
You: "Implement docs/plans/feature.md"
[No historical context needed]
```

### 2. Progressive Context Loading

**Start small, expand as needed**

**Anti-pattern:**
```
Session start: Include all potentially relevant files (50+ files)
Result: Context bloated from the start
```

**Better pattern:**
```
Session start: Include only architecture overview + current task
Step 1: Implement feature → load 3-5 relevant files
Step 2: Need integration → load interface files
Step 3: Need testing → load test utilities
Result: Context grows organically, stays minimal
```

**Example:**
```
You: "Read docs/architecture/overview.md. We're implementing user auth."
Agent: "Got it. What's first?"
You: "Create JWT token generation. Include src/utils/crypto.ts"
[Loads 1 file]
Agent: *Implements*
You: "Now integrate with src/api/auth.ts"
[Loads 1 more file]
...
```

### 3. Context Checkpointing

**Save state at key milestones**

**When to checkpoint:**
- ✅ After completing major feature
- ✅ Before starting risky refactor
- ✅ When switching context (frontend → backend)
- ✅ End of work session
- ✅ After important decisions

**How to checkpoint:**
```
You: "Checkpoint current state:
     1. Write what we've completed to docs/context/checkpoint-auth.md
     2. Write remaining tasks to docs/plans/auth-remaining.md
     3. Write any important decisions to docs/decisions/"

Agent: *Creates checkpoint files*
```

**Recovery from checkpoint:**
```
[Days/weeks later]
You: "Read docs/context/checkpoint-auth.md and continue with
     docs/plans/auth-remaining.md"
Agent: *Picks up exactly where you left off*
```

### 4. Session Handoffs

**Multi-agent or multi-session continuity**

**Handoff template (docs/context/handoff.md):**
```markdown
# Session Handoff - [Date]

## What Was Done
- Implemented X
- Fixed bug Y
- Decided on approach Z

## Current State
- Feature X: 80% complete
- Remaining: Task A, Task B
- Blocked on: Decision about C

## Important Context
- We're using PostgreSQL (see docs/decisions/001-database.md)
- Auth flow documented in docs/architecture/auth.md
- API design in docs/api/endpoints.md

## Next Steps
1. Complete Task A (see docs/plans/feature.md line 45)
2. Review PR for Task B
3. Make decision about C

## Files In Progress
- src/api/auth.ts (main implementation)
- src/database/users.ts (schema)
- tests/auth.test.ts (70% test coverage)
```

**Usage:**
```
You: "Create handoff document"
Agent: *Writes docs/context/handoff.md*

[New session or different agent]
You: "Read docs/context/handoff.md and continue"
Agent: *Fully contextualized, continues work*
```

### 5. Living Documentation

**Keep docs/ as single source of truth**

**The pattern:**
```
Code changes → Update docs
Architectural decisions → Update docs
New patterns emerge → Document in docs
Bug fixes with learnings → Update docs
```

**Why this matters:**
- Agents always have accurate information
- No drift between code and documentation
- Future sessions start with correct context
- Team members can onboard from docs/

**Example workflow:**
```
You: "After implementing this feature, update docs/architecture/api-design.md
     with the actual implementation details"

Agent:
1. Implements feature
2. Updates documentation to match reality
3. Commits both code and docs

Result: Documentation always reflects current state
```

---

## Monitoring & Troubleshooting

### Signs of Context Trouble

**Quality degradation:**
- ❌ Agent forgets recent decisions
- ❌ Contradictory suggestions
- ❌ Asking you to repeat information
- ❌ Implementing features that don't align with architecture
- ❌ Repetitive mistakes
- ❌ Generic advice instead of project-specific

**Performance issues:**
- ❌ Slower response times
- ❌ Incomplete responses that cut off
- ❌ "Rush to finish" behavior
- ❌ Skipping error handling or edge cases

**Context management failures:**
- ❌ Agent says "I don't have enough context"
- ❌ Repeatedly reading the same files
- ❌ Asking about project structure you've explained
- ❌ Missing obvious connections between files

### Diagnostic Questions

**When quality drops, ask yourself:**

1. **How full is my context window?**
   - Check token usage in your tool
   - If > 85%, time to act

2. **Am I repeating myself?**
   - If yes → externalize to .md
   - Create docs/decisions/ or .cursorrules

3. **Are there too many files in context?**
   - Review included files
   - Remove completed/irrelevant files
   - Keep only what's needed for current task

4. **Is the conversation too long?**
   - Consider session handoff
   - Externalize completed work
   - Start fresh with summary

5. **Am I using the right tool for the job?**
   - Should I be using an MCP server?
   - Should this be in a .md file?
   - Should I start a new specialized session?

### Recovery Strategies

**Strategy 1: Immediate externalization**
```
Problem: Agent forgets architectural decision
Solution: "Document our architecture decision to docs/decisions/api-design.md
          and reference it instead of me explaining again"
```

**Strategy 2: Context cleanup**
```
Problem: Too many files in context
Solution: "Remove all files. Now include only src/api/auth.ts and
          docs/architecture/auth.md for current task"
```

**Strategy 3: Session reset with handoff**
```
Problem: Conversation too long, quality degraded
Solution:
1. "Write session summary to docs/context/handoff.md"
2. Start new session
3. "Read docs/context/handoff.md and continue"
```

**Strategy 4: Plan-based reset**
```
Problem: Lost track of overall goals
Solution:
1. "Write implementation plan to docs/plans/feature.md based on what we've discussed"
2. Start new session
3. "Implement docs/plans/feature.md"
```

**Strategy 5: Compression (last resort)**
```
Problem: Can't start new session, need continuity
Solution: "Summarize our conversation: what we've built, current state, next steps.
          Keep it under 500 words"
[Use summary to continue or start fresh]
```

### Prevention Tactics

**Proactive context management:**

1. **Start with .md files**
   - Write plans before implementing
   - Document architecture upfront
   - Create .cursorrules for project conventions

2. **Regular checkpoints**
   - After each major feature
   - At end of work sessions
   - Before context gets > 70% full

3. **Ruthless relevance**
   - Include only what's needed now
   - Remove files when tasks complete
   - Don't keep "just in case" context

4. **Use the right tools**
   - MCP servers for external data
   - Task agents for exploration
   - New sessions for new features

5. **Monitor metrics**
   - Token usage
   - Response quality
   - Time to completion
   - Agent confusion frequency

**Set up alerts for yourself:**
```
When context > 60%: Review included files
When context > 75%: Plan to externalize or reset
When context > 85%: Immediate action required
```

---

## MCP Servers for Context Management

### Understanding MCP's Role

**MCP servers retrieve external data so you don't have to manually paste it into conversation.**

**The context savings equation:**
```
Without MCP:
1. You manually fetch data (browser, API, database)
2. Copy-paste into conversation
3. Agent processes
Cost: Your time + context tokens

With MCP:
1. Agent fetches data via MCP
2. Agent processes
Cost: Only processing tokens (often smaller)
```

### External Data Retrieval MCPs

**1. Context7 MCP**
- **Purpose:** Framework/library documentation
- **Example:**
  ```
  Without: Copy-paste React docs about useEffect
  With:    "Use Context7 to check React useEffect patterns"
  ```
- **Savings:** 2000+ tokens per documentation reference

**2. DevTools MCP**
- **Purpose:** Browser debugging data
- **Example:**
  ```
  Without: Screenshot console, paste errors, describe network tab
  With:    "Use DevTools MCP to analyze the error"
  ```
- **Savings:** 3000+ tokens per debugging session

**3. Database MCPs**
- **Purpose:** Query database directly
- **Example:**
  ```
  Without: Run query, export CSV, paste into conversation
  With:    "Query users table via MCP to analyze the data"
  ```
- **Savings:** 1000+ tokens per query result

**4. API Client MCPs**
- **Purpose:** Fetch from external APIs
- **Example:**
  ```
  Without: Use Postman, copy response, paste into conversation
  With:    "Fetch /api/users via MCP and analyze response"
  ```
- **Savings:** 500+ tokens per API call

**5. Filesystem MCPs**
- **Purpose:** Read logs, config files
- **Example:**
  ```
  Without: Copy entire log file into conversation
  With:    "Use filesystem MCP to grep error.log for 'FATAL'"
  ```
- **Savings:** 5000+ tokens for large log files

### When to Use MCP

**Use MCP when:**
- ✅ You need external framework/library documentation
- ✅ You need to debug browser console/network
- ✅ You need to query database for analysis
- ✅ You need to fetch from external APIs
- ✅ You need to read large log files selectively

**Don't use MCP when:**
- ❌ Information is already in your codebase (use file reads)
- ❌ Simple one-time lookup (manual might be faster)
- ❌ MCP server is slow/unreliable (manual might be better)
- ❌ You're running too many MCPs (overhead adds up)

### Best Practices

**1. Don't over-rely on MCPs**
```
Bad:  Run 10 different MCP servers simultaneously
Good: Use 2-3 most relevant MCPs
```

**2. Know what each MCP does**
```
Context7: External docs, not your project docs
DevTools: Browser data, not server logs
Database: Direct queries, not file-based DBs
```

**3. Combine with .md files**
```
You: "Use Context7 to research best practices, then write
     proposal to docs/proposals/api-design.md"

Agent:
1. Fetches external knowledge via MCP
2. Writes proposal to .md file
3. Future sessions reference .md, not MCP again
```

**4. Use for exploration, externalize findings**
```
Exploration phase:
- Use MCPs to gather information
- Agent synthesizes findings

Documentation phase:
- Write findings to docs/research/topic.md
- Future reference from .md, not MCP
```

### Common MCP Anti-Patterns

**Anti-pattern 1: Using MCP for project docs**
```
Bad:  "Use Context7 to understand our API design"
Good: "Read docs/architecture/api-design.md"
```
Context7 is for React/Vue/etc docs, not your project!

**Anti-pattern 2: Over-reliance**
```
Bad:  Every question → MCP lookup
Good: Create docs/ with common knowledge, MCP for edge cases
```

**Anti-pattern 3: Wrong tool**
```
Bad:  Use filesystem MCP to read src/api/auth.ts
Good: Just read the file directly (faster, simpler)
```

MCPs have overhead; direct file reads are better for project files.

---

## Best Practices Checklist

### Before Starting Work

- [ ] **Write a plan/proposal to .md**
  - Use openspec, droid plan, or manual writing
  - Structure: problem → approach → tasks
  - Save to docs/plans/ or docs/proposals/

- [ ] **Set up docs/ structure if needed**
  - Create docs/architecture/ for design decisions
  - Create docs/context/ for session continuity
  - Create docs/decisions/ for ADRs

- [ ] **Review relevant existing .md files**
  - Read docs/architecture/overview.md
  - Read docs/context/current-state.md
  - Read relevant docs/decisions/*.md

- [ ] **Check .cursorrules / .clauderules**
  - Project conventions documented
  - Common instructions not repeated per session
  - Update if needed

- [ ] **Start with minimal context**
  - Include only files for immediate task
  - Reference .md files for background info
  - Plan to load more files progressively

### During Work

- [ ] **Update task .md files as you progress**
  - Mark completed tasks
  - Add notes about decisions
  - Update approach if changed

- [ ] **Document decisions in docs/decisions/**
  - Architectural choices
  - Technical tradeoffs
  - "Why" behind non-obvious implementations

- [ ] **Keep conversation focused on current task**
  - One task at a time
  - Complete and externalize before moving on
  - Resist scope creep

- [ ] **Reference .md files instead of repeating info**
  ```
  Bad:  "Remember we decided to use PostgreSQL because..."
  Good: "Per docs/decisions/001-database.md, we're using PostgreSQL"
  ```

- [ ] **Monitor context usage**
  - Check token count periodically
  - If > 70%, plan to externalize
  - If > 85%, take immediate action

- [ ] **Use MCPs for external data only**
  - Framework docs via Context7
  - Browser debugging via DevTools
  - Don't use for project files

- [ ] **Progressively load context**
  - Start with 2-3 files
  - Add more only when needed
  - Remove files when tasks complete

### After Completion

- [ ] **Write session summary to docs/context/**
  - What was accomplished
  - Decisions made
  - Current state
  - Next steps

- [ ] **Update relevant docs/ with learnings**
  - Update docs/architecture/ if design changed
  - Add docs/guides/ for complex procedures
  - Update docs/api/ if endpoints changed

- [ ] **Clean up temporary files**
  - Remove debug logs
  - Clean up test files
  - Archive completed plans

- [ ] **Create handoff document if needed**
  - For multi-session work
  - For team collaboration
  - For future you

- [ ] **Commit documentation with code**
  ```bash
  git add src/ docs/
  git commit -m "Implement feature X, update architecture docs"
  ```

### Periodic Maintenance

- [ ] **Review docs/ structure monthly**
  - Archive old plans
  - Update architecture docs
  - Consolidate scattered decisions

- [ ] **Update .cursorrules as patterns emerge**
  - New conventions
  - Common pitfalls
  - Preferred approaches

- [ ] **Create templates for common .md files**
  - docs/templates/proposal.md
  - docs/templates/decision.md
  - docs/templates/handoff.md

---

## Real-World Scenarios

### Scenario 1: Large Feature Development

**Context: Implementing complete user authentication system**

**Traditional approach:**
```
Session 1:
You: "Let's build user auth with JWT, refresh tokens, RBAC, email verification..."
[Discuss everything: 10k tokens]
Agent: *Starts implementing*
[Conversation includes all files, all decisions: 100k tokens]
[Session hits context limit at 80% complete]

Session 2:
You: "Continue auth implementation... we discussed JWT, refresh tokens..."
[Re-explain: 5k tokens]
[Agent missing some context, makes conflicting choices]
[Another 80k tokens]

Total: ~195k tokens, inconsistent implementation, context pain
```

**With .md-based approach:**
```
Session 1:
You: "Let's plan user auth. Use openspec to create proposal."
Agent: *Writes docs/plans/auth-feature.md*
[Planning: 5k tokens]

Session 2:
You: "Implement docs/plans/auth-feature.md - start with database schema"
Agent: *Reads plan (500 tokens), implements schema*
[Implementation: 8k tokens]

Session 3:
You: "Continue docs/plans/auth-feature.md - JWT generation"
Agent: *Reads plan (500 tokens), implements JWT*
[Implementation: 7k tokens]

... (repeat for each component)

Total: ~40k tokens, consistent implementation, no context issues
Savings: ~155k tokens (79% reduction)
```

### Scenario 2: Multi-Session Project

**Context: Building feature over several days**

**Without documentation:**
```
Day 1: Implement 50%, end of workday
Day 2: "What were we doing?"
       Try to remember details
       Agent has no context
       Re-explain everything: 10k tokens
       Waste 30 minutes getting back into flow

Day 3: Similar problem, worse memory
       More re-explanation
       Agent makes decisions conflicting with Day 1
       Have to redo work
```

**With docs/context/ handoffs:**
```
Day 1:
- Implement 50%
- End: "Write handoff to docs/context/auth-day1.md"
- Agent writes: completed work, decisions, next steps

Day 2:
- Start: "Read docs/context/auth-day1.md and continue"
- Agent has full context in 2 minutes
- Zero wasted time, perfect continuity

Day 3:
- Start: "Read docs/context/auth-day2.md and continue"
- Seamless continuation
- Consistent decisions throughout
```

### Scenario 3: Framework Documentation Lookup

**Context: Need to understand React hooks best practices**

**Without MCP:**
```
You:
1. Open browser
2. Search "react useEffect best practices"
3. Read article
4. Copy-paste relevant sections
5. Paste into conversation: 2000 tokens

Agent: Analyzes pasted content, provides answer

Total: Your time + 2000 tokens
```

**With Context7 MCP:**
```
You: "Use Context7 to check React useEffect best practices for
     cleanup functions, then implement proper cleanup in
     src/components/DataFetcher.tsx"

Agent:
1. Queries Context7 MCP for React docs
2. Analyzes best practices
3. Implements proper cleanup

Total: Agent time + 300 tokens
Savings: Your time + 1700 tokens
```

### Scenario 4: Debugging Complex Issue

**Context: Strange authentication bug**

**Bloated approach:**
```
Include in context:
- All auth files (10 files)
- All user-related files (15 files)
- Database schemas
- API routes
- Full error logs
- Network traces

Total context: ~80k tokens
Agent: Overwhelmed, suggests generic debugging steps
```

**Focused approach with progressive loading:**
```
Start:
- Error message
- src/api/auth.ts (where error occurs)
Total: 2k tokens

Agent: "Check token validation"
You: "Add src/utils/jwt.ts"
Total: 3k tokens

Agent: "Found issue - expired token not handled"
You: "Add tests/auth.test.ts to verify fix"
Total: 5k tokens

Result: Issue found and fixed with 5k tokens vs 80k tokens
Savings: 75k tokens (94% reduction)
```

### Scenario 5: Code Review of Large PR

**Context: Review PR with 50 files changed**

**All-at-once approach:**
```
Load all 50 files into context
Try to review everything at once
Context: 100k tokens
Agent: Surface-level review, misses important details
Quality: Low (overwhelmed by volume)
```

**Checklist-driven approach:**
```
Step 1: Create docs/reviews/pr-123.md with checklist
- [ ] Security review
- [ ] Error handling
- [ ] Test coverage
- [ ] API design consistency
- [ ] Performance considerations

Step 2: Review by category
Session 1: Security - load only auth-related files
Session 2: Error handling - load only changed logic
Session 3: Tests - load only test files
...

Each session: 10-15k tokens
Total: ~50k tokens across sessions
Quality: High (focused, thorough review per category)
Savings: 50k tokens + better quality
```

### Scenario 6: Architecture Refactor

**Context: Refactoring API layer architecture**

**No planning approach:**
```
You: "Let's refactor the API to use service layer pattern"
Agent: Starts making changes
[Files change across sessions]
[Inconsistent patterns emerge]
[Have to explain service layer pattern repeatedly]
[Refactor takes 3 weeks, inconsistent implementation]
```

**Documentation-first approach:**
```
Week 1: Planning
- Write docs/proposals/service-layer-refactor.md
  - Current problems
  - Proposed architecture
  - Migration strategy
  - File-by-file plan
- Review and refine with team

Week 2: Execution
Session 1: "Implement step 1 of docs/proposals/service-layer-refactor.md"
Session 2: "Implement step 2 of docs/proposals/service-layer-refactor.md"
...

Each session:
- Reads proposal (500 tokens)
- Implements next step
- Updates proposal with progress

Result: Consistent refactor, completed in 2 weeks, well-documented
```

---

## Quick Reference

### When to Externalize to .md

```
Ask: "Will I need this information again?"
├─ YES → Write to .md file
└─ NO → Keep in conversation

Ask: "Is this a decision or just discussion?"
├─ Decision → docs/decisions/*.md
└─ Discussion → Conversation (ephemeral)

Ask: "Am I repeating myself?"
├─ YES → Create .md, reference it
└─ NO → Continue conversation
```

### File Location Guide

| Information Type | Location | Example |
|-----------------|----------|---------|
| Feature plans | `docs/plans/` | `auth-feature.md` |
| Architecture | `docs/architecture/` | `api-design.md` |
| Decisions | `docs/decisions/` | `001-database.md` |
| Session handoffs | `docs/context/` | `2024-01-session.md` |
| How-to guides | `docs/guides/` | `deployment.md` |
| API docs | `docs/api/` | `endpoints.md` |
| Active tasks | `.tasks/` | `current-sprint.md` |
| Persistent instructions | Root | `.cursorrules` |

### Context Budget Rules

| Usage | Action |
|-------|--------|
| 0-60% | ✅ Optimal - full quality |
| 60-75% | ⚠️ Monitor - consider externalizing |
| 75-85% | ⚠️ Warning - plan to reset soon |
| 85-95% | 🚨 Danger - externalize now |
| 95-100% | 🛑 Critical - immediate action |

### MCP Decision Tree

```
Do I need external data?
├─ Framework/library docs → Context7 MCP
├─ Browser debugging → DevTools MCP
├─ Database queries → Database MCP
├─ API calls → API Client MCP
└─ Project files → Direct file read (NOT MCP)
```

## Workflow Integration

**Used Throughout All Phases:**

**Phase 1: Planning**
- Context management for [PRD and specification management](../workflow/phase-1-planning.md)
- [OpenSpec CLI](../development-tools/recommended-tools/openspec-cli.md) integration for plan externalization
- Architecture decisions documented in [docs/decisions/](./#file-organization-for-context-management) for future reference

**Phase 2: Development**
- [Droid CLI](../development-tools/recommended-tools/droid-cli.md) plan/act workflow utilizing .md files
- Feature-by-feature context management per [development workflow](../workflow/phase-2-development.md#feature-by-feature-implementation)
- [Zed IDE](../development-tools/recommended-tools/zed.md) auto-compression and workflow management

**Phase 3: Testing & Debugging**
- Debug context and error tracking for [comprehensive testing](../workflow/phase-3-testing-debugging.md)
- [DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) externalizes browser debugging context
- Session handoffs between debugging sessions using [docs/context/](./#session-handoffs) pattern

**Phase 4: Deployment**
- Project handover documentation using [context management patterns](./#multi-session-project)
- Configuration and decision preservation for [client projects](./#real-world-scenarios)
- Knowledge transfer through [living documentation](./#living-documentation)

**Tool Integration:**

**Context7 MCP**
- Externalizes framework documentation to reduce context usage
- Integrates with [Core Technologies](../core-technologies.md) implementation
- Saves context for [AI Model Providers](../ai-model-providers/README.md) during architecture discussions

**Task Manager MCP**
- Persistent task management across [workflow phases](../workflow/)
- Context-aware task tracking using [task decomposition patterns](./#task-decomposition)
- Integration with [Phase 2 development workflow](../workflow/phase-2-development.md)

**Sequential Thinking MCP**
- Enhanced problem-solving context using [cognitive enhancement techniques](./#advanced-strategies)
- Strategic thinking preservation in [docs/decisions/](./#file-organization-for-context-management)
- Integration with [planning workflows](../workflow/phase-1-planning.md)

**MCP Server Context Optimization:**
- [Context7 MCP](../development-tools/mcp-servers/context7-mcp.md) — Framework documentation externalization
- [DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) — Browser debugging context management
- [Task Manager MCP](../development-tools/mcp-servers/task-manager-mcp.md) — Persistent workflow context
- [Sequential Thinking MCP](../development-tools/mcp-servers/sequential-thinking-mcp.md) — Problem-solving context
- [Shadcn MCP](../development-tools/mcp-servers/shadcn-mcp.md) — UI component context for [Phase 2 development](../workflow/phase-2-development.md)

**Business Strategy Integration:**
- [Client project handover](./#client-project-considerations) using context management best practices
- [Freelance workflow optimization](../introduction/README.md) through efficient context usage
- [Cost-effective development](../workflow/phase-0-vibecoder-preparation.md) via reduced AI token consumption

**Related Documentation:**
- [Learning Path](../../README.md#learning-path) for context management integration
- [Glossary](../glossary.md) for context-related terminology
- [Contributing](../contributing.md) for context management in documentation

---

**Back to:** [Top-level README](../../README.md)

**Related:**
- [Development Tools](../development-tools/)
- [Core Technologies](../core-technologies.md)
- [Workflow](../workflow/)
