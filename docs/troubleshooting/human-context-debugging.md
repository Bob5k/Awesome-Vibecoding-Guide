# The Human Context Problem in AI Debugging

**The uncomfortable truth about "AI can't debug this" situations.**

---

## Table of Contents
- [The Uncomfortable Truth](#the-uncomfortable-truth)
- [Why This Happens](#why-this-happens)
- [The Human-First Framework](#the-human-first-framework)
- [Real-World Examples](#real-world-examples)
- [Context Gathering Checklist](#context-gathering-checklist)
- [When to Involve AI](#when-to-involve-ai)
- [The Starting Over Myth](#the-starting-over-myth)
- [Common Scenarios](#common-scenarios)
- [Best Practices](#best-practices)

---

## The Uncomfortable Truth

**If you're being forced to "start over" on a project, you're either:**

1. **Developing something super-overly-complex on corporate level** (5% of cases)
2. **Trying to forcefully move forward instead of instructing AI properly** (95% of cases)

The main issue isn't your AI tool, the model, or the context window limit.

**The main issue is lack of context knowledge IN THE HUMAN, not in the AI window.**

### The Real Problem

People can't (or don't):
- Open browser DevTools and copy-paste the error printed in console
- Check network requests to see what's actually being sent/received
- Look at server logs to see what's happening backend
- Provide exact reproduction steps
- Share the actual error message

Instead, they push AI to debug things **AI has no clue about** because **the human is missing context too**.

Then they blame:
- ❌ "The AI is bad at debugging"
- ❌ "Context window is too small"
- ❌ "The model hallucinates"
- ❌ "Need to start a new project"

**Reality check:** You're asking AI to debug blindfolded while you're also blindfolded.

---

## Why This Happens

### 1. Developers Skip Basic Investigation

**Common pattern:**
```
User: "The submit button doesn't work. Fix it."

AI: "I need more information. What error do you see?"

User: "It just doesn't work. Can you check the code?"

AI: *makes educated guess, changes something*

User: "Still doesn't work. This AI is useless."
```

**What's missing:** The user never opened DevTools. Never checked console. Never looked at network requests. Never tried to understand WHAT is actually failing.

### 2. Fear of Looking "Dumb"

Developers think:
- "I should know what's wrong without checking logs"
- "Real programmers don't need DevTools for simple bugs"
- "AI should figure it out from the code"

**Truth:** Professional developers check logs first. Always. That's not "dumb"—that's **professional**.

### 3. Misunderstanding AI's Role

**What developers think AI does:**
- Magically understands runtime state
- Has access to browser console
- Can see network requests
- Knows what error happened

**What AI actually sees:**
- The code you shared
- The description you wrote
- Nothing about runtime behavior
- No access to errors unless you paste them

**AI is not psychic. AI is a pair programmer who can only see what you show them.**

### 4. Confusion About "Starting Over"

**User after 20 hours of development:**
> "This is broken. Should I start a new project?"

**Reality check:** You wouldn't throw away 20 hours of work in traditional development. Why would you with AI?

**What "starting over" really means:**
- ✅ New chat window (totally fine, helps with context)
- ❌ New project (waste of time, doesn't solve the problem)

**The issue isn't the project. It's your debugging process.**

---

## The Human-First Framework

### Core Principle

**Before asking AI to debug, debug the HUMAN context first.**

```
┌─────────────────────────────────────────────┐
│ Traditional (Wrong) Debugging Flow          │
├─────────────────────────────────────────────┤
│ 1. Something breaks                         │
│ 2. Tell AI "it's broken"                    │
│ 3. AI guesses and changes code              │
│ 4. Still broken                             │
│ 5. Repeat 20 times                          │
│ 6. Give up / start over                     │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│ Human-First (Correct) Debugging Flow        │
├─────────────────────────────────────────────┤
│ 1. Something breaks                         │
│ 2. HUMAN gathers context:                   │
│    - Console errors                         │
│    - Network requests                       │
│    - Reproduction steps                     │
│    - What you expected vs what happened     │
│ 3. Give AI complete picture                 │
│ 4. AI identifies root cause immediately     │
│ 5. Fixed on first try                       │
└─────────────────────────────────────────────┘
```

### The 3-Step Process

#### Step 1: Gather Context (HUMAN does this)

**Before touching AI, collect:**

1. **Console Output**
   - Open browser DevTools (F12)
   - Check Console tab
   - Copy ALL error messages
   - Include stack traces

2. **Network Activity**
   - Check Network tab in DevTools
   - Find failed requests (red)
   - Check request/response data
   - Note status codes (404, 500, etc.)

3. **Reproduction Steps**
   - Write down EXACT steps to reproduce
   - Include what you clicked, typed, selected
   - Note when error appears

4. **Expected vs Actual**
   - What you expected to happen
   - What actually happened
   - The difference between them

5. **Environment Details**
   - Browser/device
   - Operating system
   - Relevant settings

#### Step 2: Provide Complete Context to AI

**Good AI debugging request:**

```
"I'm getting an error when users try to submit the contact form.

CONTEXT:
1. Console error:
   ```
   TypeError: Cannot read property 'value' of null
   at submitForm (contact.js:45)
   ```

2. Network requests:
   - POST /api/contact returns 400 Bad Request
   - Response: {"error": "Missing required field: email"}

3. Reproduction steps:
   - Fill out name field
   - Skip email field
   - Click Submit button
   - Error appears

4. Expected: Form validation should show error before submit
5. Actual: Form submits, server rejects, page shows generic error

CODE LOCATION: contact.js lines 40-50

Can you help identify why client-side validation isn't working?"
```

**Bad AI debugging request:**

```
"Form is broken fix it"
```

#### Step 3: Lead AI Through the Process

**If debugging is complex:**
- Give AI context step by step
- Use tools like Chrome DevTools MCP to let AI see live data
- Guide AI to check specific things
- Provide feedback on each attempted fix

**Example with tools:**
```
"Let me share the browser console output with you.
[Use DevTools MCP to capture console]

Now let's check the network requests.
[Use DevTools MCP to capture network]

Based on this data, what's the root cause?"
```

---

## Real-World Examples

### Example 1: "Login Doesn't Work"

#### ❌ Bad Approach (Code-First)

```
Developer: "Login doesn't work. Here's my auth code."
[Pastes 200 lines of authentication code]

AI: "I see a potential issue with the password hashing. Try this fix."
[Provides code change]

Developer: "Still doesn't work."

AI: "Let's check the session management..."
[Provides another fix]

Developer: "STILL doesn't work. This AI is useless."
```

**Result:** 30 minutes wasted, still broken.

**Why it failed:** No context. AI is guessing blindly.

#### ✅ Good Approach (Human-First)

```
Developer: "Users can't log in. Let me gather context first."

[Opens DevTools, attempts login]

Developer: "Found it. Here's the context:

CONSOLE ERROR:
POST /api/login 401 Unauthorized
Response: {"error": "Invalid credentials"}

WHAT I DID:
1. Entered email: test@example.com
2. Entered password: (correct password)
3. Clicked Login

NETWORK TAB:
Request payload: {"email": "test@example.com", "password": "password123"}

EXPECTED: Successful login
ACTUAL: 401 error

Interesting: The password in the request is literally 'password123'
instead of the password I typed. Something's wrong with how we're
reading the password field value."

AI: "I see the issue. Line 23 in login.js is reading from the wrong
form field. You're getting the placeholder text instead of the actual
input value. Change getElementById('password').placeholder to
getElementById('password').value"

Developer: "Perfect! That fixed it."
```

**Result:** 2 minutes to gather context, 30 seconds to fix.

**Why it worked:** Complete context allowed AI to identify exact issue immediately.

### Example 2: "Page Is Slow"

#### ❌ Bad Approach

```
Developer: "The page is really slow. Optimize it."

AI: "Let's implement lazy loading, code splitting, and memoization."
[Provides complex optimization code]

Developer: "Still slow. Try something else."

AI: "Let's add service workers and caching..."
```

**Result:** 2 hours of premature optimization, still slow.

#### ✅ Good Approach

```
Developer: "Page feels slow. Let me investigate first."

[Opens DevTools Performance tab, records loading]
[Checks Network tab]

Developer: "Found the issue:

CONTEXT:
- Initial page load: 8 seconds
- Network tab shows: Downloading hero image (12MB!)
- No other requests are slow
- After image loads, everything is fast

USER ENVIRONMENT:
- Mobile device
- 3G connection
- Image is loading at full 6000x4000 resolution

EXPECTED: Page loads in <2 seconds
ACTUAL: 8 second wait for massive image

The problem isn't code performance. It's a 12MB image on mobile.

Solution: Resize image, add responsive srcset, compress for web?"

AI: "Exactly. Here's how to implement responsive images..."
```

**Result:** 5 minutes to identify real issue, 10 minutes to implement proper fix.

**Why it worked:** Investigation revealed the actual bottleneck before wasting time on wrong optimizations.

### Example 3: "Feature Is Broken"

#### ❌ Bad Approach

```
Developer: "The shopping cart isn't working. Debug it."

AI: "I'll check for state management issues..."
[Makes changes to Redux store]

Developer: "No, it's something else."

AI: "Maybe it's the API endpoint..."
[Makes backend changes]

Developer: "Users still complaining."
```

**Result:** Wild goose chase, multiple wrong fixes.

#### ✅ Good Approach

```
Developer: "Users report cart issues. Let me reproduce this."

[Tries to use cart feature]
[Records screen while using feature]

Developer: "Here's what I found:

USER REPORT: "Cart doesn't work"

REPRODUCTION:
1. User adds item to cart → ✅ Works
2. Item appears in cart → ✅ Works
3. User clicks checkout → ✅ Works
4. Payment page loads → ✅ Works
5. User enters payment info → ✅ Works
6. User clicks Pay → ❌ Nothing happens

CONSOLE ERROR:
Uncaught Error: Payment processor ID is undefined
at processPayment (checkout.js:89)

NETWORK:
POST /api/payment - never fires

ROOT CAUSE: Payment button is supposed to submit payment
but can't find processor ID in environment variables.

ENVIRONMENT CHECK:
Development: PAYMENT_PROCESSOR_ID=pk_test_xxx ✅
Production: PAYMENT_PROCESSOR_ID=(not set) ❌

The code is fine. It's a deployment configuration issue.
Need to set PAYMENT_PROCESSOR_ID in production environment."

AI: "Correct diagnosis. Here's how to safely add that environment
variable to your production deployment without exposing secrets..."
```

**Result:** Problem identified as deployment config, not code bug. Saved hours of debugging wrong thing.

**Why it worked:** Methodical investigation revealed real issue was infrastructure, not code.

---

## Context Gathering Checklist

### Every Time Something Breaks:

#### 🔍 Investigation Steps

**1. Console Errors**
- [ ] Open DevTools (F12 or Cmd+Option+I)
- [ ] Check Console tab for red errors
- [ ] Copy complete error message
- [ ] Copy stack trace
- [ ] Note line numbers

**2. Network Activity**
- [ ] Check Network tab in DevTools
- [ ] Identify failed requests (red status)
- [ ] Check request method (GET, POST, etc.)
- [ ] Check status code (404, 500, 401, etc.)
- [ ] Inspect request payload
- [ ] Inspect response data
- [ ] Check response headers

**3. Application State**
- [ ] Check Application/Storage tab
- [ ] Verify localStorage/sessionStorage
- [ ] Check cookies
- [ ] Verify authentication tokens
- [ ] Check service workers (if applicable)

**4. Reproduction Steps**
- [ ] Write exact steps to reproduce
- [ ] Note what you clicked/typed
- [ ] Record timing (immediate vs delayed)
- [ ] Test if it's consistent or intermittent
- [ ] Try in different browser/device

**5. Expected vs Actual**
- [ ] What should happen (expected behavior)
- [ ] What actually happens (observed behavior)
- [ ] The difference between them
- [ ] Why you expected that behavior

**6. Code Context**
- [ ] Identify which file/function is involved
- [ ] Check recent changes to that code
- [ ] Note related files or dependencies
- [ ] Consider what might have changed

**7. Environment Details**
- [ ] Browser and version
- [ ] Operating system
- [ ] Device type (desktop/mobile/tablet)
- [ ] Screen size (if UI-related)
- [ ] Internet connection quality
- [ ] Any relevant settings or configurations

### Before Asking AI:

**Minimum required context:**
- ✅ Console error message (if any)
- ✅ What you were trying to do
- ✅ What actually happened
- ✅ Reproduction steps

**Ideal complete context:**
- ✅ All of the above PLUS:
- ✅ Network request/response details
- ✅ Related code location
- ✅ What you've already tried
- ✅ Environment details

---

## When to Involve AI

### ✅ Involve AI When You Have:

1. **Complete Error Context**
   ```
   "Getting this error: [paste error]
   When doing: [steps]
   Expected: [outcome]
   Network shows: [request details]
   Code location: [file:line]"
   ```

2. **Specific Technical Question**
   ```
   "This function returns undefined when I expect an array.
   Here's the function: [code]
   Here's how I'm calling it: [code]
   Console shows: [output]
   What's wrong with my approach?"
   ```

3. **Architecture Decision After Investigation**
   ```
   "I've identified the bottleneck is in database queries.
   Current: 50 queries per page load
   Each query takes: 100ms
   Total: 5 second load time

   Considering:
   1. Implement caching
   2. Use query batching
   3. Add database indexes

   Which approach is best for this use case?"
   ```

### ❌ Don't Involve AI When You Haven't:

1. **Checked for Errors**
   ```
   ❌ "It doesn't work, fix it"
   ✅ "Let me check console first... [finds error] ... now I can ask AI"
   ```

2. **Attempted Basic Investigation**
   ```
   ❌ "Page is slow, optimize it"
   ✅ "Let me profile it first... [finds issue] ... now I can ask AI"
   ```

3. **Understood What's Happening**
   ```
   ❌ "Feature broke, not sure why"
   ✅ "Let me reproduce it... [reproduces] ... [checks logs] ... now I understand what's breaking"
   ```

### Using Tools to Lead AI

**AI doesn't have eyes. You do. You are AI's eyes.**

#### Manual Context Gathering (Always Available)

```
1. You open DevTools
2. You copy error messages
3. You paste into AI chat
4. AI analyzes and suggests fix
```

#### Tool-Assisted Context Gathering (Optional)

Some AI tools offer MCP (Model Context Protocol) integrations like Chrome DevTools MCP:

```
1. You connect DevTools MCP to your AI tool
2. AI can request specific information:
   - "Show me console errors"
   - "What network requests failed?"
   - "Take a screenshot of current state"
3. Tool provides data directly to AI
4. AI analyzes and suggests fix
```

**Both approaches work. The key is: gather context FIRST.**

**Tool-assisted is faster, but manual always works.**

### Leading AI Through Complex Debugging

**For complex issues, be the investigator:**

```
Developer: "Payment flow fails sometimes. Let me investigate."

[Tests payment flow multiple times]
[Notices pattern]

Developer: "I found a pattern:
- Works 80% of the time
- Fails when user clicks Pay button quickly after page load
- Console error only appears on fast clicks
- Error: 'paymentProcessor is not initialized'

Let me check initialization code..."

[Checks code]

Developer: "Found it:
- Payment processor initializes async
- Pay button is enabled immediately
- If user clicks before initialization completes, it fails

AI: The button should be disabled until processor is ready.
Here's the fix: [solution]"
```

**You lead the investigation. AI provides solutions based on what you find.**

---

## The "Starting Over" Myth

### The 20-Hour Project Scenario

**Situation:**
> "I've been working on this project for 20 hours. Now there's a bug I can't fix. Should I start over?"

**Absolutely not.**

**Why this happens:**

1. **Frustration Clouds Judgment**
   - After debugging for hours without progress
   - Feel like everything is broken
   - Think starting fresh will be easier

2. **Missing: It's Not the Project, It's the Process**
   - Your code isn't the problem
   - Your debugging approach is
   - Starting over will lead to same issue

3. **Confusion: New Chat vs New Project**
   - ✅ **New chat window**: Good idea! Fresh context, clear conversation
   - ❌ **New project**: Waste of 20 hours, doesn't solve anything

### When "Starting Over" Makes Sense

#### ✅ Start New Chat Window When:

- Conversation got too long and cluttered
- Need to reorganize your thoughts
- Want to try different approach to same problem
- Current chat is full of dead ends and confusion

**You keep the project. Just fresh conversation.**

#### ✅ Start New Project When:

- You built a prototype to test concept (now building for real)
- Architecture is fundamentally wrong for requirements
- Used wrong tech stack for the use case
- Learning project → now building production version

**Rare situations. Usually not the answer.**

#### ❌ Don't Start Over When:

- You haven't gathered proper context yet
- You haven't checked basic errors
- You're frustrated but don't know what's wrong
- AI isn't "getting it" (problem: your context, not AI)
- Project is complex (20+ hours invested)

### The Real Fix: Debug Your Process

**Instead of starting over:**

```
1. Stop coding for 30 minutes
2. Step back and investigate properly
3. Open DevTools
4. Reproduce the issue methodically
5. Gather complete context
6. Document what you find
7. THEN ask AI with full context
```

**If you've spent 20 hours on a project:**
- You have working code
- You have architecture
- You have logic
- You have UI
- Starting over throws away all of that

**Better approach:**
```
"I've hit a wall on this 20-hour project. Before I do anything drastic,
let me investigate this bug properly.

[Spends 30 minutes gathering context]
[Finds the actual issue]

Oh. It's a typo in an environment variable.
[Fixes in 2 minutes]

Imagine if I had started over..."
```

### Starting Over Is Easy, Debugging Is Professional

**Junior mindset:**
> "This is hard. Let me start over and do it differently."

**Professional mindset:**
> "This is hard. Let me investigate systematically, understand the root cause, and fix it properly."

**Starting over is avoiding the problem, not solving it.**

---

## Common Scenarios

### Scenario 1: "It Works Locally But Not in Production"

#### ❌ Bad Approach
```
Developer: "It works on my machine but not in production. Deploy it again."

AI: "Try rebuilding and redeploying..."

Developer: "Still doesn't work in production."
```

#### ✅ Good Approach
```
Developer: "Works locally, fails in production. Let me check differences:

LOCAL ENVIRONMENT:
- Node version: 18.x
- Environment vars: [lists vars]
- Database: localhost
- API endpoint: http://localhost:3000

PRODUCTION ENVIRONMENT:
- Node version: 16.x (DIFFERENT!)
- Environment vars: [checks deploy config]
  → Missing: DATABASE_URL ❌
  → Missing: API_KEY ❌
- Database: [production URL]
- API endpoint: https://api.production.com

PRODUCTION LOGS:
Error: Cannot find module 'some-package'
→ Package uses Node 18 features
→ Production is Node 16

ISSUES FOUND:
1. Node version mismatch
2. Missing environment variables
3. Dependency incompatibility

Now I can ask AI: 'How do I configure production environment to match
local requirements and handle version differences?'"
```

### Scenario 2: "Tests Are Failing"

#### ❌ Bad Approach
```
Developer: "Tests failing after my changes. Fix the tests."

AI: "Here's updated test code..."

Developer: "Still 10 tests failing."
```

#### ✅ Good Approach
```
Developer: "Tests failing. Let me see which ones and why:

TEST RESULTS:
✅ 45 passing
❌ 10 failing

FAILING TESTS (common pattern):
- All in auth.test.js
- All expect specific API response format
- All fail with: "Expected object, got undefined"

MY CHANGES:
- Modified API response structure
- Changed from { data: { user } } to { user }
- Tests expect old structure

ROOT CAUSE: Tests are correct for old API structure.
My code changed API structure.

OPTIONS:
1. Update tests to match new structure (if new structure is better)
2. Revert to old structure (if tests represent contract)
3. Support both for backward compatibility

AI: Which approach fits this API use case best?"
```

### Scenario 3: "Random Intermittent Errors"

#### ❌ Bad Approach
```
Developer: "Sometimes get random errors. No pattern. Fix it."

AI: "Try adding error handling..."

Developer: "Still happening randomly."
```

#### ✅ Good Approach
```
Developer: "Getting intermittent errors. Let me gather data:

OBSERVATION:
- Error appears ~30% of requests
- No obvious pattern at first
- Same code, different results

INVESTIGATION:
[Monitors for 10 requests]
[Notes which ones fail]

PATTERN FOUND:
- Fails when server response takes >5 seconds
- Fails when multiple requests in parallel
- Fails specifically on: /api/data endpoint

ERROR MESSAGE (when it happens):
"TypeError: Cannot read property 'items' of undefined"

CODE ANALYSIS:
- Endpoint returns data structure: { items: [] }
- But sometimes returns: { error: "Timeout" }
- Code assumes items always exists ❌

ROOT CAUSE: No error handling for timeout responses.
Code expects items array but gets error object.

CONTEXT FOR AI:
'This endpoint returns different structures based on success/timeout.
How should I handle both cases gracefully?'"
```

### Scenario 4: "AI Keeps Giving Wrong Solutions"

#### ❌ Bad Approach
```
Developer: "AI gave me wrong solution 5 times. This AI sucks."
[Switches to different AI]
Developer: "New AI also gives wrong solution."
```

#### ✅ Good Approach
```
Developer: "AI isn't solving this. Let me check MY context:

WHAT I'VE BEEN SAYING:
'Fix the button click handler'

WHAT I HAVEN'T PROVIDED:
- What the button is supposed to do
- What error occurs
- What happens vs what should happen
- Any console errors
- The actual code

Oh. I'm asking AI to fix something without explaining the problem.

NEW APPROACH WITH CONTEXT:
'The submit button should send form data to /api/submit.

EXPECTED: Click → validate → POST request → success message
ACTUAL: Click → nothing happens

CONSOLE ERROR:
ReferenceError: submitForm is not defined
at HTMLButtonElement.onclick (index.html:42)

CODE:
HTML: <button onclick="submitForm()">Submit</button>
JS: No submitForm function defined ❌

AH! The function is called handleSubmit in JS but referenced as
submitForm in HTML.

AI: This is a naming mismatch. Change X to Y?'

AI: 'Yes, exactly. Change onclick="submitForm()" to
onclick="handleSubmit()" or rename the function.'

Developer: 'That was my fault for not providing context.'"
```

---

## Best Practices

### ✅ DO:

1. **Investigate Before Asking**
   - Open DevTools FIRST
   - Check console FIRST
   - Look at network requests FIRST
   - Then ask AI with data

2. **Provide Complete Context**
   - Error messages (exact text)
   - Reproduction steps (exact clicks)
   - Expected vs actual (be specific)
   - Code location (file:line)
   - Environment details (browser/OS/device)

3. **Lead the Investigation**
   - You are AI's eyes and ears
   - You can see runtime state
   - You can open DevTools
   - You reproduce the issue
   - You gather facts
   - AI analyzes facts and provides solutions

4. **Use Tools When Helpful**
   - DevTools MCP for automated context gathering
   - But manual context gathering always works
   - Choose based on what's faster for you

5. **Document Your Findings**
   - Write down what you discover
   - Organize context before sharing
   - Makes it easier for AI to help
   - Makes it easier for you to think clearly

6. **Test Hypotheses Systematically**
   - Change one thing at a time
   - Verify each change
   - Report results back to AI
   - Iterate based on data

7. **New Chat When Needed**
   - Long, cluttered conversation → new chat
   - Keep the project, fresh context
   - Summarize findings from old chat
   - Continue with clean slate

### ❌ DON'T:

1. **Don't Skip Investigation**
   - ❌ "It's broken, fix it"
   - ✅ "Let me check what's broken first"

2. **Don't Expect AI to Be Psychic**
   - ❌ "Something's wrong with the login"
   - ✅ "Login returns 401, console shows: [error], network shows: [data]"

3. **Don't Start Over Prematurely**
   - ❌ "Bug is hard, let me start new project"
   - ✅ "Bug is hard, let me investigate properly"

4. **Don't Provide Vague Context**
   - ❌ "Page is slow"
   - ✅ "Page load takes 8 seconds, DevTools shows 12MB image loading"

5. **Don't Guess at Solutions**
   - ❌ "Maybe it's the database? Or caching? Or...?"
   - ✅ "Let me gather data to identify the actual bottleneck"

6. **Don't Blame the Tools**
   - ❌ "This AI model is bad at debugging"
   - ✅ "I need to provide better context for the AI"

7. **Don't Rush**
   - ❌ "Quick, try random fixes until something works"
   - ✅ "Take 10 minutes to investigate properly, save hours of guessing"

---

## Summary: The Human-First Debugging Mindset

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  95% of "AI can't debug this" is actually                   │
│  "Human didn't provide context"                             │
│                                                             │
│  BEFORE asking AI to debug:                                 │
│  1. Open DevTools                                           │
│  2. Check console errors                                    │
│  3. Check network requests                                  │
│  4. Reproduce the issue                                     │
│  5. Gather complete context                                 │
│                                                             │
│  THEN provide AI with:                                      │
│  - Exact error messages                                     │
│  - Reproduction steps                                       │
│  - Expected vs actual behavior                              │
│  - Network request/response data                            │
│  - Code location                                            │
│  - Environment details                                      │
│                                                             │
│  AI is your pair programmer, not a psychic.                 │
│  You are AI's eyes. Gather context. Then collaborate.       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Remember:

- **You wouldn't restart a 20-hour project in traditional development**
- **Don't restart it in AI-assisted development either**
- **Fix the process (context gathering), not the project**
- **New chat ≠ new project**
- **Investigation before automation**
- **Human context first, AI solutions second**

---

## Related Resources

- [Troubleshooting Guide](README.md) - Complete troubleshooting reference
- [Debugging Prompts](../prompting/task-specific-patterns.md#debugging--error-resolution) - Templates for effective debugging communication
- [Phase 3: Testing & Debugging](../workflow/phase-3-testing-debugging.md) - Workflow integration
- [DevTools MCP Setup](../workflow/phase-2-development.md#prerequisites-environment-setup) - Optional tool-assisted context gathering

---

**The uncomfortable truth?**

Most debugging problems are human context problems.

**The good news?**

Now you know how to fix them. 🎯
