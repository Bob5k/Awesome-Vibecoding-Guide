# OpenSpec CLI — Specification Framework 📐

OpenSpec CLI is a powerful specification-driven development tool that transforms plain language descriptions into comprehensive project plans, tasks, and technical specifications. It bridges the gap between ideas and implementation by creating structured, editable documentation that guides the development process while maintaining the conversational vibecoding approach.

## 🎯 Core Value Proposition

### Specification-Driven Development

The magic of OpenSpec lies in its ability to convert user descriptions into complete development frameworks:

1. **Plain Language Input** → Describe what you want to build in natural language
2. **AI-Powered Generation** → OpenSpec creates proposals, tasks, and detailed specifications automatically
3. **Markdown Documentation** → Everything is saved as structured .md files for easy editing and review
4. **Natural Language Interaction** → Continue vibecoding with your agent throughout the process
5. **Phased Implementation** → Large features are broken down into manageable phases

**The more descriptive your initial prompt, the better the output quality.**

### Universal Integration

OpenSpec works seamlessly with virtually any coding agent:
- **Zed** (via AGENTS.md file)
- **Claude** (via CLAUDE.md instructions)
- **Droid CLI** (via custom instruction files)
- **Any AI coding agent** that can follow file-based instructions

## 🚀 Main Use Cases

### 1. Feature Development from Scratch

**Workflow:**
```
User: "I want to build a comprehensive user authentication system with social login, email verification, role-based access control, and admin dashboard"

OpenSpec Output:
- Phase 1: Database schema design and core authentication
- Phase 2: Social login integration (Google, GitHub, etc.)
- Phase 3: Email verification and password reset
- Phase 4: Role-based access control implementation
- Phase 5: Admin dashboard and user management
```

**Result:** 15-20 detailed tasks across 5 phases, each with technical specifications and implementation guidance.

### 2. Large-Scale Project Planning

OpenSpec excels at breaking down complex projects into digestible components:

- **E-commerce Platform** → Payment processing, inventory management, user accounts, admin panels
- **SaaS Application** → Multi-tenancy, billing, analytics, user onboarding
- **Mobile App Backend** → API design, database architecture, authentication, real-time features

### 3. Refactoring and System Upgrades

Perfect for planning major architectural changes:
```
"I need to migrate from REST to GraphQL, implement caching layer, and redesign the database schema"
```

### 4. Rapid Prototyping

Quickly generate specifications for MVPs and proof-of-concepts:
```
"I need a simple task management app with drag-and-drop, real-time updates, and team collaboration features"
```

## 💡 Key Features

### 1. Persistent Context Management

All specifications are saved as `.md` files, providing:
- **Version Control** → Track changes to specifications over time
- **Context Preservation** → AI agents maintain understanding of project scope
- **Easy Review** → Human-readable documentation for team collaboration
- **Editable Workflows** → Modify tasks and specifications as needed

### 2. Phase-Based Development

OpenSpec automatically splits large features into logical phases:
- **Foundation Phase** → Core architecture and database design
- **Feature Phases** → Individual feature implementations
- **Integration Phase** → Connecting components and testing
- **Polish Phase** → UI/UX refinements and optimization

### 3. Multi-LLM Workflow Support

One of OpenSpec's most powerful capabilities is enabling different LLMs for different development stages:

**Example Workflow:**
```
Phase 1: Planning & Specification
→ Use GPT-5-high (via [Droid CLI](./droid-cli.md)) for complex architectural decisions
→ Generate comprehensive plans and detailed specifications

Phase 2: Implementation
→ Switch to GLM-4.6 for cost-effective development
→ Execute individual tasks following the approved specifications

Result: Premium quality planning + budget-friendly implementation
```

**Benefits:**
- **Cost Optimization** → Use expensive LLMs only for high-value planning
- **Quality Assurance** → Get the best thinking for critical decisions
- **Development Speed** → Faster implementation with proven specifications
- **Reliability** → Consistent output regardless of LLM used for implementation

## 🔧 Practical Implementation

### Step-by-Step Workflow

1. **Natural Language Specification**
   - Simply describe your feature requirements in plain English to your AI agent
   - Example: "I want to build a user authentication system with social login and email verification"
   - The more detailed your description, the better the generated specifications

2. **Review Generated Specifications**
   - Open the generated `.md` files created by OpenSpec
   - Review proposals, tasks, and technical specifications
   - Edit as needed to align with your requirements

3. **Phase-Based Development**
   - Work through each phase with your AI agent
   - Simply tell your agent which phase you want to work on next
   - No complex commands or syntax required

4. **Iterative Refinement**
   - Modify specifications between phases through natural conversation
   - Adjust tasks based on development insights
   - Maintain context throughout the project

### Best Practices

1. **Descriptive Input Matters**
   - Include business requirements, technical constraints, user scenarios
   - Mention performance requirements, scalability considerations
   - Specify existing systems that need integration

2. **Review Before Implementation**
   - Always review generated specifications before coding
   - Edit tasks to match your coding style and preferences
   - Adjust phase boundaries based on your team's workflow

3. **Use Different LLMs Strategically**
   - Premium LLMs for planning and complex problem-solving
   - Cost-effective LLMs for routine implementation
   - Specialized models for specific domains when needed

## 🎭 Real-World Example

**Input:** "I want to build a real-time collaborative document editor with Google Docs-like features"

**OpenSpec Output:**
```
Phase 1: Core Architecture (Tasks 1-4)
- Real-time synchronization system design
- Database schema for document storage
- WebSocket implementation plan
- Conflict resolution strategy

Phase 2: Editor Implementation (Tasks 5-9)
- Rich text editor integration
- Cursor tracking and user presence
- Version control and history
- Permission system

Phase 3: Collaboration Features (Tasks 10-14)
- Real-time commenting system
- Document sharing and permissions
- Export functionality
- Mobile responsiveness

Phase 4: Polish & Optimization (Tasks 15-18)
- Performance optimization
- Offline support
- Advanced formatting features
- Analytics and usage tracking
```

## 🆚 Advantages Over Alternatives

- **Completely Free** → No subscription costs or usage limits
- **Easy Integration** → Works with existing codebases (edge over GitHub Speckit)
- **Universal Compatibility** → Works with any coding agent
- **Persistent Documentation** → Specifications live as editable markdown files
- **Phase-Based Approach** → Natural progression from planning to implementation
- **Multi-LLM Support** → Flexibility to optimize costs and quality

**Replaced in my stack:** Traycer.ai (saving $25/month)

## 🎯 Bottom Line

OpenSpec CLI transforms vague ideas into concrete, actionable development plans while preserving the natural, conversational vibecoding experience. Unlike complex CLI tools that require memorizing commands and syntax, OpenSpec lets you continue talking to your AI agent in plain English while automatically generating structured specifications. By creating detailed specifications that work with any coding agent, it enables reliable, scalable development while maintaining the flexibility to use different LLMs for different tasks. The result is a systematic approach to building anything from simple features to complex enterprise applications without disrupting your natural development workflow.

See also: [Droid CLI](./droid-cli.md), [GLM Coding Plan](./glm-coding-plan.md), [DevTools MCP](./devtools-mcp.md)

Back: [Tools & Tech Stack](./README.md)