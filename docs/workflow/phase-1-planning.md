# Phase 1: Planning (Pre‑Development) 🗺️

**Tools:** Any AI chat (ChatGPT, Claude, Gemini, etc.) + Clavix

## The Modern Planning Workflow

Planning is where vibecoding truly starts. The recommended approach uses external AI chats to refine your ideas, then leverages Clavix to generate comprehensive PRDs with ready-to-implement task lists.

---

## Step 1: External Chat Ideation (PRIMARY Approach)

Before touching any code or tools, use any AI chat platform to explore and validate your idea.

### Why External Chat First?

- **Thought refinement**: Natural conversation helps clarify fuzzy ideas
- **Feature validation**: AI helps identify missing requirements or edge cases
- **Technical direction**: Get feedback on architecture and tech stack choices
- **PRD generation**: End the conversation with a comprehensive description ready for Clavix

### Recommended Platforms

Choose any AI chat you prefer:
- **ChatGPT** - Great for general ideation and feature planning
- **Claude** (web) - Excellent for technical architecture discussions
- **Gemini** - Good alternative with strong reasoning
- **Any other AI chat** - Use what works best for you

### The Ideation Process

**Pro Tip:** For effective AI collaboration during ideation, see [Mastering AI Prompts](../prompting/README.md) - learn how to structure your questions and requests for better results.

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

This helps the AI (and later Clavix) understand both **WHAT** you're building and **HOW** it should be built.

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

## Step 2: Clavix PRD Generation (MUST-HAVE)

Clavix is essential for transforming your ideas into structured PRDs with implementation-ready task lists.

### Why Clavix?

- Uses CLEAR framework (Concise, Logical, Explicit, Adaptive, Reflective) for optimal structure
- Generates comprehensive Product Requirements Documents automatically
- Creates ready-to-implement task lists with clear acceptance criteria
- Includes built-in task tracking and progress management
- Optimizes prompts for maximum AI effectiveness

### Using Clavix

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

**2. Run Clavix**

```bash
# Install Clavix globally
npm install -g clavix

# Initialize in your project
clavix init

# Generate PRD with task list
/clavix:prd
# Or via CLI: clavix prd

# Generate implementation tasks
clavix tasks generate
```

**3. Review the output**

Clavix generates structured PRD with implementation tasks ready for development.

---

## Step 3: Traditional Planning Steps

After Clavix generates your PRD and task lists, you'll have:

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

✅ **Always mention infrastructure** - Clavix needs to know both what and how

✅ **Use Claude for plan review** - Get a second opinion on your architecture

✅ **Use GLM or GPT for detailed specs** - Great for expanding feature details

✅ **Iterate the plan** - Don't hesitate to refine specs before coding

---

## Business Planning Integration 💼

### Client Project Considerations
If building for clients, include these planning elements:

**Pricing Strategy:**
- Define project scope boundaries based on features planned
- Set clear deliverables and timelines
- Plan for testing and revision cycles

**Technical Approach:**
- Choose [cost-effective hosting](../hosting-tools/README.md) for client sites
- Plan for maintenance and update workflows
- Consider client technical expertise for handover

**Value Proposition:**
- Focus on performance benefits of your [core tech stack](../core-technologies.md)
- Highlight faster deployment and lower hosting costs
- Plan for SEO and performance optimization

### Personal Project Considerations
If building for your own business:

**Market Validation:**
- Research competition during external chat phase
- Define monetization strategy early
- Plan for user acquisition and growth

**MVP Planning:**
- Focus on core features that solve the main problem
- Plan iterative improvement based on user feedback
- Consider [budget-friendly tools](../workflow/phase-0-vibecoder-preparation.md) initially

---

## Common Issues & Troubleshooting

### Clavix Not Generating Useful Output
**Issue:** Clavix produces generic or incomplete PRD structure
- **Solution:** Ensure your input includes BOTH what (features) AND how (tech stack, infrastructure)
- **Tip:** Use `/clavix:deep` for comprehensive analysis of complex projects
- **See:** [Step 2: Clavix PRD Generation](#step-2-clavix-prd-generation-must-have) for proper input format

### AI Chat Conversations Going Off-Track
**Issue:** Ideation conversations become unfocused or overwhelming
- **Solution:** Use structured prompts from [Mastering AI Prompts](../prompting/README.md)
- **Tip:** Start with the problem, not the solution
- **Break down:** Large features into smaller, manageable pieces

### Unclear Project Scope
**Issue:** Can't define clear boundaries for the project
- **Solution:** Review [Project Scoping](#project-scoping) section in Phase 0
- **Start with:** MVP (Minimum Viable Product) approach
- **See also:** [Business Model Planning](../business-model/README.md) for client scoping

### Planning Taking Too Long
**Issue:** Spending days on planning without starting development
- **Solution:** Time-box planning to 1-2 days maximum
- **Remember:** Plans will evolve during development - don't over-optimize
- **Move forward when:** You have clear PRD, architecture, and first features defined

**For additional help:** Consult the [Troubleshooting Guide](../troubleshooting/README.md) for detailed solutions to planning challenges.

---

## Next Steps

Once you have your planning docs ready:

1. ✅ You have a clear PRD and architecture
2. ✅ Features are specified and broken into tasks
3. ✅ Tech stack and infrastructure are defined
4. ✅ Business considerations are documented
5. → **Next**: [Set up your environment and start development](./phase-2-development.md)

**Related Reading:**
- [Introduction: Business Model](../introduction/README.md) - Freelance strategy details
- [Phase 0: Cost-Effective Tools](../workflow/phase-0-vibecoder-preparation.md) - Budget planning
- [Core Technologies](../core-technologies.md) - Client-friendly tech stack

---

Next: [Phase 2 → Development](./phase-2-development.md)

Back: [Workflow overview](./README.md)
