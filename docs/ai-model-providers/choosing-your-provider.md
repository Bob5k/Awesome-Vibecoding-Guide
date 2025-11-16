# Choosing Your AI Provider

## Introduction

Selecting the right AI provider is crucial for an effective vibecoding workflow. This guide helps you navigate the landscape of AI model providers, comparing costs, features, privacy, and use cases to find the perfect fit for your needs and budget.

The AI provider landscape has matured significantly, offering options from budget-friendly to enterprise-grade. Whether you're a hobbyist working on side projects or a professional developer building commercial applications, there's a provider that matches your requirements.

**Key factors to consider:**
- **Budget**: What can you afford monthly?
- **Privacy**: Are you working with sensitive or proprietary code?
- **Rate Limits**: How intensively will you use the AI assistant?
- **Model Variety**: Do you need access to multiple models for different tasks?
- **Integration**: Which development tools (Claude Code CLI, Droid CLI, etc.) will you use?

---

## Quick Comparison Matrix

| Provider | Monthly Cost | Rate Limits | Privacy | Model Access | Best For |
|----------|-------------|-------------|---------|--------------|----------|
| **GLM Lite** | $3-6 | 120 prompts/5h | Good | GLM-4.6 | Best value-to-price ratio |
| **GLM Lite + NanoGPT** | $11 | 120 prompts/5h | Good | GLM-4.6 | Budget coding |
| **GLM Pro** | $15-30* | 600 prompts/5h | Good | GLM-4.6 | Regular development |
| **Synthetic Standard** | $10-20* | 135 prompts/5h | Excellent | 20+ models | Privacy & flexibility |
| **GLM Max** | $60 | 2400 prompts/5h | Good | GLM-4.6 | Heavy usage (overkill) |
| **Synthetic Pro** | $60 | 1350 prompts/5h | Excellent | 20+ models | Heavy usage (recommended) |
| **nanoGPT** | $8 | 60k req/month | Poor | Many models | Backup/experimentation only |
| **Claude Pro** | ~$20 | Weekly limits | Excellent | Claude models | Low usage hobbyists** |
| **OpenRouter** | Pay-per-use / Free models | Varies | Varies | Many models | Unreliable |
| **Chutes.ai** | Pay-per-use / Plans from 3$ | Varies | Poor | Many models | Unreliable |

\* First purchase discount available
\*\* Despite similar price point, tiny quota and weekly limits make it poor value vs alternatives

---

## Budget-Based Recommendations

### 💎 Tier 1: $3-6/month — Cheapest & Most Reliable

**Primary Recommendation: [GLM Coding Plan Standard](glm-coding-plan.md)**

- **Cost**: $3 first purchase, $6 standard monthly
- **Rate Limits**: 120 prompts per 5 hours
- **Model**: GLM-4.6 (Sonnet 4-level quality)
- **Best For**: Hobby projects, learning, occasional coding

**Why this is the best value:**
- Absolute best value-to-price ratio in the market
- Reliable, established provider with clear policies
- Quality on par with much more expensive alternatives
- Hard to hit limits even with moderate usage
- Perfect for students and hobbyists

**Use Cases:**
- Side projects and personal development
- Learning to code with AI assistance
- Weekend coding sessions
- Budget-conscious developers
- Testing vibecoding workflows

**Integration:**
- Works excellently with [Claude Code CLI](../development-tools/recommended-tools/claude-code-cli.md)
- Most efficient with [Droid CLI](../development-tools/recommended-tools/droid-cli.md) for planning

**When to upgrade:** If you find yourself consistently hitting the 120 prompts/5h limit across multiple sessions

[Sign up with referral link](https://z.ai/subscribe?ic=CUEFJ9ALMX) (10% discount)

---

### 🎯 Tier 2: ~$11/month — Budget Friendly for Heavy Usage

**Primary Recommendation: GLM Lite + nanoGPT Combination**

**Strategy:**
1. **Primary**: GLM Coding Plan Lite ($11/month) — 120 prompts per 5 hours
2. **Backup**: [nanoGPT](honorable-mentions/nanogpt.md) ($8/month with [referral](https://nano-gpt.com/invite/UfrjxgDi) 5% off) — 60,000 requests/month

**How to use this combo:**
- Use GLM for majority of your work (reliable, fast, private)
- Switch to nanoGPT when you hit GLM limits
- nanoGPT acts as overflow capacity for heavy sessions

**Total Cost:** ~$11/month (if you only need GLM Lite) or ~$19/month (if adding nanoGPT)

**Important Drawbacks:**
- nanoGPT models are quantized at fp8 (slightly reduced quality)
- nanoGPT has privacy concerns (see [detailed analysis](honorable-mentions/nanogpt.md))
- Don't use nanoGPT for sensitive/proprietary code

**Best For:**
- Heavy users on tight budgets
- Developers who occasionally need burst capacity
- Projects where code will be public anyway
- Learning and experimentation

**Alternative:** Just stick with GLM Lite — for most users, paying for nanoGPT is unnecessary as GLM limits are generous

---

### 🚀 Tier 3: $15-30/month — Privacy & Flexibility

**Two Strong Options:**

#### Option A: [Synthetic.new Standard](synthetic-new.md)
- **Cost**: $10 first month ([referral link](https://synthetic.new/?referral=IDyp75aoQpW9YFt)), $20 thereafter
- **Rate Limits**: 135 prompts per 5 hours
- **Models**: 20+ frontier open-source models
- **Privacy**: Excellent — self-hosted on US infrastructure

**Why choose Synthetic:**
- Privacy-first approach for sensitive code
- Multiple models for different use cases
- 200 tokens/sec performance (2x faster than GLM)
- No weekly limits, only 5h rolling windows
- Model experimentation without switching providers

**Best For:**
- Privacy-conscious developers
- Professional development with sensitive code
- Developers who want model variety
- Those prioritizing speed and reliability

#### Option B: [GLM Coding Plan Pro](glm-coding-plan.md)
- **Cost**: $15 first purchase, $30 standard monthly
- **Rate Limits**: 600 prompts per 5 hours
- **Model**: GLM-4.6
- **Privacy**: Good — established provider

**Why choose GLM Pro:**
- Best cost-effectiveness for single-model usage
- 5x higher limits than Lite plan
- Very hard to hit even with 2-5 parallel agents
- Simpler if you don't need model variety

**Important Note on First Purchase Discount:**
- $15 applies only to FIRST purchase of monthly/quarterly/yearly plans
- All subsequent charges are $30
- Quarterly/yearly plans preserve the discount rate

**Decision Guide:**
- **Choose Synthetic** if: Privacy matters, want model flexibility, prefer speed
- **Choose GLM Pro** if: Want best value, don't need multiple models, prefer simplicity

#### Honorable Mention: Claude Pro Subscription (~$20)*

**NOT RECOMMENDED** despite being at similar price point.

**Why to avoid:**
- Tiny quota compared to Synthetic/GLM at same price
- Weekly rate limits (vs 5h rolling window)
- Insufficient for serious development work
- Poor value-to-price ratio

**When it might make sense:**
- You desperately need Claude's reasoning for complex architecture
- You're doing occasional prototyping only
- Budget doesn't matter and you want "the best"

See [detailed analysis](honorable-mentions/claude-subscription.md) for why even the author dropped it in favor of GLM.

**Better approach:** Use Claude Code CLI tool with GLM as provider instead of Claude subscription.

---

### ⚡ Tier 4: ~$60/month — Power Users & Heavy Usage

**Primary Recommendation: [Synthetic.new Pro Plan](synthetic-new.md)**

- **Cost**: $60/month
- **Rate Limits**: 1,350 prompts per 5 hours (10x Standard)
- **Models**: All 20+ frontier models included
- **Privacy**: Excellent

**Why Synthetic Pro over GLM Max:**
- Same price point ($60)
- More than sufficient limits (1,350 vs 2,400)
- Multiple models vs single GLM model
- Better privacy with self-hosted infrastructure
- Faster performance (200 tokens/sec)

**Alternative: GLM Max Plan**
- **Cost**: $60/month
- **Rate Limits**: 2,400 prompts per 5 hours
- **Model**: GLM-4.6 only

**Only choose GLM Max if:**
- You genuinely need 2,400 prompts/5h (unlikely even with many agents)
- You prefer single-model consistency
- You don't value model variety

**Reality Check:**
Even on GLM Pro (600 prompts/5h), the author hasn't hit limits with multiple parallel agents. The 2,400 limit is overkill for 99% of users.

**Best For:**
- Professional development teams
- Agencies building for clients
- Developers working 8+ hours daily with AI
- Those running many parallel agents
- Mission-critical development workflows

**Cost Comparison:**
- Claude Code Max20: €200+ per month (with EU VAT)
- Codex Pro: €229 per month (EU with VAT)
- Synthetic Pro: $60 per month
- GLM Max: $60 per month

The value proposition is clear: comparable or better functionality at 70% lower cost.

---

## Budget Provider Alternatives

### nanoGPT — Budget Aggregator

**Cost:** $8/month ([5% off with referral](https://nano-gpt.com/invite/UfrjxgDi))
**Rate Limits:** 60,000 requests per month
**Models:** Various aggregated models

**Critical Limitations:**
- **Privacy Concerns**: Routes through third-party providers
- **fp8 Quantization**: Slightly reduced model quality
- **Data Security**: No guarantee code won't be used for training
- **Not self-hosted**: Multiple parties in request chain

**Best Use Cases:**
- Backup when primary provider is down
- Model exploration and experimentation
- Non-sensitive public projects
- Hobby development where privacy isn't critical

**NOT Recommended For:**
- Proprietary code development
- Client work with sensitive data
- Professional commercial applications
- Privacy-conscious developers

See [detailed nanoGPT analysis](honorable-mentions/nanogpt.md) for complete privacy breakdown.

### OpenRouter — Multi-Provider Gateway

**Cost:** Pay-per-use (varies by model)
**Models:** Access to many providers

**Limitations:**
- Inconsistent performance
- No rate limit guarantees
- Complex billing
- Reliability issues

See [OpenRouter analysis](honorable-mentions/openrouter.md) for details.

### Chutes.ai — Budget Platform

**Not recommended** due to reliability issues.

See [Chutes analysis](honorable-mentions/chutes.ai.md) for details.

---

## Use Case Recommendations

### For Hobby Developers / Learning
**Recommendation:** GLM Standard ($3-6/month)
- Best value for occasional use
- Quality comparable to expensive alternatives
- Perfect for learning vibecoding

### For Privacy-Focused Development
**Recommendation:** Synthetic Standard or Pro
- Self-hosted models on US infrastructure
- Clear privacy policies
- No third-party routing
- Ideal for proprietary code

### For Budget-Conscious Heavy Users
**Recommendation:** GLM Lite + nanoGPT combo (~$11-19/month)
- Use GLM as primary (private, reliable)
- nanoGPT as overflow (public projects only)
- Cost-effective for high usage

### For Professional Development
**Recommendation:** Synthetic Standard ($20) or GLM Pro ($30)
- Synthetic: Better if privacy matters, want flexibility
- GLM Pro: Better if cost-effectiveness is priority
- Both suitable for client work

### For Teams / Agencies
**Recommendation:** Synthetic Pro ($60/month)
- Sufficient limits for team use
- Multiple models for different tasks
- Privacy guarantees for client work
- Better value than GLM Max at same price

### For Model Experimentation
**Recommendation:** Synthetic Standard ($20)
- 20+ models under one subscription
- Test different approaches without switching providers
- No additional costs for trying new models

---

## Provider Deep Dives

For detailed information about each provider:

**Primary Providers:**
- [Synthetic.new](synthetic-new.md) — Privacy-first, multiple models, fast performance
- [GLM Coding Plan](glm-coding-plan.md) — Cost-effective, reliable, Sonnet 4-level quality

**Budget Alternatives:**
- [nanoGPT](honorable-mentions/nanogpt.md) — Aggregator with privacy concerns
- [OpenRouter](honorable-mentions/openrouter.md) — Multi-provider gateway
- [Chutes.ai](honorable-mentions/chutes.ai.md) — Budget platform (unreliable)

**Honorable Mentions:**
- [Claude Subscription](honorable-mentions/claude-subscription.md) — Premium option, poor value
- [Honorable Mentions Overview](honorable-mentions/README.md) — All alternatives

---

## Integration Guidance

### Connecting to Development Tools

**Claude Code CLI:**
- Works with all providers via API configuration
- Fastest with GLM according to testing
- See [Claude Code CLI setup](../development-tools/recommended-tools/claude-code-cli.md)

**Droid CLI:**
- Most efficient planning architecture
- Best results with GLM Coding Plan
- See [Droid CLI setup](../development-tools/recommended-tools/droid-cli.md)

**MCP Servers:**
- [Context7 MCP](../development-tools/mcp-servers/context7-mcp.md) — Documentation access
- [DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) — Browser automation
- [Sequential Thinking MCP](../development-tools/mcp-servers/sequential-thinking-mcp.md) — Enhanced reasoning

All providers work with standard MCP servers through their APIs.

---

## Migration Strategy

### Starting Free → First Paid Subscription

**Best First Step:** GLM Standard ($3-6)
- Lowest commitment
- Learn if AI-assisted development works for you
- Upgrade when you hit limits

### From Budget to Professional

**GLM Standard → Synthetic Standard:**
- When privacy becomes important
- When you want to try multiple models
- When speed matters (200 tokens/sec)

**GLM Standard → GLM Pro:**
- When you consistently hit 120 prompts/5h
- When you start running parallel agents
- When you stick with single model

### From Professional to Power User

**Synthetic Standard → Synthetic Pro:**
- Team growth requiring more capacity
- Running many parallel workflows
- Professional agency work

**GLM Pro → Synthetic Pro (not GLM Max):**
- Want model variety for different tasks
- Need privacy guarantees
- 600 prompts/5h isn't enough but 1,350 would be

---

## Key Takeaways

1. **Best Value Overall:** GLM Standard ($3-6) — unbeatable value-to-price ratio
2. **Best for Privacy:** Synthetic Standard/Pro — self-hosted, clear policies
3. **Best for Budget Heavy Usage:** GLM Lite + nanoGPT combo (~$11-19)
4. **Best for Professional Work:** Synthetic Standard ($20) or GLM Pro ($30)
5. **Best for Power Users:** Synthetic Pro ($60) — better than GLM Max at same price

**What to Avoid:**
- Claude Pro subscription (poor value at $20 vs alternatives)
- Chutes.ai (too unreliable)
- Using nanoGPT for sensitive code (privacy concerns)
- GLM Max unless you genuinely need 2,400 prompts/5h (overkill)

**Start Here:**
1. Evaluate your budget and privacy requirements
2. Choose from Tier 1 or 2 recommendations
3. Upgrade when you hit limits or need more features
4. Don't overpay for limits you won't use

Remember: With proper vibecoding technique, the quality gap between providers narrows significantly. Focus on workflow, not just model performance.

---

**Next Steps:**
- [Phase 0: Vibecoder Preparation](../workflow/phase-0-vibecoder-preparation.md) — Tool selection guide
- [Development Tools Overview](../development-tools/README.md) — IDE and CLI setup
- [Core Technologies](../core-technologies.md) — Tech stack recommendations

Back: [AI Model Providers](./README.md)
