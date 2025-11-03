# Tools I Dropped — Honest Assessment 🪓

This section documents tools I've personally used and decided to drop from my workflow. My goal is to provide transparent, experience-based insights to help you make informed decisions about your own tech stack.

## Tools

- [Traycer.ai](#traycerai) - AI-powered development planning and validation
- [Claude Code](#claude-code) - Anthropic's CLI coding assistant

---

## Traycer.ai

### Why I left
- **Too slow**—planning takes long, validation too, fixes even longer
- **Plugin dependency**—requires VS Code/derivatives (no Zed support as per time of writing this guide)
- **Costly**—$25/month for realistic workloads (with recent pricing changes having 1 artifact per 45 minutes it might not be even enough for serious, fast paced development)
- **Frustration**—when the plan hallucinates, rollbacks waste lots of time

### What was good
- Automatic validation of ongoing development
- High output quality (when it works)
- Usually, the combination of plan + validation + improvements after validation improved overall project quality (at the cost of significantly longer delivery time).

### Conclusion
You can achieve similar results with OpenSpec + GLM for a fraction of the price—and often in less time—than with Traycer.

---

## Claude Code

### Why I left
- **Performance degradation** - Claude's capabilities noticeably declined around August 2025
- **Limit changes** - Reduced weekly allowances after initial setup, making it less reliable for consistent work
- **Crazy expensive** - For serious development (few hours per day, 5 days/week), you need at least the Max5 plan at $100/month (~€120 in EU due to VAT)
- **Cost vs benefit** - Sometimes even Max20 wasn't enough for intensive development sessions
- **Better alternatives** - Open-source models, eg. GLM Coding Plan provide comparable results at a fraction of the cost

### What was good
- State-of-the-art model performance when it works well
- Seamless integration with Claude's ecosystem
- Good for quick prototyping when you need the absolute best model
- Reliable API and infrastructure

### Conclusion
If you desperately need SOTA model performance, Claude Code might be worth it, but the cost is prohibitive for most developers. The difference in quality between Claude and good open-source models becomes negligible when you have proper vibecoding techniques and a solid workflow around the LLM. Using GLM provides significantly better monthly profit margins while delivering comparable results.



Back: [Tools & Tech Stack](./README.md)