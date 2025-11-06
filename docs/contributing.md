# Contributing 🤝

Thank you for your interest in improving the Awesome Vibecoding Guide! This document provides comprehensive guidelines for contributing to the repository, with special focus on maintaining consistent cross-referencing throughout the documentation.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Types of Contributions](#types-of-contributions)
3. [Cross-Reference Standards](#cross-reference-standards)
4. [Writing Guidelines](#writing-guidelines)
5. [Documentation Structure](#documentation-structure)
6. [Review Process](#review-process)
7. [Style Guide](#style-guide)

---

## Getting Started

### How to Contribute

**For Minor Changes:**
1. Fork the repository
2. Make your changes following the guidelines below
3. Test your changes by reading through the affected sections
4. Submit a pull request with a clear description

**For Major Changes:**
1. Open an issue to discuss your proposed changes
2. Wait for maintainer feedback and approval
3. Implement changes following these guidelines
4. Submit a pull reference to your issue

**For Bug Fixes:**
1. Check existing issues to avoid duplicates
2. Open a new issue with reproduction steps if needed
3. Fix the issue following the guidelines
4. Include tests or verification steps

---

## Types of Contributions

**High-Priority Contributions:**
- ✅ Cross-reference improvements and additions
- ✅ Tool documentation updates
- ✅ Workflow clarification
- ✅ New tool recommendations
- ✅ Cost optimization strategies

**Medium-Priority Contributions:**
- ✅ Grammar and clarity improvements
- ✅ Structure and navigation enhancements
- ✅ Examples and use cases
- ✅ Performance optimizations

**Low-Priority Contributions:**
- ✅ Stylistic improvements
- ✅ Minor formatting changes
- ✅ Redundant content removal

---

## Cross-Reference Standards

### When to Add Cross-References

**Always Link When:**
- ✅ A section mentions tools that have dedicated documentation
- ✅ Workflow phases reference each other
- ✅ Concepts in one section are explained in detail elsewhere
- ✅ Implementation details reference larger concepts
- ✅ Business considerations relate to technical implementation

**Link Types and Examples:**

**1. Navigation Links**
```markdown
[Descriptive link text](../path/to/document.md) — For direct navigation

Examples:
- [Core Technologies](../core-technologies.md) — Recommended tech stack
- [Phase 1: Planning](../workflow/phase-1-planning.md) — Project structure
- [Hosting Tools](../hosting-tools/README.md) — Complete hosting guide
```

**2. Section-Specific Links**
```markdown
[Descriptive link text](../path/to/document.md#specific-section) — For targeted information

Examples:
- [Phase 0 tool selection](../workflow/phase-0-vibecoder-preparation.md#tool-setup) — Setup details
- [Free alternatives](../ai-model-providers/README.md#honorable-mentions) — Budget options
- [Cost optimization](../workflow/phase-0-vibecoder-preparation.md#cost-effective-development-strategy) — Money-saving tips
```

**3. Tool-Specific Links**
```markdown
[Tool mentions](../development-tools/tool-name.md) — For detailed tool information

Examples:
- [Zed IDE](../development-tools/recommended-tools/zed.md) — Primary development environment
- [DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) — Testing and debugging
- [GLM Coding Plan](../ai-model-providers/glm-coding-plan.md) — Main AI provider
```

**4. Concept Links**
```markdown
[Concept references](../path/to/document.md) — For detailed explanations

Examples:
- [Context management](../context-management/README.md) — Efficient workflow practices
- [Vibecoding philosophy](../introduction/philosophy.md) — Core principles
- [MCP servers](../development-tools/README.md#mcp-servers) — Tool integrations
```

### Cross-Reference Quality Checklist

**Before submitting any contribution:**

- [ ] All major concepts link to relevant sections
- [ ] Workflow phases reference appropriate tools and next steps
- [ ] Business considerations are integrated where relevant
- [ ] New sections include "Related Reading" or "Next Steps"
- [ ] Navigation links use descriptive text (avoid "click here")
- [ ] Cross-references maintain context (make sense without reading target)
- [ ] Internal links work (verify by clicking through)
- [ ] Link text is consistent with target document titles

### Common Cross-Reference Patterns

**Tool Integration Sections:**
```markdown
## Implementation Tools for [Technology]

**Development Tools:**
- [Tool Name](../path/to/tool.md) — Description of usage
- [Tool Name](../path/to/tool.md) — Specific integration benefit

**Workflow Integration:**
- [Phase X](../workflow/phase-x-name.md) — How this fits in the process
- [Related Phase](../workflow/phase-y-name.md) — Dependencies and connections

**Budget Considerations:**
- [Cost comparison](../ai-model-providers/README.md#pricing) — Financial impact
- [Free alternatives](../development-tools/honorable-mentions/README.md) — Budget options
```

**Workflow Cross-Phase Integration:**
```markdown
## Pre-requisites & Next Steps

**Requires completion of:**
- [Previous Phase](../workflow/phase-x-previous.md) — What's needed first
- [Setup documentation](../path/to/setup.md) — Prerequisites
- [Tool configuration](../development-tools/README.md) — Environment preparation

**Prepares for:**
- [Next Phase](../workflow/phase-y-next.md) — What comes next
- [Related documentation](../path/to/document.md) — Supporting information

**Related Reading:**
- [Concept explanation](../path/to/concept.md) — Detailed background
- [Practical examples](../path/to/examples.md) — Implementation details
```

### Cross-Reference Anti-Patterns to Avoid

**❌ Don't:**
- Link to non-existent files
- Use generic link text like "click here" or "here"
- Create circular references
- Link to sections that don't exist
- Break links by changing file names without updating references
- Over-link (link every other word)

**✅ Do:**
- Verify all links work
- Use descriptive, meaningful link text
- Keep cross-references balanced and helpful
- Update references when moving files
- Test navigation flow
- Consider user journey when adding links

---

## Writing Guidelines

### Content Standards

**Keep sections:**
- ✅ **Concise** - Get to the point quickly
- ✅ **Actionable** - Readers can follow steps immediately
- ✅ **Aligned** - Match the guide's practical, experience-based tone
- ✅ **Up-to-date** - Reflect current tools and best practices

**Avoid:**
- ❌ Theoretical discussions without practical application
- ❌ Outdated tool recommendations
- ❌ Overly complex explanations
- ❌ Personal preferences without justification

### Voice and Tone

**Maintain the guide's voice:**
- Practical and experience-based
- Confident but not dogmatic
- Cost-conscious and efficiency-focused
- Accessible to intermediate developers
- Action-oriented language

**Example:**
```markdown
✅ Good: "Use Cloudflare Pages for hosting - it's free and fast"
❌ Avoid: "One might consider that Cloudflare Pages potentially offers advantages"
```

### Technical Accuracy

**Ensure all recommendations are:**
- Based on real commercial experience
- Tested and verified
- Cost-effective and practical
- Currently maintained and supported

**When recommending tools:**
- Include pricing information
- Mention alternatives for budget constraints
- Provide setup instructions or links
- Explain why this tool over alternatives

---

## Documentation Structure

### File Organization

```
docs/
├── README.md                 # Main index
├── introduction/             # Philosophy and approach
│   ├── README.md
│   └── philosophy.md
├── workflow/                 # Core methodology
│   ├── README.md
│   ├── phase-0-vibecoder-preparation.md
│   ├── phase-1-planning.md
│   ├── phase-2-development.md
│   ├── phase-3-testing-debugging.md
│   └── phase-4-deployment.md
├── development-tools/        # Tool documentation
│   ├── README.md
│   ├── recommended-tools/
│   ├── mcp-servers/
│   └── honorable-mentions/
├── ai-model-providers/       # AI service documentation
│   ├── README.md
│   ├── glm-coding-plan.md
│   ├── synthetic-new.md
│   ├── factory-ai.md
│   └── honorable-mentions/
├── core-technologies.md      # Tech stack recommendations
├── hosting-tools/           # Infrastructure guide
│   └── README.md
├── context-management/      # Workflow efficiency
│   └── README.md
├── glossary.md              # Key terms
└── contributing.md          # This file
```

### Section Structure Templates

**New Tool Documentation:**
```markdown
# Tool Name

## Overview
[What the tool does, why it's recommended]

## Pricing
[Current pricing, cost comparison]

## Key Features
[Main capabilities, benefits]

## Integration Setup
[Step-by-step configuration]

## Workflow Integration
**Used in:**
- [Phase X](../workflow/phase-x.md) — Specific use case
- [Phase Y](../workflow/phase-y.md) — Another use case

**Tool Integration:**
- [Related tool](../development-tools/related-tool.md) — How they work together
- [Setup guide](../development-tools/setup.md) — Configuration

## Best Practices
[Recommended usage patterns]

## When to Use
[Scenarios where this tool excels]

## Alternatives
- [Free option](../development-tools/honorable-mentions/free-tool.md) — Budget alternative
- [Premium option](../development-tools/premium-tool.md) — Feature comparison

Back: [Development Tools](../development-tools/README.md)
```

**New Workflow Phase:**
```markdown
# Phase X: [Name]

**Tools:** [Required tools and technologies]

## Overview
[What this phase accomplishes]

## Prerequisites
- [Previous phase completion](../workflow/phase-x-previous.md)
- [Setup requirements](../path/to/setup.md)

## Step-by-Step Process
[Detailed implementation steps]

## Best Practices
[Proven approaches and tips]

## Common Pitfalls
[What to avoid and why]

## Quality Assurance
[How to verify completion]

## Next Steps
- [Phase Y](../workflow/phase-y-next.md) — What comes next
- [Related documentation](../path/to/related.md) — Supporting information

Back: [Workflow Overview](../workflow/README.md)
```

---

## Review Process

### Self-Review Checklist

Before submitting any contribution, verify:

**Content Quality:**
- [ ] Information is accurate and up-to-date
- [ ] Examples are tested and work as described
- [ ] Pricing and tool information is current
- [ ] Technical details are correct
- [ ] Tone matches guide's voice

**Structure and Navigation:**
- [ ] Section headings follow consistent hierarchy
- [ ] Table of contents is updated if applicable
- [ ] Cross-references are accurate and helpful
- [ ] Navigation flow makes sense
- [ ] File organization follows established patterns

**Cross-References:**
- [ ] All links work and point to correct destinations
- [ ] Link text is descriptive and meaningful
- [ ] Cross-references enhance rather than clutter
- [ ] Related concepts are properly connected
- [ ] Workflow phases reference appropriate tools and next steps

**Writing Quality:**
- [ ] Grammar and spelling are correct
- [ ] Sentences are clear and concise
- [ ] Technical terms are explained or linked
- [ ] Actionable advice is provided
- [ ] Content adds value to the guide

### Testing Your Changes

**Navigation Testing:**
1. Read through affected sections
2. Click all cross-references to ensure they work
3. Verify navigation flow makes sense
4. Check for broken links or missing sections

**Content Verification:**
1. Test any code examples or commands
2. Verify tool pricing and availability
3. Check that steps work as described
4. Ensure compatibility with mentioned tools

**User Experience:**
1. Read sections as a new user would
2. Verify that information flows logically
3. Check that cross-references provide value
4. Ensure content is accessible and actionable

---

## Style Guide

### Writing Style

**Preferred Language:**
- Use active voice
- Write in second person ("you") for direct guidance
- Use present tense for instructions
- Be conversational but professional
- Include specific examples and numbers

**Formatting Preferences:**
```markdown
# Main headings (## for major sections)
## Subsection Headings

**Tool names and important terms** in bold
`Code examples` and `commands` in backticks
- Bullet points for lists
- Numbered lists for step-by-step processes
```

### Cross-Reference Formatting

**Standard patterns:**

**Navigation:**
```markdown
Back to: [Section name](../path/to/document.md)
Next: [Section name → Section title](../path/to/document.md)
```

**Related Information:**
```markdown
**Related Reading:**
- [Concept name](../path/to/concept.md) — Brief description
- [Tool guide](../path/to/tool.md) — How to use

**Tool Integration:**
- [Tool name](../development-tools/tool.md) — Primary usage
- [Setup guide](../development-tools/setup.md) — Configuration
```

### Code and Command Examples

**Format consistently:**
```markdown
**Terminal commands:**
```bash
npm install package-name
npm run build
```

**Configuration examples:**
```toml
# wrangler.toml
name = "my-project"
compatibility_date = "2023-10-30"
```

**API examples:**
```typescript
// TypeScript/JavaScript
const response = await fetch('/api/endpoint');
const data = await response.json();
```
```

---

## Quick Reference

### Common Cross-Reference Patterns

| Source Section | Target Type | Link Format |
|---------------|-------------|-------------|
| Workflow phases | Tools | [Tool name](../development-tools/tool.md) — Usage description |
| Workflow phases | Other phases | [Phase name](../workflow/phase-name.md) — What comes next |
| Tool docs | Workflow phases | [Phase X](../workflow/phase-x.md) — When to use this tool |
| Concepts | Implementation | [Related guide](../path/to/guide.md) — Practical application |
| Business content | Technical | [Tech stack](../core-technologies.md) — Implementation details |

### File Naming Conventions

- Use kebab-case for file names: `phase-1-planning.md`
- Keep descriptive but concise names: `glm-coding-plan.md` (not `glm-coding-plan-detailed-guide.md`)
- Use `README.md` for directory indexes
- Avoid spaces and special characters in file names

### Link Verification Commands

```bash
# Check for broken links (if you have linkchecker installed)
linkchecker --check-extern docs/

# Or manually verify key navigation paths:
# - Main README → all major sections
# - Workflow phases → next/previous phases
# - Tool docs → related workflow phases
# - All cross-references in modified files
```

---

## Questions and Support

**If you need help with contributing:**
1. Check existing issues for similar discussions
2. Open a new issue with your question
3. Tag maintainers for specific guidance

**For urgent issues:**
- Critical broken links
- Outdated pricing information
- Security-related concerns

**For enhancement discussions:**
- New tool recommendations
- Workflow improvements
- Documentation structure changes

---

Thank you for contributing to the Awesome Vibecoding Guide! Your improvements help make this resource more valuable for the entire community.

**Back to index:** [Top‑level README](../README.md)
