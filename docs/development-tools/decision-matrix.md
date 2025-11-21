# Tool Selection Decision Matrix

## Philosophy Reminder

This guide operates on a **cost-effectiveness principle**:
- **Target:** 80-99% of functionality at free or low cost
- **Source of truth:** This guide itself (proven in commercial production)
- **Approach:** Start free, upgrade only when justified by clear ROI

**The expensive-tool trap:**
- $200/month Claude Code subscription isn't necessary for most freelancers
- Free/budget tools can deliver professional results
- Cost savings compound quickly (save $2,400/year = client you don't need to find)

**When this guide differs from popular advice:**
- Popular advice says "use Cursor Pro" ($20/mo)
- This guide says "try Qwen CLI (free) first"
- **Reason:** Most developers never need the premium features

## Decision Framework

Use this four-factor framework when choosing tools:

### 1. Cost-Effectiveness
**Question:** What's the real cost per value delivered?

**Calculation:**
```
Cost-effectiveness = (Features you'll actually use × Reliability) / Total cost
```

**Example:**
- **Claude Code:** $200/mo, 100 features, use 20 → 20/200 = 0.1
- **Qwen CLI:** Free, 40 features, use 30 → 30/0 = ∞

**Winner:** Often the simpler, cheaper tool

### 2. Feature Completeness
**Question:** Does it have what I actually need (not what sounds cool)?

**Essential features checklist:**
- ✅ Code generation
- ✅ Context awareness
- ✅ File editing
- ✅ Error understanding
- ✅ Multi-file refactoring (nice to have)

**Premium features (rarely needed):**
- ❌ Voice coding
- ❌ Real-time collaboration
- ❌ Advanced analytics
- ❌ Team management

### 3. Reliability
**Question:** Does it work consistently when I need it?

**Reliability factors:**
- Uptime (API availability)
- Error handling
- Rate limiting
- Local fallback options

**Red flags:**
- Frequent "Rate limit exceeded" errors
- API downtime during your work hours
- No offline mode
- Vague error messages

### 4. Integration
**Question:** Does it fit my existing workflow?

**Integration checklist:**
- Works with my current IDE
- Supports my tech stack
- Compatible with my git workflow
- Doesn't require workflow changes
- Has escape hatches (not locked in)

## Coding Agents Comparison

Detailed comparison of AI coding assistants:

| Feature | Qwen CLI | GLM | Claude Code | Cursor |
|---------|----------|-----|-------------|--------|
| **Monthly Cost** | $0 | $15 | $200 | $20 |
| **Annual Cost** | $0 | $180 | $2,400 | $240 |
| **Model** | Qwen 2.5 72B | GLM-4-Plus | Claude Sonnet 4 | Multiple |
| **Local/Remote** | Remote (Factory API) | Remote (GLM API) | Remote (Anthropic) | Remote |
| **Context Window** | 128k tokens | 128k tokens | 200k tokens | Varies |
| **Code Quality** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Multi-file Editing** | ✅ Yes | ✅ Yes | ✅ Yes (best) | ✅ Yes |
| **IDE Integration** | CLI only | CLI only | VS Code (official) | Built-in IDE |
| **File Search** | ✅ Grep/glob | ✅ Grep/glob | ✅ Advanced | ✅ Advanced |
| **Terminal Commands** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **Git Integration** | Manual | Manual | Automatic | Automatic |
| **Learning Curve** | Low | Low | Medium | Low |
| **Offline Mode** | ❌ No | ❌ No | ❌ No | ❌ No |
| **Rate Limits** | Generous | Moderate | Very generous | Varies by plan |
| **BYOK (Bring Your Own Key)** | N/A | N/A | ❌ No | ✅ Yes |

### Qwen CLI (Free via Factory AI)

**Best for:**
- Beginners learning AI-assisted coding
- Budget-conscious freelancers
- Side projects and learning
- Developers who want CLI workflow

**Pros:**
- ✅ Completely free (Factory AI provides free tier)
- ✅ Powerful model (Qwen 2.5 72B)
- ✅ Large context window (128k tokens)
- ✅ Multi-file editing
- ✅ Simple CLI interface
- ✅ No credit card required

**Cons:**
- ❌ CLI only (no IDE integration)
- ❌ Rate limits (but generous for free)
- ❌ Requires manual git commands
- ❌ No advanced features (code review, analytics, etc.)

**When to use:**
- Starting out with AI coding
- Budget is $0
- Comfortable with CLI
- Don't need IDE integration

**Setup:**
```bash
# Install
npm install -g qwen-cli

# Configure
qwen config set apiKey YOUR_FACTORY_API_KEY

# Use
qwen chat "Create a contact form component"
```

**Real-world example:**
> "I built my entire SaaS MVP using Qwen CLI (free). Only upgraded to GLM when I started billing clients and needed faster responses." - Freelancer using this guide

### GLM ($15/month)

**Best for:**
- Freelancers billing clients
- Developers who want good value
- Production work needing reliability
- Projects requiring consistent quality

**Pros:**
- ✅ Affordable ($15/mo)
- ✅ Excellent model (GLM-4-Plus)
- ✅ Good rate limits
- ✅ Reliable API
- ✅ Large context window
- ✅ Consistent responses

**Cons:**
- ❌ CLI only (no IDE integration)
- ❌ Requires manual git commands
- ❌ Limited advanced features
- ❌ Chinese company (if that matters for your clients)

**When to upgrade from Qwen:**
- You're billing clients and can expense it
- You hit Qwen's rate limits
- You need more reliable/faster responses
- You can justify $15/mo ($0.50/day)

**ROI calculation:**
```
$15/month = $0.50/day
If GLM saves you 15 minutes/day
Your time worth $40/hour
Savings: (15/60) × $40 = $10/day
ROI: $10/day - $0.50/day = $9.50/day profit
```

### Claude Code ($200/month)

**Best for:**
- Agencies with multiple developers
- High-value enterprise projects
- Teams needing best-in-class AI
- Developers billing $150+/hour

**Pros:**
- ✅ Best code quality (Claude Sonnet 4)
- ✅ Excellent context understanding
- ✅ Native VS Code extension
- ✅ Advanced multi-file operations
- ✅ Very generous rate limits
- ✅ Professional support
- ✅ Enterprise features

**Cons:**
- ❌ Expensive ($200/mo = $2,400/year)
- ❌ Overkill for most freelancers
- ❌ Locked to Anthropic models
- ❌ No BYOK (bring your own key)
- ❌ VS Code only

**When to use:**
- You bill $150+/hour and work 40+ hours/week
- You're an agency billing clients for AI assistance
- You work on complex, high-value projects
- You can expense it as business cost
- You need the absolute best code quality

**When NOT to use:**
- You're a hobbyist
- You're a freelancer billing < $100/hour
- You're building side projects
- You can't directly bill clients for it
- You're cost-conscious

**ROI calculation:**
```
$200/month = $6.67/day (working days)
If Claude Code saves you 30 minutes/day vs. GLM
Your time worth $150/hour
Savings: (30/60) × $150 = $75/day
ROI: $75/day - $6.67/day = $68.33/day profit ✅

But if your time is worth $50/hour:
Savings: (30/60) × $50 = $25/day
ROI: $25/day - $6.67/day = $18.33/day profit
Annual: $18.33 × 250 = $4,582
Is this worth it? Maybe not if GLM gives you 90% of the value for $15/mo.
```

### Cursor ($20/month)

**Best for:**
- Developers who want IDE integration
- Visual Studio Code users
- Developers wanting BYOK option
- Balance between cost and features

**Pros:**
- ✅ Built-in IDE (fork of VS Code)
- ✅ Native AI integration
- ✅ Multi-model support
- ✅ BYOK (use your own API keys)
- ✅ Affordable ($20/mo)
- ✅ Familiar VS Code interface
- ✅ Composer (multi-file editing)
- ✅ Active development

**Cons:**
- ❌ Another IDE to manage
- ❌ $20/mo ongoing cost
- ❌ Limited free tier (50 requests)
- ❌ Rate limits on free tier
- ❌ Some features require Pro

**When to use:**
- You want IDE integration but can't afford Claude Code
- You want BYOK (bring your own API keys)
- You're comfortable switching to new IDE
- $20/mo fits your budget
- You want multi-model access

**BYOK advantage:**
- Use cheaper APIs (GPT-4, Claude API directly)
- Pay only for usage (potentially < $10/mo)
- No rate limits from Cursor
- Full control over API usage

**Real-world example:**
> "I use Cursor with my own Claude API key. Costs me $8-12/month instead of $20. Best of both worlds." - Developer using this guide

### Comparison Matrix: Which Should You Choose?

| Your Situation | Recommended Tool | Monthly Cost | Why |
|----------------|------------------|--------------|-----|
| **Beginner learning** | Qwen CLI | $0 | Free, learn AI coding without commitment |
| **Hobbyist / side projects** | Qwen CLI | $0 | No cost, adequate for personal projects |
| **Freelancer (starting out)** | Qwen CLI → GLM | $0-15 | Start free, upgrade when billing clients |
| **Freelancer (established)** | GLM or Cursor | $15-20 | Justified by client billing |
| **Agency / team** | Claude Code | $200+ | Split cost across team, highest quality |
| **Enterprise work** | Claude Code | $200+ | Expense it, best reliability |
| **Budget-conscious pro** | GLM + Zed | $15 | Maximum value, minimal cost |
| **Want IDE integration** | Cursor | $20 | Best integration for price |
| **Want flexibility** | Cursor BYOK | Variable | Use your own API keys |

## AI Providers Comparison

Where to get API access for AI models:

| Provider | Models | Pricing | Free Tier | Best For |
|----------|--------|---------|-----------|----------|
| **Factory AI** | GLM-4-Plus, Qwen 2.5 | Pay-as-you-go | ✅ Yes (generous) | Budget developers |
| **Synthetic AI** | Multiple SOTA models | Pay-as-you-go | ✅ Yes (moderate) | Multi-model access |
| **GLM Direct** | GLM series | Subscription $15/mo | ❌ No | Direct GLM access |
| **Anthropic** | Claude 3.5/4 | Pay-as-you-go | ✅ Yes (limited) | Claude access |
| **OpenAI** | GPT-4, GPT-4 Turbo | Pay-as-you-go | ✅ Yes ($5 credit) | GPT access |

### Factory AI

**Website:** https://factory.ai

**Models available:**
- GLM-4-Plus (Chinese, excellent quality)
- Qwen 2.5 72B (Chinese, powerful)
- DeepSeek V2 (Chinese, cost-effective)
- And more

**Pricing:**
- **Free tier:** Generous daily limits (adequate for learning/side projects)
- **Paid:** Pay-as-you-go, ~$0.50-2 per 1M tokens
- **No subscription required**

**Best for:**
- Beginners (free tier)
- Cost-conscious developers
- Access to Chinese SOTA models
- Testing multiple models

**Pros:**
- ✅ Free tier sufficient for most hobbyists
- ✅ No credit card for free tier
- ✅ Multiple model options
- ✅ Good API documentation
- ✅ Competitive pricing

**Cons:**
- ❌ Chinese company (if compliance matters)
- ❌ Rate limits on free tier
- ❌ Limited English documentation
- ❌ Newer platform (less established)

### Synthetic AI

**Website:** https://synthetic.ai

**Models available:**
- Multiple SOTA models
- Claude, GPT-4, and more
- Regularly updated model access

**Pricing:**
- **Free tier:** Moderate limits
- **Paid:** Pay-as-you-go
- **Competitive rates**

**Best for:**
- Multi-model workflows
- Testing different models
- Developers wanting flexibility
- Cost-conscious access to premium models

**Pros:**
- ✅ Access to multiple premium models
- ✅ Free tier available
- ✅ Competitive pricing
- ✅ Good API stability

**Cons:**
- ❌ Smaller platform (less support)
- ❌ Limited documentation
- ❌ May not have all latest models

### GLM Direct (Recommended for Freelancers)

**Website:** https://open.bigmodel.cn

**Models:**
- GLM-4-Plus (flagship model)
- GLM-4 (standard model)
- GLM-3-Turbo (faster, cheaper)

**Pricing:**
- **Subscription:** ¥99/month (~$15 USD)
- **Includes:** Sufficient quota for freelance work
- **No usage limits** within quota

**Best for:**
- Freelancers billing clients
- Consistent workload
- Production applications
- Predictable costs

**Pros:**
- ✅ Predictable monthly cost
- ✅ Excellent model quality
- ✅ Good rate limits
- ✅ Direct from source (no intermediary)
- ✅ Reliable API

**Cons:**
- ❌ Chinese website/docs (use translator)
- ❌ Requires Chinese payment method (or virtual card)
- ❌ $15/month commitment
- ❌ Only GLM models

**Setup process:**
1. Visit https://open.bigmodel.cn
2. Register account (use email)
3. Verify identity (passport accepted)
4. Subscribe to ¥99/month plan
5. Get API key
6. Use with CLI tools

### Anthropic (Claude Direct)

**Website:** https://console.anthropic.com

**Models:**
- Claude 3.5 Sonnet (current best)
- Claude 3 Opus (most capable)
- Claude 3 Sonnet (balanced)
- Claude 3 Haiku (fastest)

**Pricing (API):**
- **Sonnet 3.5:** $3/MTok input, $15/MTok output
- **Opus:** $15/MTok input, $75/MTok output
- **Haiku:** $0.25/MTok input, $1.25/MTok output

**Free tier:**
- $5 credit for new users
- Limited rate limits

**Best for:**
- Highest quality code generation
- Complex reasoning tasks
- Using with Cursor BYOK
- When cost isn't primary concern

**Pros:**
- ✅ Highest quality model (Claude)
- ✅ Excellent reasoning
- ✅ Great at following instructions
- ✅ Strong at refactoring
- ✅ Enterprise-grade reliability

**Cons:**
- ❌ Expensive compared to alternatives
- ❌ Rate limits on free tier
- ❌ Small free tier ($5)

**Cost example (realistic freelancer usage):**
```
Typical month:
- 10M input tokens (~20k lines of context per day)
- 2M output tokens (~4k lines generated per day)

Cost:
Input: 10 × $3 = $30
Output: 2 × $15 = $30
Total: $60/month

vs. GLM at $15/month
Savings: $45/month
```

### OpenAI (GPT-4)

**Website:** https://platform.openai.com

**Models:**
- GPT-4 Turbo (latest, most capable)
- GPT-4 (powerful)
- GPT-3.5 Turbo (fast, cheap)

**Pricing:**
- **GPT-4 Turbo:** $10/MTok input, $30/MTok output
- **GPT-4:** $30/MTok input, $60/MTok output
- **GPT-3.5 Turbo:** $0.50/MTok input, $1.50/MTok output

**Free tier:**
- $5 credit for new users (expires after 3 months)
- Rate limits

**Best for:**
- General-purpose AI tasks
- Using with Cursor BYOK
- Balanced cost/quality with GPT-3.5
- When Claude isn't suitable

**Pros:**
- ✅ Well-established platform
- ✅ Good documentation
- ✅ Multiple model options
- ✅ GPT-3.5 Turbo is cost-effective
- ✅ Strong ecosystem

**Cons:**
- ❌ GPT-4 is expensive
- ❌ Code quality often worse than Claude/GLM for dev work
- ❌ Small free tier
- ❌ Strict rate limits

## IDE Comparison

| IDE | Cost | Best For | AI Integration | Speed | Extensions |
|-----|------|----------|----------------|-------|-----------|
| **Zed** | Free | Speed lovers | Via Claude API/Ollama | ⭐⭐⭐⭐⭐ | Limited |
| **VS Code** | Free | Most developers | Extensions (Cline, Roo-Cline) | ⭐⭐⭐⭐ | Extensive |
| **Cursor** | $20/mo | AI-first coding | Native (best) | ⭐⭐⭐⭐ | VS Code compatible |
| **Windsurf** | $15/mo | Codeium fans | Native (Codeium) | ⭐⭐⭐⭐ | Limited |

### Zed (Recommended for Budget-Conscious)

**Cost:** Free and open source

**Pros:**
- ✅ Extremely fast (Rust-based)
- ✅ Modern, clean UI
- ✅ Built-in collaboration
- ✅ Native performance
- ✅ Low resource usage
- ✅ Claude API integration (bring your own key)
- ✅ Ollama support (local models)

**Cons:**
- ❌ Limited extensions ecosystem
- ❌ Newer (less mature than VS Code)
- ❌ AI features less polished than Cursor
- ❌ Smaller community

**Best for:**
- Developers who prioritize speed
- Clean, distraction-free coding
- Using your own Claude API key
- Local AI models (Ollama)
- Budget-conscious professionals

**AI setup:**
```
Settings → Language Models
- Add Claude API key (from Anthropic)
- Or configure Ollama (local, free)
```

### VS Code (Most Versatile)

**Cost:** Free and open source

**Pros:**
- ✅ Free and open source
- ✅ Massive extension ecosystem
- ✅ Industry standard
- ✅ Excellent documentation
- ✅ Multiple AI options (Cline, Roo-Cline, Continue, GitHub Copilot)
- ✅ Highly customizable
- ✅ Great debugging

**Cons:**
- ❌ Can be slow with many extensions
- ❌ Resource-heavy
- ❌ AI features require extensions
- ❌ Configuration complexity

**Best for:**
- Most developers (industry standard)
- Extensive customization needs
- Using AI extensions (Cline, Roo-Cline)
- When you need specific extensions
- Team standardization

**Recommended AI extensions:**
- **Cline** - AI assistant (supports multiple APIs)
- **Roo-Cline** - Enhanced Cline fork
- **Continue** - AI code assistant (BYOK)
- **GitHub Copilot** - Code completion ($10/mo or free for students)

### Cursor (Best AI Integration)

**Cost:** $20/month Pro (or free with limits)

**Pros:**
- ✅ Best native AI integration
- ✅ Built on VS Code (familiar)
- ✅ Composer (excellent multi-file editing)
- ✅ BYOK support (use your own API keys)
- ✅ Multi-model support
- ✅ VS Code extensions work
- ✅ Active development

**Cons:**
- ❌ $20/month for full features
- ❌ Yet another IDE to manage
- ❌ Free tier very limited (50 requests)
- ❌ Some features locked behind Pro

**Best for:**
- Developers who want best AI experience
- Can afford $20/mo
- Want BYOK option
- Multi-file editing workflows
- Willing to switch from VS Code

**Free tier limitations:**
- 50 free requests/month (very limited)
- No Composer access
- Limited models

**Pro tier ($20/mo):**
- Unlimited requests (fair use)
- Full Composer access
- All models
- BYOK option

### Windsurf (Codeium-Based)

**Cost:** $15/month (or free tier)

**Pros:**
- ✅ Native AI integration (Codeium)
- ✅ Cheaper than Cursor ($15 vs $20)
- ✅ Built-in collaboration
- ✅ Modern UI
- ✅ Good performance

**Cons:**
- ❌ Locked to Codeium models
- ❌ No BYOK option (unlike Cursor)
- ❌ Smaller community
- ❌ Limited extension ecosystem
- ❌ Less mature than alternatives

**Best for:**
- Codeium fans
- Want native AI for less than Cursor
- Don't need BYOK flexibility

**Not recommended if:**
- You want model flexibility
- You want to use your own API keys
- You need extensive extensions
- You're budget-conscious (Zed + API is cheaper long-term)

### IDE Recommendation by Persona

| Your Priority | Recommended IDE | Cost | AI Solution |
|---------------|----------------|------|-------------|
| **Speed** | Zed | Free | Claude API BYOK |
| **Versatility** | VS Code | Free | Cline extension + Factory AI |
| **Best AI** | Cursor | $20/mo | Native or BYOK |
| **Budget** | VS Code or Zed | Free | Free tier APIs |
| **Standard** | VS Code | Free | Any extension |

## MCP Servers (Free Options)

Model Context Protocol servers extend AI capabilities.

### What is MCP?

**MCP (Model Context Protocol)** lets AI assistants access external data and tools:
- File systems
- Databases
- APIs
- Build tools
- Git repositories
- Documentation

**Free MCP servers you should use:**

| Server | Purpose | Cost | Value |
|--------|---------|------|-------|
| **Filesystem MCP** | Local file access | Free | Essential |
| **Git MCP** | Repository context | Free | Essential |
| **SQLite MCP** | Database queries | Free | High |
| **Web MCP** | Fetch web content | Free | Medium |
| **Brave Search MCP** | Web search | Free | Medium |

### Filesystem MCP

**What it does:** Gives AI access to read/write your project files

**Why use it:** AI can make cross-file edits without you copying files

**Cost:** Free

**Setup:**
```bash
# Usually included with AI coding tools
# No configuration needed
```

### Git MCP

**What it does:** AI can read git history, branches, commits, diffs

**Why use it:** AI understands project evolution, can suggest better approaches based on history

**Cost:** Free

**Setup:**
```bash
# Included with most AI coding tools
# Make sure your project is a git repository
git init
```

### SQLite MCP

**What it does:** AI can query SQLite databases directly

**Why use it:** AI can analyze data, write queries, understand schema

**Cost:** Free

**Setup:**
```bash
# Install MCP server
npm install -g @modelcontextprotocol/server-sqlite

# Configure in your AI tool settings
```

**Use case:**
```
You: "Show me all users who signed up last month"
AI: [Writes and executes SQL query, shows results]
```

### Web MCP

**What it does:** AI can fetch web pages for context

**Why use it:** AI can read documentation, API references, etc.

**Cost:** Free

**Use case:**
```
You: "Check the Astro docs for the latest image optimization syntax"
AI: [Fetches docs.astro.build, finds relevant section, writes code]
```

### Brave Search MCP

**What it does:** AI can perform web searches

**Why use it:** AI can find current information, docs, examples

**Cost:** Free (API key required)

**Setup:**
1. Get free Brave Search API key (https://brave.com/search/api/)
2. Configure MCP server with key

**Use case:**
```
You: "Find the latest Tailwind CSS dark mode best practices"
AI: [Searches web, reads results, summarizes findings]
```

### Other Free MCP Servers

- **GitHub MCP** - Query GitHub APIs (issues, PRs, repos)
- **Postgres MCP** - Query PostgreSQL databases
- **Docker MCP** - Interact with Docker containers
- **AWS MCP** - Query AWS resources (requires AWS account)

**Where to find more:** https://github.com/modelcontextprotocol/servers

## Migration Guides

### Moving from Expensive to Budget Tools

#### Claude Code ($200/mo) → GLM ($15/mo)

**Savings:** $185/month ($2,220/year)

**What you lose:**
- Native VS Code integration (use Cline extension instead)
- Some advanced context features (95% of the time you won't notice)
- Anthropic support (rely on community)

**What you keep:**
- High-quality code generation (GLM-4-Plus is excellent)
- Multi-file editing (via Cline)
- File search and terminal access
- Git operations

**Migration steps:**
1. **Subscribe to GLM** - https://open.bigmodel.cn (~$15/mo)
2. **Install Cline** - In VS Code, install "Cline" extension
3. **Configure Cline** - Add GLM API key
4. **Test workflow** - Run same tasks you did with Claude Code
5. **Cancel Claude Code** - Once confident

**Adjustment period:** 1-2 weeks to get comfortable with new workflow

**Real testimonial:**
> "I was skeptical about downgrading from Claude Code, but honestly I don't miss it. GLM + Cline gives me 90% of the capability at 7.5% of the cost." - Freelancer who made the switch

#### Cursor Pro ($20/mo) → VS Code + Free APIs

**Savings:** $20/month ($240/year)

**What you lose:**
- Unified AI IDE (use VS Code + extension instead)
- Composer (use Cline/Roo-Cline equivalents)
- Premium models unlimited (use free tiers or cheap APIs)

**What you keep:**
- Multi-file editing (Cline has this)
- Code generation (via free APIs)
- IDE features (VS Code is more powerful)

**Migration steps:**
1. **Install VS Code** (if not already using)
2. **Install Cline or Roo-Cline**
3. **Get free API keys**:
   - Factory AI (free tier)
   - Anthropic ($5 credit)
   - OpenAI ($5 credit)
4. **Configure extension** with API keys
5. **Cancel Cursor** once comfortable

**Pro tip:** Rotate through free tiers to maximize free usage

#### Cursor BYOK → Keep Cursor, Use Cheaper APIs

**Savings:** Variable (potentially $10-15/mo)

**Strategy:**
- Keep Cursor IDE ($20/mo)
- Use your own cheaper API keys instead of Cursor's
- Pay only for API usage (potentially $5-10/mo)
- Net cost: ~$25-30/mo vs $20/mo + usage

**Wait, that's not savings?**
- Actually, Cursor Pro usage-based pricing can exceed $20/mo
- BYOK gives you cost control
- Use cheaper models (GPT-3.5, Claude Haiku) for simple tasks
- Use premium models only when needed

## ROI Scenarios

### Hobbyist / Learner (Target: $0/month)

**Profile:**
- Learning to code or building side projects
- No client income
- Budget: $0

**Recommended stack:**
```
IDE: VS Code (free) or Zed (free)
AI: Qwen CLI (free via Factory AI)
Hosting: Cloudflare Pages (free)
Analytics: Plausible.io free tier
Total: $0/month
```

**Capabilities:**
- Full AI-assisted development
- Deploy static sites
- Basic analytics
- Professional results

**What you give up:**
- Premium AI models (use free tiers)
- Advanced features (rarely needed anyway)
- Unlimited usage (free tiers sufficient for learning)

**Verdict:** ✅ Completely viable, no compromises for learning

### Freelancer (Budget: $5-20/month)

**Profile:**
- Billing 1-5 clients
- $50-100/hour rate
- Revenue: $2,000-5,000/month

**Recommended stack (Tier 1: $15/mo):**
```
IDE: VS Code (free)
AI: GLM ($15/mo)
Hosting: Cloudflare Pages (free)
Analytics: Plausible.io paid ($9/mo) or free
Total: $15-24/month
```

**ROI calculation:**
```
Monthly cost: $15
If AI saves 2 hours/month
Your rate: $75/hour
Savings: 2 × $75 = $150
ROI: $150 - $15 = $135 profit
Annual: $135 × 12 = $1,620 profit
```

**Verdict:** ✅ 10x ROI, easily justified

**Recommended stack (Tier 2: $20/mo):**
```
IDE: Cursor ($20/mo)
AI: Cursor built-in + BYOK for heavy usage
Hosting: Cloudflare Pages (free)
Analytics: Cloudflare Analytics (free)
Total: $20-25/month
```

**When to choose Tier 2:**
- You value IDE integration highly
- You want multi-model access
- $20/mo easily justified by your revenue

### Agency (Budget: $50-100/month)

**Profile:**
- Team of 2-4 developers
- Billing multiple clients
- Revenue: $20,000-50,000/month

**Recommended stack (per developer):**
```
IDE: Cursor ($20/mo) or Claude Code ($200/mo)
AI: Included with IDE
Hosting: Cloudflare Pages (free) or Pro ($20/mo)
Monitoring: Paid tier ($20-50/mo)
Total per dev: $40-270/month
Team of 3: $120-810/month
```

**Which to choose:**
- **Claude Code ($200/mo)** if:
  - Working on complex projects
  - AI cost is billable to clients
  - Quality is paramount
  - Developers bill $150+/hour

- **Cursor ($20/mo)** if:
  - Budget-conscious agency
  - Developers bill $75-150/hour
  - Good balance needed

**ROI calculation (Claude Code):**
```
Cost: $200/month per developer
If AI saves 10 hours/month
Developer cost: $75/hour (fully loaded)
Savings: 10 × $75 = $750
ROI: $750 - $200 = $550 profit
Annual per dev: $550 × 12 = $6,600
Team of 3: $19,800/year profit
```

**Verdict:** ✅ Easily justified for agencies

### When Expensive Tools Make Sense

**Claude Code ($200/mo) is justified when:**

1. **You bill $150+/hour** and work full-time
   - Savings exceed cost by 10x+
   - Cost is negligible vs. revenue

2. **Working on enterprise/complex projects**
   - Code quality is critical
   - Mistakes are expensive
   - Client expects best results

3. **Agency with billable AI costs**
   - Include AI tools in project quotes
   - Client pays for the tooling
   - Zero effective cost to you

4. **You need specific features**
   - Advanced VS Code integration
   - Enterprise support
   - Team features

**When Claude Code is NOT justified:**

1. **You're a hobbyist** - Use free tools
2. **Freelancer billing < $100/hour** - GLM or Cursor better ROI
3. **Can't directly expense it** - Hard to justify $2,400/year
4. **Side projects** - Way overkill
5. **Learning/education** - Free tools are fine

## Summary Decision Tree

```
START: What's your budget?

├─ $0/month → Qwen CLI + VS Code/Zed + Factory AI free tier
│   ├─ Hobbyist? → Stay here ✅
│   ├─ Learning? → Stay here ✅
│   └─ Freelancer? → Consider upgrade when billing clients

├─ $15-25/month → GLM or Cursor
│   ├─ Want CLI? → GLM ($15/mo)
│   ├─ Want IDE integration? → Cursor ($20/mo)
│   └─ Freelancer sweet spot ✅

├─ $50-100/month → Cursor or Claude Code
│   ├─ Small agency? → Cursor for team
│   ├─ High-value projects? → Claude Code
│   └─ Can expense it? → Claude Code

└─ $200+/month → Claude Code
    ├─ Enterprise projects? → Yes ✅
    ├─ Agency team? → Yes ✅
    ├─ Bill $150+/hour? → Yes ✅
    └─ Otherwise? → Probably overkill ⚠️
```

## Cross-References

**Related documentation:**
- [Introduction - Philosophy](../introduction/philosophy.md) - Cost-effectiveness principles
- [Business Model - ROI Tracking](../business-model/roi-tracking.md) - Calculating tool ROI
- [Core Technologies](../core-technologies.md) - Tech stack decisions
- [Cheat Sheets](./cheat-sheets/README.md) - Quick reference for tool usage

**Development tools documentation:**
- [Qwen CLI Guide](./qwen-cli.md) - Detailed Qwen setup and usage
- [GLM Setup](./glm-setup.md) - Subscribe and configure GLM
- [Cursor Configuration](./cursor-config.md) - Optimize Cursor settings
- [VS Code Extensions](./vscode-extensions.md) - Recommended extensions

---

**Remember:** Start free, upgrade only when clearly justified by ROI. The goal is sustainable, profitable development - not using the latest expensive tools.
