# Windsurf — High-Speed AI IDE

## Overview
Windsurf is Codeium's AI-powered IDE (acquired by Cognition in 2025), built as a VS Code fork with integrated agentic capabilities. It stands out with its SWE-1.5 agent model achieving 950 tokens/second—13x faster than Claude Sonnet 4.5—while maintaining near-frontier coding performance.

## Key Strengths

### SWE-1.5: Speed Without Compromise
- **950 tokens/second**: 13x faster than Sonnet 4.5 (69 tok/s), 6x faster than Haiku 4.5
- **40.08% on SWE-Bench Pro**: Near-SOTA performance (vs Sonnet 4.5's 43.60%)
- **Frontier-size model**: Hundreds of billions of parameters optimized for speed
- **Co-designed architecture**: Model, inference system, and agent harness unified for performance

### Codemaps: Visual Codebase Understanding
- **AI-annotated code maps**: Powered by SWE-1.5 and Sonnet 4.5
- **Visual navigation**: See connections, flow, and relationships across modules
- **Instant jumping**: Click any node to navigate directly to code location
- **Smart or Fast modes**: Choose between thorough analysis (Sonnet 4.5) or rapid mapping (SWE-1.5)
- **Best for**: Onboarding to new codebases, tracing client-server flows, debugging authentication

### Development Experience
- **VS Code fork**: Full compatibility with extensions and familiar workflows
- **Cascade integration**: Built-in AI chat with context-aware suggestions
- **Planning Mode**: Native collaborative planning for complex tasks
- **Browser integration**: Implicit context understanding from web resources
- **Active development**: Frequent updates (Wave 10, Wave 11) with new capabilities

## Best Use Cases
- Developers wanting fastest possible AI agent responses (950 tok/s)
- VS Code users seeking integrated AI without switching IDEs
- Teams onboarding to large codebases (Codemaps visualization)
- Rapid prototyping where speed matters more than unlimited requests
- Projects requiring visual code flow understanding

## Limitations & Trade-offs

### Pricing Model
- **$15/month for 500 requests**: Monthly cap may limit heavy users
- **No BYOK support**: Can't bring your own API keys like Zed (except for Anthropic API key)
- **Compare to alternatives**:
  - Zed (free) + GLM ($3-6) = unlimited requests with rolling windows
  - Windsurf = faster experience but fixed monthly limit

### When to Choose Alternatives
- **Use Zed + Droid CLI** if you need:
  - Unlimited usage without request caps
  - BYOK flexibility (use any LLM provider)
  - Maximum cost optimization
  - Lighter resource usage (Zed uses 20% of VS Code resources)

- **Use Windsurf** if you prioritize:
  - Absolute speed (950 tok/s agent)
  - VS Code ecosystem compatibility
  - All-in-one solution without configuration
  - Visual codebase exploration (Codemaps)

## Technical Details

### Performance Benchmarks
- **SWE-1.5 speed**: 950 tokens/second via Cerebras partnership
- **Latency optimization**: Reduced overhead per step by up to 2 seconds
- **Agent efficiency**: Rewrote lint checking and command execution pipelines

### Model Access
- Free tier available for experimentation
- Paid tier: $15/month for 500 requests across multiple models
- Support for OpenAI, Anthropic, and proprietary SWE models

## Why It Matters
Windsurf represents a meaningful evolution in AI-assisted development: it proves that speed and intelligence don't have to trade off. The SWE-1.5 model's 950 tok/s throughput makes AI coding feel genuinely instantaneous, while Codemaps addresses a real pain point—understanding unfamiliar codebases.

For VS Code users, Windsurf offers the smoothest path to high-speed vibecoding without learning a new IDE. The trade-off is flexibility: you're locked into Windsurf's pricing model rather than optimizing costs with BYOK providers.

### Complementary to Zed
Windsurf and Zed serve different needs:
- **Windsurf**: Speed-first, all-in-one, VS Code familiarity
- **Zed**: Flexibility-first, BYOK, resource efficiency, unlimited usage

Both are legitimate choices depending on whether you value maximum speed (Windsurf) or maximum control (Zed).

## Recent Developments (2024-2025)
- **October 2025**: SWE-1.5 launch with 950 tok/s performance
- **July 2025**: Cognition acquisition, Wave 11 with Browser tools and Voice Mode
- **June 2025**: Wave 10 with Planning Mode and enhanced collaboration
- **May 2025**: SWE-1 Frontier Models for native agentic capabilities
- **November 2024**: Initial launch as VS Code fork

**Official Resources**: [windsurf.com](https://windsurf.com) | [docs.windsurf.com](https://docs.windsurf.com) | [Codemaps Documentation](https://docs.windsurf.com/windsurf/codemaps)

---

**See also**: [Zed.dev](./zed.md) (lightweight alternative) • [Droid CLI](./droid-cli.md) (BYOK agent) • [Tool Compatibility](../compatibility.md)

Back: [Development Tools](../README.md)
