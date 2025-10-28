# Context Management 🧠

## Fundamentals

The most important rule: context is your most valuable resource. Manage it deliberately.

## Techniques

### 1) Selective File Inclusion

Modular structure:

```text
project/
├── src/
│   ├── components/   # Only when working with UI
│   ├── api/          # Only when working on backend
│   ├── utils/        # Only when tools are needed
│   └── database/     # Only when working with DB
└── docs/             # Always indexed by Context7
```

Practice:
- Add only relevant folders to the prompt
- Don’t let AI scan the entire codebase every time
- You know best what’s needed—not AI

### 2) MCP as Context Savings

Instead of:
> “Check the browser console, find errors, analyze the stack trace, inspect the network tab, review responses, debug the backend, fix the issue.”

Say:
> “Use the DevTools MCP to find and fix the error.”

Result: 95% fewer tokens consumed with better results.

### 3) Dialog Compression

In Zed (automatic):
- When context fills up → the agent creates a summary
- Dialog is compressed
- Essential context is preserved
- You can continue without resetting

Manually:
- Periodically compress / compact the conversation and start from the compacted version
- Don't trust the tools themselves to do the compacting and context management for you
- Trust your intuition instead — context is the most important thing when we're talking about Vibecoding

### 4) Avoiding Bloat

Don’t:
- Add `node_modules` to context
- Mass-include all files “just in case”
- Repeat the same instructions multiple times
- Run too many MCP servers at once

Do:
- Include only relevant files
- Use `.cursorrules` or similar for persistent instructions
- Use Context7 MCP for documentation
- Favor a modular architecture

## Monitoring Context Usage

Signs of trouble:
- Degradation in answer quality
- AI forgets prior decisions
- Repetitive mistakes
- Suggestions misaligned with project architecture

Solutions:
- Compress the dialog (summary)
- Remove unnecessary files from context
- Start a new session with a clear context + summary
- Add key decisions to `/docs`

## Context Window Strategy

Models and their limits:
- Claude Sonnet 3.5: 200k tokens
- GPT-4o: 128k tokens
- GLM 4.5: 128k+ tokens

My practice:
- Use up to 85% of capacity
- When approaching the limit: compress
- Never fill 100% — AI starts to rush to finish

Community pro tip:
If you have 1M context (Claude), you can fill it but compress around ~200k. The AI won’t feel end‑of‑context pressure and won’t trigger “rush‑to‑finish” behavior.

Back to index: [Top‑level README](../../README.md)
