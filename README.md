# The Comprehensive Vibecoding Guide

## From a practitioner, for practitioners

A compendium of knowledge drawn from commercial project experience and hundreds of thousands of lines of AI-assisted code.
Feel free to read through this or feed this repository to your chosen AI agent to summarize it and ask questions. 
The plan is to build some comprehensive, complete guidelines based on my observations and experience on vibecoding and real life commercial projects, which I develop to basically feed my family :) 
Stars and watchers will be appreciated!

---

## Table of Contents

1. [Introduction](#introduction)
2. [Quickstart](#quickstart)
3. [Tools and Tech Stack](#tools-and-tech-stack)
4. [Context Management](#context-management)
5. [Workflow and Process](#workflow-and-process)
6. [Glossary](#glossary)
7. [Contributing](#contributing)
8. [License](#license)

---

## Introduction

Vibecoding is an approach to software creation where you collaborate with AI as a coding partner. This guide is based on real commercial experience—projects delivered for clients where 98–100% of [...]  

### Who am I?

- Head of Department with over 10 years in software development
- 6 years as Head of Quality Assurance (process and engineering)
- Freelancer vibecoder—building software for local businesses
- AI experience since the early GPT beta
- Delivering commercial projects for companies with €100M–€1B annual revenue (mainly e-commerce)

### What will you learn?

- How to save ~70% on AI tool costs without sacrificing quality
- How to manage context effectively in long-term projects
- How to avoid pitfalls and the most common vibecoding mistakes
- How to build a reliable tool stack tailored to your needs
- How to deliver commercial projects powered entirely by AI

---

## Quickstart

Follow these steps to start vibecoding effectively:

1. Define the feature and outcomes (write a brief PRD).
2. Create specifications per feature (OpenSpec or your preferred format).
3. Set up your stack: Zed, GLM, Context7 MCP, DevTools MCP.
4. Load only relevant files into context; keep it lean.
5. Implement tasks one by one with an AI agent; review after each.
6. Test using DevTools MCP first, then manual checks.
7. Commit per finished feature; review before merge.

---

## Tools and Tech Stack

### My Core Stack (Current – 2025)

#### 1. Zed.dev – Primary IDE

Why Zed?
- AI-native IDE—built from the ground up for AI work
- Super frequent updates of the IDE itself, with major updates also improving the IDE significantly
- Lightweight—uses only 20% of VS Code’s resources for similar tasks
- Excellent context management—built-in AI agent keeps context clean
- Easy integration—connect to any LLM via API
- Agent features—great for longer tasks with automatic tracking

Key resource management advantages:
- Efficiently utilize up to 85% of the LLM’s token capacity
- No plugin clutter—clean context
- When a conversation nears the limit, the agent automatically compresses the dialog while preserving intent

#### 2. Droid CLI — Main Coding Agent

Why Droid CLI?
- Native spec-writing plans and expert execution against those plans
- Seamless alignment with GLM Coding Plan and OpenSpec-driven workflows
- Strong for larger features and multi-step implementations
- Configurable model routing; I occasionally use Codex and GPT‑5‑high for bigger plans

How I use it:
- Author specs with OpenSpec → run Droid CLI to plan → implement tasks sequentially
- Pair with DevTools MCP for fast feedback and testing

#### 3. GLM Coding Plan — Main LLM

Pricing:
- Lite: $3/month — 120 prompts per 5 hours
- Pro: $15/month — 600 prompts per 5 hours
- Max: $30/year — 2,400 prompts per 5 hours
- Practicality of limits: Very hard to hit even with 2–5 parallel agents on Pro and Max plans
- Optional: 10% off referral link (disclosure): <https://z.ai/subscribe?ic=CUEFJ9ALMX>

Why GLM?
- Lowest cost while keeping quality around Sonnet 4 level
- State-of-the-art open-source model
- Can autonomously resolve bugs for 10–15 minutes without intervention
- Handles complex projects (Next.js + complex database + backend)
- Works quite well with modern web development stacks (Svelte, React, Next.js, Astro, D1 databases, Cloudflare Wrangler files, etc.)

Cost comparison:
- Claude Code Max20: €200+ per month (with EU VAT)
- Codex Pro: €229 in EU with VAT per month
- Most alternatives will be more expensive than GLM (or other open-source models)

#### 4. OpenSpec CLI — Specification Framework

Advantages:
- **Completely free**
- Easy integration with existing codebases (edge over GitHub Speckit)
- Specification-driven development
- Works with any LLM via Zed (AGENTS.md file) or the majority of current AI coding agents via dedicated instructions files (CLAUDE.md, etc.)

Replaced in my stack: Traycer.ai (saving $25/month)

#### 5. Context7 MCP — Documentation Management

Features:
- Knowledge about what exactly should be done regarding chosen tech stack
- Documentation on given framework
- Critical for long-term projects
- Super critical for debugging issues — asking to use Context7 MCP to find documentation on a given issue usually helps the LLM resolve the problem

#### 6. DevTools MCP — Testing & Debugging

Testing breakthrough:
- 95% less context usage than Playwright
- Intelligent navigation for web development tests
- Automatic debugging: console logs, navigation, 500 errors

Workflow:
- Launch the MCP
- Inform the agent about issues
- The agent autonomously gathers data, debugs, and resolves

Pro tip: It’s more efficient to tell the LLM “use MCP” instead of writing a long debugging prompt.
Pro tip 2: For web development, it can even perform its own tests using Chrome DevTools MCP when prompted correctly.

### Complementary Stack

#### Claude Code CLI Client — Backup Coding Agent

Why Claude Code (backup)?
- Seamless with GLM Coding Plan (same as Droid)
- A bit faster for small changes and tight loops
- Currently configured to use GLM 4.6 natively in my setup

When to use:
- Small diffs, quick refactors, and single-file changes
- When I need a fast turnaround aligned with the GLM plan

#### GitHub Speckit

- Excellent for new projects
- Integration issues with existing, complex codebases
- My pick for kickstarting clean projects
- After recent updates—highly recommended for pure vibecoding

### MCP Servers — Recommendations

I use:
- Context7—absolutely essential
- shadcn MCP—smooth integration; essential for developing good‑looking websites using ready‑to‑use components
- Sequential Thinking MCP—context and planning optimization
- Task Manager MCP—project organization and proper planning tool to ensure that context doesn't get lost mid-development.
- Task Manager tip: You can reference tasks or task groups across your coding agent sessions.

Note: Don’t use too many MCPs—they will quickly consume your context window!

### Tools I Dropped

#### Traycer.ai

Why I left:
- Too slow—planning takes long, validation too, fixes even longer
- Plugin dependency—requires VS Code/derivatives (no Zed support as per time of writing this guide)
- Costly—$25/month for realistic workloads (with recent pricing changes having 1 artifact per 45 minutes it might not be even enough for serious, fast paced development)
- Frustration—when the plan hallucinates, rollbacks waste lots of time

What was good:
- Automatic validation of ongoing development
- High output quality (when it works)
- Usually, the combination of plan + validation + improvements after validation improved overall project quality (at the cost of significantly longer delivery time).

Conclusion: You can achieve similar results with OpenSpec + GLM for a fraction of the price—and often in less time—than with Traycer.

### Tool Compatibility

Not recommended to combine:
- Replit, Lovable, Bolt—closed platforms, limiting options
- Too many MCP servers at once
- Tools without the ability to connect using your own LLM API

---

## Context Management

### Fundamentals

**The most important rule:** Context is your most valuable resource. Manage it deliberately.

### Context Management Techniques

#### 1. Selective File Inclusion

Modular structure:

```text
project/
├── src/
│   ├── components/   # Only when working with UI
│   ├── api/          # Only when working on backend
│   ├── utils/        # Only when tools are needed
│   └── database/     # Only when working with DB
└── docs/             # Always indexed by Context7
```

Practice:
- Add only relevant folders to the prompt
- Don’t let AI scan the entire codebase every time
- You know best what’s needed—not AI

#### 2. MCP as Context Savings

Example — DevTools MCP:

Instead of:
> “Check the browser console, find errors, analyze the stack trace, inspect the network tab, review responses, debug the backend, fix the issue.”

Say:
> “Use the DevTools MCP to find and fix the error.”

Result: 95% fewer tokens consumed with better results.

#### 3. Dialog Compression

In Zed (automatic):
- When context fills up → the agent creates a summary
- Dialog is compressed
- Essential context is preserved
- You can continue without resetting

Manually:
- Periodically compress / compact the conversation and start from the compacted version
- Don't trust the tools themselves to do the compacting and context management for you
- Trust your intuition instead - **context is the most important thing when we're talking about Vibecoding**

#### 4. Avoiding Bloat

Don’t:
- Add `node_modules` to context
- Mass-include all files “just in case”
- Repeat the same instructions multiple times
- Run too many MCP servers at once

Do:
- Include only relevant files
- Use `.cursorrules` or similar for persistent instructions
- Use Context7 MCP for documentation
- Favor a modular architecture

### Monitoring Context Usage

Signs of trouble:
- Degradation in answer quality
- AI forgets prior decisions
- Repetitive mistakes
- Suggestions misaligned with project architecture

Solutions:
- Compress the dialog (summary)
- Remove unnecessary files from context
- Start a new session with a clear context + summary
- Add key decisions to `/docs`

### Context Window Strategy

Models and their limits:
- Claude Sonnet 3.5: 200k tokens
- GPT-4o: 128k tokens
- GLM 4.5: 128k+ tokens

My practice:
- Use up to 85% of capacity
- When approaching the limit: compress
- Never fill 100%—AI starts to rush to finish

Community pro tip:
If you have 1M context (Claude), you can fill it but compress around ~200k. The AI won’t feel end-of-context pressure and won’t trigger “rush-to-finish” behavior.

---

## Workflow and Process

### Project Phases

#### Phase 1: Planning (Pre-Development)

Tools: ChatGPT / Claude (web) + GitHub Speckit / OpenSpec

Steps:
1. Ideation—dialog with AI about the idea
2. Product Requirements Document (PRD)—detailed feature description
3. Specifications—split into features
4. Task Breakdown—each feature broken into tasks

Output:
/docs/
├── prd.md
├── architecture.md
├── features/
│ ├── feature-1-spec.md
│ ├── feature-1-tasks.md
│ ├── feature-2-spec.md
│ └── feature-2-tasks.md
└── tech-stack.md

Pro tips:
- Use Claude 3.5 to review plans
- Use GLM / GPT to write plans
- Do this before opening the IDE

#### Phase 2: Development

Tools: Zed + GLM + Context7 MCP + Devtools MCP

Workflow:
Open the project in Zed

Load the feature spec into context

One feature at a time:
a. Read the tasks
b. Agent implements task by task
c. After each task: manual review
d. After the feature: comprehensive review

Commit after each completed feature

Rules:
- One feature at a time—don’t mix
- Modular code—easier context management
- Commit frequently—after each working feature
- Review manually—always check before merge

Example session:
Session 1: User Authentication Feature

Task 1: Setup auth schema [COMMIT]

Task 2: Login endpoint [COMMIT]

Task 3: Register endpoint [COMMIT]

Task 4: JWT middleware [COMMIT]

Feature Review → merge to main

Session 2: Dashboard UI

#### Phase 3: Testing & Debugging

Tools: Devtools MCP + GLM + Manual Testing

Process:

1. Automated Testing via MCP:
> “Use DevTools MCP to test the login page and find bugs.”

Agent:
- Opens the browser
- Navigates the app
- Collects console errors
- Analyzes network calls
- Identifies issues
- Proposes a fix

2. Manual Testing:
- Walk through the functionality yourself
- Document edge cases
- Check different browsers/devices

3. Debugging Deep Dive:

Golden rule: Debugging is effective only when you dig deep.

Don’t:
"Doesn’t work, fix it"
"Still doesn’t work, fix pls" (x100)

Do:
Analyze the bug (manually or via MCP)

Gather logs specific to the issue

Identify the exact root cause

Tell the AI what you found + ask for a fix

If the same bug repeats 2–3 times:
1. Stop—something is fundamentally wrong
2. Use MCP to gather precise logs
3. Analyze them before the next prompt
4. You may need to change approach, not just code

#### Phase 4: Code Review & Refactoring

Process:
1. First pass—Claude 3.5 / GPT-4o review of the entire feature codebase
2. Identify issues
   - Performance problems
   - Security holes
   - Code duplication
   - Convention violations
3. Refactoring—GLM implements suggestions
4. Second review—ensure everything works

Beware over-optimization:
- If a simple bug requires a complete refactor → something’s off
- Try other models (Gemini, a different Claude)—maybe there’s a simpler solution
- Don’t let AI over-engineer simple problems

#### Phase 5: Deployment

My practice:
- Cloudflare Pages/Workers
- Vercel (for Next.js)
- GitHub Pages (static)

Automated deployment:
Setup CI/CD
git push → automatic deploy

---

## Glossary

- MCP: Model Context Protocol servers that extend agent capabilities (e.g., documentation, DevTools).
- Context window: The maximum token capacity a model can consider in a single interaction.
- Dialog compression: Summarizing conversation history to free up context.
- OpenSpec: An open specification pattern/CLI for spec‑driven development.

---

## Contributing

Contributions are welcome. Please open an issue to discuss major changes first, and use pull requests for proposed edits. Keep sections concise, actionable, and aligned with the guide’s tone.

---

## License

This project is licensed under the terms of the LICENSE file included in this repository.
```
