# Phase 1: Planning (Pre‑Development) 🗺️

**Tools:** Any AI chat (ChatGPT, Claude, Gemini, etc.) + OpenSpec

## The Modern Planning Workflow

Planning is where vibecoding truly starts. The recommended approach uses external AI chats to refine your ideas, then leverages OpenSpec to kickstart the project with proper structure.

---

## Step 1: External Chat Ideation (PRIMARY Approach)

Before touching any code or tools, use any AI chat platform to explore and validate your idea.

### Why External Chat First?

- **Thought refinement**: Natural conversation helps clarify fuzzy ideas
- **Feature validation**: AI helps identify missing requirements or edge cases
- **Technical direction**: Get feedback on architecture and tech stack choices
- **PRD generation**: End the conversation with a comprehensive description ready for OpenSpec

### Recommended Platforms

Choose any AI chat you prefer:
- **ChatGPT** - Great for general ideation and feature planning
- **Claude** (web) - Excellent for technical architecture discussions
- **Gemini** - Good alternative with strong reasoning
- **Any other AI chat** - Use what works best for you

### The Ideation Process

**1. Start with the problem**
```
"I want to build a task management app for remote teams.
Users need to collaborate on tasks, track time, and generate reports."
```

**2. Iterate and refine**
- Discuss features and priorities
- Validate technical approaches
- Consider edge cases and user flows
- Talk through architecture decisions

**3. Include infrastructure early**

**CRITICAL**: Mention your tech stack during the conversation:
```
"I'm thinking of using Astro for the frontend, Tailwind for styling,
and deploying to Cloudflare Pages. What do you think?"
```

This helps the AI (and later OpenSpec) understand both **WHAT** you're building and **HOW** it should be built.

**4. Get a PRD at the end**

Once you've refined the idea, ask the chat to produce a comprehensive description:
```
"Based on our conversation, can you create a detailed Product Requirements
Document (PRD) that includes:
- Project overview and goals
- Core features and functionality
- Technical stack (Astro, Tailwind, Cloudflare Pages)
- User flows and requirements
- Architecture considerations

Format it in a way that can be used as input for project planning tools."
```

---

## Step 2: OpenSpec Project Kickoff (MUST-HAVE)

OpenSpec is essential for transforming your PRD into a structured project plan.

### Why OpenSpec?

- Analyzes your PRD and generates comprehensive project structure
- Creates feature specifications automatically
- Breaks down features into actionable tasks
- Understands infrastructure when you mention it
- Provides implementation proposals

### Using OpenSpec

**1. Prepare your input**

Use the PRD from your chat conversation. Make sure it includes:
- ✅ What you're building (features, requirements)
- ✅ How to build it (tech stack, infrastructure, deployment)
- ✅ Any specific constraints or preferences

**Example input with infrastructure:**
```markdown
# Task Management Platform

Build a collaborative task management app using:
- **Frontend**: Astro + React components
- **Styling**: Tailwind CSS
- **Backend**: Cloudflare Workers + D1 database
- **Deployment**: Cloudflare Pages
- **Auth**: Cloudflare Access

Features:
1. User authentication and team workspaces
2. Task creation, assignment, and tracking
3. Time tracking per task
4. Weekly/monthly reports
...
```

**2. Run OpenSpec**

```bash
openspec init
# Follow prompts, paste your PRD when asked
```

**3. Review the output**

OpenSpec generates structured documentation ready for development.

---

## Step 3: Traditional Planning Steps

After OpenSpec generates your project structure, you'll have:

### 1. Product Requirements Document (PRD)
Detailed feature descriptions and requirements

### 2. Architecture Documentation
Technical decisions and system design

### 3. Feature Specifications
Each feature broken down into:
- User stories
- Acceptance criteria
- Technical considerations

### 4. Task Breakdown
Features split into actionable development tasks

---

## Expected Output Structure

```text
/docs/
├── prd.md                    # Product requirements
├── architecture.md           # Technical architecture
├── tech-stack.md            # Technology decisions
├── features/
│   ├── feature-1-spec.md    # Feature specification
│   ├── feature-1-tasks.md   # Implementation tasks
│   ├── feature-2-spec.md
│   └── feature-2-tasks.md
└── deployment.md            # Infrastructure and deployment plan
```

---

## Pro Tips

✅ **Do this before opening the IDE** - Plan thoroughly, code confidently

✅ **Invest time in the chat conversation** - A good PRD saves hours in development

✅ **Always mention infrastructure** - OpenSpec needs to know both what and how

✅ **Use Claude for plan review** - Get a second opinion on your architecture

✅ **Use GLM or GPT for detailed specs** - Great for expanding feature details

✅ **Iterate the plan** - Don't hesitate to refine specs before coding

---

## Next Steps

Once you have your planning docs ready:

1. ✅ You have a clear PRD and architecture
2. ✅ Features are specified and broken into tasks
3. ✅ Tech stack and infrastructure are defined
4. → **Next**: [Set up your environment and start development](./phase-2-development.md)

---

Next: [Phase 2 → Development](./phase-2-development.md)

Back: [Workflow overview](./README.md)
