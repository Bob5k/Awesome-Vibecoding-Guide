# Cross-Reference Guide

Navigate related topics across the documentation. This guide shows how concepts connect and where to find related information.

## Major Concept Maps

### AI-Assisted Development Workflow

```
Context Management
├─→ Basic Setup (context-management/README.md)
├─→ Advanced Scenarios (context-management/advanced-scenarios.md)
└─→ Troubleshooting (troubleshooting/recovery-patterns.md)

Prompting & Iteration
├─→ Basic Prompting (prompting/README.md)
├─→ Common Prompts Cheat Sheet (development-tools/cheat-sheets/common-prompts.md)
└─→ Workflow Integration (workflow/README.md)

Quality Assurance
├─→ Accessibility (quality-standards/accessibility.md)
├─→ SEO (quality-standards/seo.md)
├─→ Performance (quality-standards/performance.md)
└─→ Testing (workflow/phase-3-testing-debugging.md)
```

### Business & Project Management

```
Project Setup
├─→ Philosophy (introduction/philosophy.md)
├─→ Core Technologies (core-technologies.md)
├─→ Tech Stack Decision (tech-stacks/README.md)
└─→ Tool Selection (development-tools/decision-matrix.md)

Client Work
├─→ Client Management (business-model/client-management.md)
├─→ Maintenance Strategy (business-model/maintenance-strategy.md)
├─→ ROI Tracking (business-model/roi-tracking.md)
└─→ Quality Standards (quality-standards/README.md)
```

## Topic Index

### By Development Phase

**Planning & Setup:**
- [Philosophy & Principles](./introduction/philosophy.md)
- [Core Technologies Overview](./core-technologies.md)
- [Tool Selection Matrix](./development-tools/decision-matrix.md)
- [Context Management Setup](./context-management/README.md)

**Implementation:**
- [Phase 1: Planning](./workflow/phase-1-planning.md)
- [Phase 2: Implementation](./workflow/phase-2-implementation.md)
- [Common Prompts](./development-tools/cheat-sheets/common-prompts.md)
- [Git Strategies](./workflow/git-strategies.md)

**Testing & Deployment:**
- [Phase 3: Testing & Debugging](./workflow/phase-3-testing-debugging.md)
- [Performance Standards](./quality-standards/performance.md)
- [Accessibility Testing](./quality-standards/accessibility.md)
- [SEO Verification](./quality-standards/seo.md)

**Maintenance:**
- [Maintenance Strategy](./business-model/maintenance-strategy.md)
- [Recovery Patterns](./troubleshooting/recovery-patterns.md)
- [ROI Tracking](./business-model/roi-tracking.md)

### By Technology

**Astro:**
- [Core Technologies](./core-technologies.md)
- [Performance Optimization](./quality-standards/performance.md) (Astro-specific section)
- [Accessibility Patterns](./quality-standards/accessibility.md) (Astro components)
- [SEO Setup](./quality-standards/seo.md) (Astro patterns)
- [Internationalization](./tech-stacks/internationalization.md)

**Cloudflare:**
- [Cloudflare Pages](./hosting-tools/cloudflare-pages.md)
- [Cloudflare CLI Cheat Sheet](./development-tools/cheat-sheets/cloudflare-cli.md)
- [Core Technologies](./core-technologies.md) (D1, KV, R2 sections)

**Git:**
- [Git Strategies](./workflow/git-strategies.md)
- [Git Commands Cheat Sheet](./development-tools/cheat-sheets/git-commands.md)
- [Recovery Patterns](./troubleshooting/recovery-patterns.md)

**AI Tools:**
- [Tool Decision Matrix](./development-tools/decision-matrix.md)
- [Context Management](./context-management/README.md)
- [Advanced Scenarios](./context-management/advanced-scenarios.md)

### By Problem Type

**Performance Issues:**
1. [Performance Standards](./quality-standards/performance.md) - Core Web Vitals optimization
2. [Testing & Debugging](./workflow/phase-3-testing-debugging.md) - Performance tab usage
3. [Debugging Commands](./development-tools/cheat-sheets/debugging-commands.md) - Performance profiling

**Accessibility Problems:**
1. [Accessibility Standards](./quality-standards/accessibility.md) - WCAG compliance guide
2. [Testing & Debugging](./workflow/phase-3-testing-debugging.md) - Accessibility testing
3. [SEO](./quality-standards/seo.md) - Accessibility/SEO overlap

**SEO Issues:**
1. [SEO Standards](./quality-standards/seo.md) - Complete SEO guide
2. [Performance Standards](./quality-standards/performance.md) - Core Web Vitals affect SEO
3. [Internationalization](./tech-stacks/internationalization.md) - Multilingual SEO

**Context/AI Issues:**
1. [Context Management](./context-management/README.md) - Basic setup
2. [Advanced Scenarios](./context-management/advanced-scenarios.md) - Complex projects
3. [Recovery Patterns](./troubleshooting/recovery-patterns.md) - Context loss recovery
4. [Common Prompts](./development-tools/cheat-sheets/common-prompts.md) - Better prompts

**Git Problems:**
1. [Recovery Patterns](./troubleshooting/recovery-patterns.md) - Git recovery strategies
2. [Git Commands Cheat Sheet](./development-tools/cheat-sheets/git-commands.md) - Command reference
3. [Git Strategies](./workflow/git-strategies.md) - Best practices

**Deployment Issues:**
1. [Cloudflare CLI Cheat Sheet](./development-tools/cheat-sheets/cloudflare-cli.md) - Wrangler commands
2. [Cloudflare Pages](./hosting-tools/cloudflare-pages.md) - Deployment guide
3. [Recovery Patterns](./troubleshooting/recovery-patterns.md) - Emergency rollback

### By User Type

**Beginners:**
1. [Philosophy](./introduction/philosophy.md) - Start here
2. [Core Technologies](./core-technologies.md) - Tech stack overview
3. [Tool Decision Matrix](./development-tools/decision-matrix.md) - Choose free tools
4. [Context Management](./context-management/README.md) - Essential setup
5. [Workflow Overview](./workflow/README.md) - Development process

**Freelancers:**
1. [Client Management](./business-model/client-management.md) - Client relationships
2. [ROI Tracking](./business-model/roi-tracking.md) - Track profitability
3. [Maintenance Strategy](./business-model/maintenance-strategy.md) - Ongoing revenue
4. [Quality Standards](./quality-standards/README.md) - Deliver professional work
5. [Tool Decision Matrix](./development-tools/decision-matrix.md) - Cost-effective tools

**Agencies:**
1. [Advanced Context Scenarios](./context-management/advanced-scenarios.md) - Team collaboration
2. [Tool Decision Matrix](./development-tools/decision-matrix.md) - Team tool selection
3. [Quality Standards](./quality-standards/README.md) - Client deliverables
4. [Workflow](./workflow/README.md) - Team processes

## Frequently Needed Combinations

### "Set up new Astro + Cloudflare project"
1. [Core Technologies](./core-technologies.md)
2. [Context Management](./context-management/README.md)
3. [Cloudflare Pages](./hosting-tools/cloudflare-pages.md)
4. [Git Strategies](./workflow/git-strategies.md)

### "Improve site performance"
1. [Performance Standards](./quality-standards/performance.md)
2. [SEO Standards](./quality-standards/seo.md) (Core Web Vitals section)
3. [Testing & Debugging](./workflow/phase-3-testing-debugging.md)
4. [Debugging Commands](./development-tools/cheat-sheets/debugging-commands.md)

### "Make site accessible"
1. [Accessibility Standards](./quality-standards/accessibility.md)
2. [Testing & Debugging](./workflow/phase-3-testing-debugging.md) (Accessibility testing)
3. [Client Management](./business-model/client-management.md) (Explaining value)

### "Optimize for search engines"
1. [SEO Standards](./quality-standards/seo.md)
2. [Performance Standards](./quality-standards/performance.md) (Core Web Vitals)
3. [Accessibility Standards](./quality-standards/accessibility.md) (SEO overlap)
4. [Internationalization](./tech-stacks/internationalization.md) (If multilingual)

### "Recover from mistakes"
1. [Recovery Patterns](./troubleshooting/recovery-patterns.md)
2. [Git Commands Cheat Sheet](./development-tools/cheat-sheets/git-commands.md)
3. [Debugging Commands](./development-tools/cheat-sheets/debugging-commands.md)

### "Add multilingual support"
1. [Internationalization](./tech-stacks/internationalization.md)
2. [SEO Standards](./quality-standards/seo.md) (Hreflang section)
3. [Client Management](./business-model/client-management.md) (Pricing i18n)

### "Choose cost-effective tools"
1. [Tool Decision Matrix](./development-tools/decision-matrix.md)
2. [Philosophy](./introduction/philosophy.md)
3. [ROI Tracking](./business-model/roi-tracking.md)

### "Handle complex project structure"
1. [Advanced Context Scenarios](./context-management/advanced-scenarios.md)
2. [Context Management](./context-management/README.md)
3. [Git Strategies](./workflow/git-strategies.md)

## Quick Reference Links

### Cheat Sheets (Quick Copy-Paste)
- [Git Commands](./development-tools/cheat-sheets/git-commands.md)
- [Cloudflare CLI](./development-tools/cheat-sheets/cloudflare-cli.md)
- [Common Prompts](./development-tools/cheat-sheets/common-prompts.md)
- [Debugging Commands](./development-tools/cheat-sheets/debugging-commands.md)

### Standards (Quality Checklist)
- [Accessibility](./quality-standards/accessibility.md)
- [SEO](./quality-standards/seo.md)
- [Performance](./quality-standards/performance.md)

### Workflow (Process Guides)
- [Phase 1: Planning](./workflow/phase-1-planning.md)
- [Phase 2: Implementation](./workflow/phase-2-implementation.md)
- [Phase 3: Testing & Debugging](./workflow/phase-3-testing-debugging.md)
- [Git Strategies](./workflow/git-strategies.md)

### Business (Client & Revenue)
- [Client Management](./business-model/client-management.md)
- [Maintenance Strategy](./business-model/maintenance-strategy.md)
- [ROI Tracking](./business-model/roi-tracking.md)

## Learning Paths

### Path 1: Complete Beginner
```
1. Introduction → Philosophy
2. Core Technologies
3. Tool Decision Matrix (choose free tools)
4. Context Management
5. Workflow Overview
6. Phase 1: Planning (start small project)
7. Phase 2: Implementation
8. Phase 3: Testing
9. Cheat Sheets (as reference)
```

### Path 2: Experienced Developer (New to AI)
```
1. Philosophy (understand approach)
2. Context Management (critical!)
3. Tool Decision Matrix (choose based on budget)
4. Workflow Overview
5. Common Prompts (effective AI usage)
6. Quality Standards (maintain professionalism)
7. Advanced Scenarios (when needed)
```

### Path 3: Freelancer Starting Client Work
```
1. Philosophy
2. Business Model → Client Management
3. Quality Standards (all three)
4. Workflow (all phases)
5. Maintenance Strategy
6. ROI Tracking
7. Tool Decision Matrix (cost-effective choices)
```

### Path 4: Agency/Team
```
1. Tool Decision Matrix (team tools)
2. Advanced Context Scenarios (team collaboration)
3. Quality Standards (deliverables)
4. Workflow (team processes)
5. Git Strategies (team conventions)
6. Business Model (all docs)
```

## Where to Go Next

**Just finished a section? Here's what's related:**

**Read Philosophy?** → Next: Core Technologies, Tool Decision Matrix

**Read Core Technologies?** → Next: Context Management, Workflow Overview

**Read Context Management?** → Next: Workflow Phase 1, Common Prompts

**Read Quality Standards?** → Next: Testing & Debugging, Client Management

**Read Workflow?** → Next: Git Strategies, Testing & Debugging

**Read Business Model?** → Next: Quality Standards, ROI Tracking

**Read Cheat Sheets?** → Keep open as reference while working

**Read Troubleshooting?** → Bookmark for when issues arise

**Read Advanced Scenarios?** → Come back when projects grow complex

---

**Remember:** You don't need to read everything linearly. Use this guide to jump to relevant topics as you need them.
