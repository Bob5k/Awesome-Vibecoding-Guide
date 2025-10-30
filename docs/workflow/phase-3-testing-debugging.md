# Phase 3: Testing & Debugging 🧪

**Tools:** DevTools MCP + Your coding agent + Manual Testing

## Process

1) Automated Testing via MCP:
> “Use DevTools MCP to test the login page and find bugs.”

Agent:
- Opens the browser
- Navigates the app
- Collects console errors
- Analyzes network calls
- Identifies issues
- Proposes a fix

2) Manual Testing:
- Walk through the functionality yourself
- Document edge cases
- Check different browsers/devices

3) Debugging Deep Dive:

Golden rule: Debugging is effective only when you dig deep.

Don’t:
"Doesn’t work, fix it"
"Still doesn’t work, fix pls" (x100)

Do:
Analyze the bug (manually or via MCP)

Gather logs specific to the issue

Identify the exact root cause

Tell the AI what you found + ask for a fix

If the same bug repeats 2–3 times:
1. Stop—something is fundamentally wrong
2. Use MCP to gather precise logs
3. Analyze them before the next prompt
4. You may need to change approach, not just code

Next: [Phase 4 → Code Review & Refactoring](./phase-4-code-review-refactoring.md)

Back: [Workflow overview](./README.md)
