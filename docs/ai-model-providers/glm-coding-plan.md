# GLM Coding Plan — Main LLM 🧠

## Pricing
- Lite: $3/month — 120 prompts per 5 hours
- Pro: $15/month — 600 prompts per 5 hours
- Max: $30/month — 2,400 prompts per 5 hours
- Practicality of limits: Very hard to hit even with 2–5 parallel agents on Pro and Max plans
- Note: prices are for first month, but can be preserved on this level aswell for quarterly or yearly-basis plans
- Note2: I'm on Max plan currently, but haven't hit limits when I was on Pro plan for over a month in the past aswell
- **IMPORTANT:** Currently the fastest combo of working with GLM is to conenct it to Claude Code. However - the most efficient combo is to connect it to Droid CLI - due to superior planning and following the plan architecture of Droid.
- Optional: 10% off referral link (disclosure): <https://z.ai/subscribe?ic=CUEFJ9ALMX>

## Why GLM?
- Lowest cost while keeping quality around Sonnet 4 level
- State‑of‑the‑art open‑source model
- Can autonomously resolve bugs for 10–15 minutes without intervention
- Handles complex projects (Next.js + complex database + backend)
- Works quite well with modern web development stacks (Svelte, React, Next.js, Astro, D1 databases, Cloudflare Wrangler files, etc.)

## Cost comparison
- Claude Code Max20: €200+ per month (with EU VAT)
- Codex Pro: €229 in EU with VAT per month
- Most alternatives will be more expensive than GLM considering the fact that GLM Coding Plan efficiently gives you A TON of tokens per 5h, not even talking about per month.

## Recommended Workflow Integration

**Best Used In:**
- [Phase 1: Planning](../workflow/phase-1-planning.md) - PRD refinement and architecture discussions
- [Phase 2: Development](../workflow/phase-2-development.md) - Code generation and debugging
- [Core Technologies Implementation](../core-technologies.md) - Astro + Tailwind development

**Budget Considerations:**
- Compare with [free alternatives](./honorable-mentions/README.md) before upgrading
- See [Phase 0 tool selection](../workflow/phase-0-vibecoder-preparation.md) for upgrade timing

**Integration Setup:**
- [Droid CLI](../development-tools/recommended-tools/droid-cli.md) — Most efficient integration for planning and architecture
- [Claude Code CLI](../development-tools/recommended-tools/claude-code-cli.md) — Fastest working combination
- [Context7 MCP](../development-tools/mcp-servers/context7-mcp.md) — Documentation access during development

**Workflow Phases by Usage:**

**Phase 0 (Preparation):**
- Evaluate against [free alternatives](../workflow/phase-0-vibecoder-preparation.md#free-option-perfect-for-getting-started)
- Upgrade from [budget options](../workflow/phase-0-vibecoder-preparation.md#budget-option-professional-grade) when hitting limits

**Phase 1 (Planning):**
- Use for PRD refinement and feature breakdown
- Combine with [OpenSpec CLI](../development-tools/recommended-tools/openspec-cli.md) for structured planning
- Architecture discussions for [Core Technologies](../core-technologies.md) stack

**Phase 2 (Development):**
- Daily coding assistance and debugging
- [DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) integration for automated testing
- Component generation for Astro + Tailwind projects

**Phase 3 (Testing & Debugging):**
- Bug analysis and resolution
- Code review and optimization
- Integration with [testing workflows](../workflow/phase-3-testing-debugging.md)

Back: [AI Model Providers](./README.md)
