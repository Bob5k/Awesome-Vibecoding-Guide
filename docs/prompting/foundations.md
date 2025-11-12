# Prompt Engineering Foundations 🎯

**Master the fundamentals of communicating with AI coding assistants effectively**

---

## Table of Contents

1. [Introduction](#introduction)
2. [The Anatomy of a Good Prompt](#the-anatomy-of-a-good-prompt)
3. [Universal Principles](#universal-principles)
4. [Context Loading Strategies](#context-loading-strategies)
5. [Common Anti-Patterns](#common-anti-patterns)
6. [Prompt Evolution](#prompt-evolution)
7. [Measuring Prompt Quality](#measuring-prompt-quality)
8. [Best Practices Checklist](#best-practices-checklist)

---

## Introduction

### Why Prompt Engineering Matters in Vibecoding

**The reality:** Your coding speed with AI is directly proportional to your prompting skill.

```
Vague prompt → 10 iterations → 30 minutes wasted → Frustrated developer
Clear prompt → 1-2 iterations → 5 minutes total → Productive developer
```

**The economics:**
- **Bad prompt:** 3,000 tokens × 10 iterations = 30,000 tokens = $0.60 + your time
- **Good prompt:** 500 tokens × 2 iterations = 1,000 tokens = $0.02 + minimal time

**Cost savings:** 97% fewer tokens, 6× faster implementation

**This guide teaches you:** How to consistently write prompts that get high-quality code on the first or second try.

---

## The Anatomy of a Good Prompt

### The Four Components Framework

Every effective prompt has four elements:

```
┌─────────────────────────────────────────────┐
│         EFFECTIVE CODING PROMPT             │
├─────────────────────────────────────────────┤
│  1. CLARITY      │  What you want           │
│  2. CONTEXT      │  What AI needs to know   │
│  3. CONSTRAINTS  │  Boundaries & requirements│
│  4. CRITERIA     │  How to verify success   │
└─────────────────────────────────────────────┘
```

### 1. Clarity: What You Want

**Definition:** Specific, unambiguous description of the desired outcome.

**Bad (Vague):**
```
"Fix the authentication"
```

**Why it fails:**
- What needs fixing? Login? Registration? Password reset?
- What's broken? Error? Performance? Security?
- Which files? Which functions?

**Good (Clear):**
```
"Fix the JWT token expiration handling in src/auth/middleware.ts.
Currently, expired tokens return 500 errors instead of 401 Unauthorized."
```

**Why it works:**
- ✅ Specific file and function
- ✅ Clear problem statement
- ✅ Expected behavior defined
- ✅ Current behavior described

---

### 2. Context: What AI Needs to Know

**Definition:** Relevant information about your project, architecture, and conventions.

**Types of context:**

```
┌──────────────────────────────────────┐
│  Project Context Types               │
├──────────────────────────────────────┤
│  • Architecture patterns             │
│  • Tech stack specifics              │
│  • Coding conventions                │
│  • Related files/functions           │
│  • Business logic constraints        │
│  • Previous decisions                │
└──────────────────────────────────────┘
```

**Example:**

**Bad (No context):**
```
"Add user registration endpoint"
```

**Good (With context):**
```
"Add user registration endpoint to src/api/auth.ts following the pattern
used in src/api/posts.ts. Use our existing ValidationMiddleware from
src/middleware/validation.ts. Database schema is in src/models/User.ts.
We use bcrypt for password hashing (see src/utils/crypto.ts for examples)."
```

**Context sources:**
- Documentation files (`docs/architecture/*.md`)
- Existing code patterns (reference similar implementations)
- `.cursorrules` or `.clauderules` (project conventions)
- ADRs (Architecture Decision Records)

---

### 3. Constraints: Boundaries & Requirements

**Definition:** Rules, limitations, and requirements that must be followed.

**Common constraint types:**

```
Technical Constraints:
├─ Performance requirements
├─ Security requirements
├─ Compatibility requirements
├─ Dependency restrictions
└─ Resource limitations

Business Constraints:
├─ Legal/compliance requirements
├─ UX requirements
├─ Timeline considerations
└─ Budget limitations

Code Quality Constraints:
├─ Test coverage requirements
├─ Code style guidelines
├─ Documentation requirements
└─ Maintainability standards
```

**Example:**

**Without constraints:**
```
"Create a file upload feature"
```

**With constraints:**
```
"Create a file upload feature with these constraints:
- Max file size: 10MB
- Allowed types: PDF, PNG, JPG only
- Must validate file type server-side (not just extension)
- Use streaming upload for files >1MB to avoid memory issues
- Must work with our existing S3-compatible storage (Cloudflare R2)
- Error messages must be user-friendly, not technical
- Must include progress indicator for uploads >2MB
- Security: implement CSRF protection
- Must write integration tests"
```

**Why constraints matter:**
- Prevent over-engineering
- Ensure security is considered
- Guide architectural decisions
- Set clear scope boundaries

---

### 4. Success Criteria: How to Verify

**Definition:** Concrete, measurable ways to determine if the implementation is correct.

**Types of success criteria:**

```
Functional Criteria:
├─ Expected behavior descriptions
├─ Test scenarios that must pass
├─ Edge cases to handle
└─ Integration requirements

Quality Criteria:
├─ Performance metrics
├─ Security checks
├─ Code coverage targets
└─ Accessibility standards

User Experience Criteria:
├─ UI/UX requirements
├─ Error message quality
├─ Loading states
└─ Responsive behavior
```

**Example:**

**Without success criteria:**
```
"Implement pagination for the user list"
```

**With success criteria:**
```
"Implement pagination for the user list. Success means:

Functional:
- Displays 20 users per page
- Navigation works (prev/next, page numbers)
- URL updates with page number (?page=2)
- Maintains filters/sorting when paginating
- Shows 'No users found' when page is empty

Performance:
- Loads in <500ms for 10k total users
- No n+1 query problems

UX:
- Shows loading state during fetch
- Disables prev on first page, next on last
- Shows current page (e.g., "Page 2 of 15")
- Keyboard navigation works (arrow keys)

Testing:
- Unit tests for pagination logic
- Integration test for the full flow"
```

**Why this matters:**
- AI knows when it's done
- You can verify objectively
- Reduces back-and-forth iterations
- Sets clear expectations

---

## Universal Principles

### Principle 1: Be Specific, Not Vague

**Rule:** Every word in your prompt should add useful information.

**Transformation examples:**

| Vague ❌ | Specific ✅ |
|---------|-----------|
| "Make it better" | "Reduce response time from 2s to <500ms by adding database indexes" |
| "Fix the bug" | "Fix null pointer exception in UserService.findById when user doesn't exist" |
| "Add error handling" | "Wrap API calls in try-catch, return user-friendly messages, log errors to Sentry" |
| "Improve security" | "Add rate limiting (10 req/min), input sanitization, and JWT expiration validation" |
| "Make it responsive" | "Use Tailwind breakpoints: stack on mobile (<768px), 2-col on tablet, 3-col on desktop" |

**Practice:**

Before sending a prompt, ask yourself:
- "Could this be more specific?" → If yes, make it more specific
- "Would someone unfamiliar with my project understand?" → If no, add context
- "Can I quantify this requirement?" → If yes, add numbers/metrics

---

### Principle 2: Show, Don't Just Tell

**Rule:** Provide examples of what you want, don't just describe it.

**Why examples matter:**
- Different people interpret words differently
- Examples eliminate ambiguity
- AI learns patterns from examples
- Reduces misunderstanding

**Pattern:**

```
[Description] + [Example input/output] + [Edge cases]
```

**Example:**

**Just telling (unclear):**
```
"Format dates in a user-friendly way"
```

**Showing (clear):**
```
"Format dates in a user-friendly relative format:
- Today: 'Today at 2:30 PM'
- Yesterday: 'Yesterday at 2:30 PM'
- This week: 'Monday at 2:30 PM'
- This year: 'March 15 at 2:30 PM'
- Older: 'March 15, 2023'

Use 12-hour time with AM/PM. Handle timezone correctly (user's local time).

Edge cases:
- Just now (<1 min ago): 'Just now'
- Invalid date: 'Invalid date'
- Future dates: Use absolute format"
```

**Real-world scenario:**

**Before (vague):**
```
"Create an error message component"
```

**After (with examples):**
```
"Create an ErrorMessage component that displays errors like this:

Example 1 (Field error):
  [X] Email is required

Example 2 (API error):
  [!] Failed to save user. Please try again.

Example 3 (Multiple errors):
  [!] Please fix the following:
      • Email is required
      • Password must be at least 8 characters

Props:
- error: string | string[]
- type: 'field' | 'api' | 'warning'
- dismissible?: boolean

Styling:
- Red border and icon for 'field' and 'api'
- Yellow for 'warning'
- Use Tailwind colors: red-500, yellow-500
- Icon from Heroicons"
```

---

### Principle 3: Use Incremental Refinement

**Rule:** Start broad, then narrow down. Don't try to perfect the prompt on first try.

**The iteration pattern:**

```
Iteration 1: Basic request → Get working code
Iteration 2: Add constraints → Refine implementation
Iteration 3: Handle edge cases → Polish
```

**Example progression:**

**Iteration 1 (Get it working):**
```
"Create a search function for user names in src/api/users.ts"
```

↓ *AI generates basic search*

**Iteration 2 (Add requirements):**
```
"Update the search to:
- Be case-insensitive
- Search both first name and last name
- Return results sorted by relevance (exact match first)"
```

↓ *AI refines implementation*

**Iteration 3 (Edge cases):**
```
"Handle these edge cases:
- Empty search query → return all users
- Special characters → escape properly
- Very long query (>100 chars) → truncate and warn"
```

**Why this works:**
- Each iteration builds on previous work
- AI maintains context better
- You can verify at each step
- Less overwhelming than one massive prompt

**When to use single-shot vs iteration:**

| Scenario | Approach |
|----------|----------|
| Simple, well-defined task | Single comprehensive prompt |
| Complex feature | Iterative refinement |
| Uncertain requirements | Start simple, iterate |
| Known patterns | Single detailed prompt |
| New territory | Explore with iterations |

---

### Principle 4: Reference Files and Patterns Explicitly

**Rule:** Tell AI exactly where to look for context and patterns to follow.

**Pattern structure:**

```
"[Task] following the pattern in [reference file].
Use [specific function/class] as example.
Context in [docs file]."
```

**Examples:**

**Bad (no references):**
```
"Add a new API endpoint for creating posts"
```

**Good (with references):**
```
"Add a new POST /api/posts endpoint to src/api/posts.ts following
the same pattern as POST /api/users in src/api/users.ts.

Specifically:
- Use the same validation middleware approach
- Follow the same error handling pattern
- Use the same response format (201 Created with location header)

Database schema is in src/models/Post.ts.
Authentication middleware in src/middleware/auth.ts."
```

**Reference types:**

```
├─ Code patterns: "Following the pattern in [file]"
├─ Architecture docs: "Per architecture in docs/architecture/api-design.md"
├─ Similar features: "Like the user registration flow in src/api/auth.ts"
├─ Style guide: "Following our conventions in .cursorrules"
└─ Decision records: "As decided in docs/decisions/001-api-design.md"
```

**Benefits:**
- AI understands your project's style
- Consistent code across features
- Reduces need to explain conventions
- Faster, more accurate implementations

---

### Principle 5: Separate Concerns in Prompts

**Rule:** Don't mix multiple unrelated tasks in one prompt.

**Bad (mixed concerns):**
```
"Add user authentication, fix the broken pagination on the posts page,
and update the styling of the header to match the new design"
```

**Why it fails:**
- AI context split across three different areas
- Harder to verify each part
- Difficult to debug if one part fails
- Increases cognitive load

**Good (separated):**

**Prompt 1:**
```
"Implement user authentication with JWT tokens in src/api/auth.ts"
```

**Prompt 2 (after first is complete):**
```
"Fix pagination bug in src/components/PostList.tsx where next button
appears on last page"
```

**Prompt 3 (after second is complete):**
```
"Update header styling in src/components/Header.tsx to match the design
in designs/header-v2.png"
```

**Exception:** Related tasks that must be done together can be combined:

```
"Add password reset functionality:
1. POST /api/auth/reset-request endpoint (generates token, sends email)
2. POST /api/auth/reset-confirm endpoint (validates token, updates password)
3. Update User model to include resetToken and resetTokenExpiry fields

These must be implemented together for the feature to work."
```

**Decision framework:**

```
Ask: "Could these tasks be done by different developers independently?"
├─ YES → Separate prompts
└─ NO → Combined prompt OK
```

---

## Context Loading Strategies

### The Context Hierarchy

**Understand AI's perspective:**

```
┌─────────────────────────────────────────┐
│  How AI Sees Your Context (Priority)   │
├─────────────────────────────────────────┤
│  1. Your current prompt (highest)       │
│  2. Recently included files             │
│  3. Previous conversation               │
│  4. Project configuration files         │
│  5. Earlier context (lowest)            │
└─────────────────────────────────────────┘
```

**Implication:** Most recent, most explicitly mentioned context has highest impact.

---

### Strategy 1: Just-In-Time Context Loading

**Principle:** Include only what's needed for the current task, load more as needed.

**Anti-pattern:**
```
"Include all files in src/ just in case"
[AI context bloated, performance degrades]
```

**Better pattern:**
```
Session start: Include only task description + architecture overview
Step 1: Load 2-3 files directly relevant to current task
Step 2: If AI needs more context, add specific files
Step 3: Complete task, remove files from context
```

**Example workflow:**

**Initial prompt:**
```
"Read docs/architecture/api-design.md. I need to add a new endpoint
for user profile updates. Don't implement yet, just confirm you
understand the architecture."
```

↓ *AI confirms understanding*

**Implementation prompt:**
```
"Now implement PUT /api/users/:id in src/api/users.ts. Include:
- src/api/users.ts (existing endpoints for pattern)
- src/models/User.ts (schema)
- src/middleware/validation.ts (validation approach)"
```

**Result:**
- Minimal context usage
- AI has exactly what it needs
- Can scale to large implementations

---

### Strategy 2: Documentation-First Approach

**Principle:** Write plans to .md files, reference them in prompts.

**The pattern:**

```
┌──────────────────────────────────────────┐
│  1. Write plan to docs/plans/feature.md │
│  2. Prompt: "Implement plan in [file]"  │
│  3. AI reads plan (one-time context cost)│
│  4. AI implements (minimal prompt needed)│
└──────────────────────────────────────────┘
```

**Benefits:**
- Plan reusable across sessions
- Version controlled
- Human editable
- Zero context cost after initial read

**Example:**

**Instead of:**
```
"Add user authentication with these requirements: [3000 words]"
[Uses massive context every time you mention it]
```

**Do this:**
```
You: "Create docs/plans/authentication.md with comprehensive plan"
AI: [Writes detailed plan]
You: [Review and edit plan]
You: "Implement docs/plans/authentication.md"
AI: [Reads plan, implements]
```

**Context savings:**
- Initial approach: 3,000 tokens per prompt × 10 prompts = 30,000 tokens
- Documentation approach: 3,000 tokens once + 10 × 20 tokens = 3,200 tokens
- **Savings: 89% fewer tokens**

---

### Strategy 3: Progressive Disclosure

**Principle:** Reveal complexity gradually, not all at once.

**Pattern:**

```
Level 1: High-level architecture
Level 2: Component details
Level 3: Implementation specifics
Level 4: Edge cases and optimization
```

**Example: Complex Feature Implementation**

**Level 1 (Architecture):**
```
"We're building a real-time chat feature. Architecture:
- Frontend: React components in src/components/chat/
- Backend: WebSocket server in src/websocket/chat.ts
- Database: Messages in D1 (Cloudflare)
- State: Zustand store

Read docs/architecture/realtime-chat.md for full details.
Do you understand the overall approach?"
```

↓ *AI confirms*

**Level 2 (Component structure):**
```
"Let's start with the frontend structure. Create these components:
- ChatWindow (container)
- MessageList (displays messages)
- MessageInput (user input)
- UserList (online users)

Don't implement yet, just create the file structure and component
skeletons with props/types."
```

↓ *AI creates structure*

**Level 3 (Implementation):**
```
"Now implement MessageList component. Include:
- Virtual scrolling for 1000+ messages
- Auto-scroll to bottom on new message
- Load more when scrolling to top

Reference src/components/feed/PostList.tsx for virtual scrolling pattern."
```

↓ *AI implements*

**Level 4 (Polish):**
```
"Add these enhancements to MessageList:
- Scroll to first unread message on mount
- Highlight mentions (@username)
- Show 'user is typing' indicator
- Handle message edits/deletes"
```

**Why this works:**
- AI not overwhelmed by complexity
- You verify at each level
- Easy to course-correct
- Natural debugging points

---

### Strategy 4: Smart File References

**Principle:** Reference files strategically based on what AI needs.

**Reference types:**

```
1. Pattern reference: "Follow the pattern in [file]"
   → AI learns style, doesn't need full file content

2. Schema reference: "Schema in [file]"
   → AI needs to read file for structure

3. Integration reference: "Integrates with [file]"
   → AI needs to understand interface

4. Context reference: "Related logic in [file]"
   → AI should be aware, may need to read
```

**Example:**

```
"Implement user profile update endpoint.

Pattern: Follow POST /users pattern in src/api/users.ts (lines 45-78)
Schema: User model in src/models/User.ts
Integration: Use ValidationMiddleware from src/middleware/validation.ts
Context: Related authentication logic in src/api/auth.ts (FYI, no need to read unless relevant)"
```

**File reference syntax:**

```
Full file: "Read src/api/users.ts"
Specific function: "See handleUserUpdate in src/api/users.ts"
Line range: "Pattern in src/api/users.ts lines 45-78"
Multiple files: "Read src/api/users.ts and src/models/User.ts"
```

---

### Strategy 5: Context Anchoring

**Principle:** Establish stable reference points that persist across conversation.

**Anchor types:**

```
└─ Architecture documents (docs/architecture/)
└─ Project conventions (.cursorrules)
└─ Key examples (well-implemented features)
└─ Decision records (docs/decisions/)
```

**Pattern:**

**Session start:**
```
"This session, our anchors are:
1. API design: docs/architecture/api-design.md
2. Code style: .cursorrules
3. Database patterns: src/database/BaseRepository.ts

Reference these for all implementations. Confirm you've read them."
```

**During session:**
```
"Per our API design anchor, implement GET /api/users/:id"
[AI remembers the anchor document, follows conventions]
```

**Benefits:**
- Consistent references across conversation
- Reduces need to repeat context
- AI develops "mental model" of your project
- Easier to maintain conversation coherence

---

## Common Anti-Patterns

### Anti-Pattern 1: The Vague Hope

**Description:** Hoping AI will "figure out" what you want without clear guidance.

**Example:**
```
"Make the app better"
```

**Why it fails:**
- "Better" is subjective
- No measurable outcome
- AI guesses randomly
- Wastes your time reviewing irrelevant changes

**Fix:**
```
"Improve the user list page performance:
- Current: 3s load time with 1000 users
- Target: <500ms load time
- Approach: Implement virtual scrolling and pagination
- Measure: Use browser Performance API"
```

**Lesson:** If you can't measure it, AI can't optimize for it.

---

### Anti-Pattern 2: The Context Dump

**Description:** Including everything "just in case" without direction.

**Example:**
```
"Here's my entire codebase: [pastes 50 files]
Now fix the login bug"
```

**Why it fails:**
- AI overwhelmed by irrelevant context
- Increases cost (tokens)
- Slower responses
- AI may focus on wrong areas

**Fix:**
```
"Login bug: Users get 500 error on submit.

Relevant files:
- src/api/auth.ts (login endpoint, line 45 throws error)
- src/middleware/validation.ts (validates login request)
- Error log: [paste specific error message]

Expected: 200 OK with JWT token
Actual: 500 Internal Server Error"
```

**Lesson:** Quality of context > quantity of context

---

### Anti-Pattern 3: The Assumption Trap

**Description:** Assuming AI knows your project specifics without explanation.

**Example:**
```
"Add the feature we discussed"
```

**Why it fails:**
- AI has no previous conversation (if new session)
- Even in same session, may not remember details
- Ambiguous reference

**Fix:**
```
"Add the user role-based access control feature:
- Three roles: admin, editor, viewer (as documented in docs/plans/rbac.md)
- Middleware in src/middleware/rbac.ts
- Role checked on every API request
- Follows the pattern from our auth middleware"
```

**Lesson:** Be explicit. Never assume "the AI knows."

---

### Anti-Pattern 4: The Moving Target

**Description:** Changing requirements mid-implementation without clear communication.

**Example:**
```
Prompt 1: "Add pagination with 10 items per page"
[AI implements]
Prompt 2: "Actually make it 20, and add filters, and sorting, and..."
[AI confused about what to keep vs change]
```

**Why it fails:**
- Unclear what's changing vs staying same
- AI may redo everything unnecessarily
- Context becomes messy

**Fix:**
```
Prompt 2: "Keep the pagination structure you built, but update:
- Change items per page from 10 → 20
- Add these NEW features:
  - Filter by status (dropdown)
  - Sort by date/name (toggle)

Don't change: the existing pagination logic, URL params, or API structure"
```

**Lesson:** Clearly distinguish changes from additions from deletions.

---

### Anti-Pattern 5: The No-Verify

**Description:** Not providing success criteria, so AI has no definition of "done."

**Example:**
```
"Implement user search"
[AI implements something]
You: "That's not what I wanted"
[Repeat 5 times]
```

**Why it fails:**
- AI guessing what "done" means
- No objective measure
- Frustration on both sides

**Fix:**
```
"Implement user search. Success means:

Must have:
- Search box in header
- Searches first name, last name, email
- Results appear in dropdown below search box
- Click result → navigate to user profile
- Debounce search (500ms)

Nice to have (if time):
- Highlight matching text
- Show user avatar in results
- Keyboard navigation (arrow keys)

Test it with:
- Empty search → no results dropdown
- 'john' → shows all Johns
- Special chars → no errors"
```

**Lesson:** Define "done" explicitly and objectively.

---

### Anti-Pattern 6: The Tool Mismatch

**Description:** Using the wrong prompting approach for the tool or model.

**Example:**
```
[Using single-shot prompt for exploration task]
"Explore the codebase and figure out why it's slow"
[AI gives generic advice instead of investigating]
```

**Why it fails:**
- Some tasks need multiple rounds
- Single prompt can't cover open-ended exploration
- Context management matters

**Fix:**

**Iteration 1:**
```
"Analyze the user list page performance. Read src/pages/UserList.tsx
and report what you find."
```

**Iteration 2 (based on findings):**
```
"You found N+1 queries. Read src/api/users.ts and propose a fix
using eager loading."
```

**Iteration 3:**
```
"Implement your proposed fix with the necessary database query changes."
```

**Lesson:** Match prompt style to task type (exploration vs implementation vs debugging).

---

### Anti-Pattern 7: The Ignored Error

**Description:** Not providing error messages and logs when debugging.

**Example:**
```
"The login doesn't work, fix it"
```

**Why it fails:**
- AI has to guess the problem
- Wastes time on wrong issues
- May not fix actual bug

**Fix:**
```
"Login fails with this error:

Error message:
  TypeError: Cannot read property 'id' of undefined
  at src/api/auth.ts:45

Stack trace:
  at handleLogin (src/api/auth.ts:45:10)
  at src/middleware/validation.ts:12:5

What happens:
- User submits login form
- Request reaches handleLogin
- Crashes on line 45 when accessing user.id

Context:
- This started after we added email verification
- Only happens for unverified users
- Verified users can log in fine

Relevant code: src/api/auth.ts lines 40-50"
```

**Lesson:** Debugging requires data. Provide error messages, stack traces, and context.

---

### Anti-Pattern 8: The Scope Creep

**Description:** Continuously adding requirements without clear task boundaries.

**Example:**
```
"Add a contact form"
[AI starts]
"Oh also add email validation"
[AI adjusts]
"And send to multiple recipients"
[AI adjusts]
"And log submissions to database"
[AI confused about what version to implement]
```

**Why it fails:**
- AI may redo work multiple times
- Unclear what's in scope
- Context becomes messy
- Implementation may be inconsistent

**Fix:**

**Option 1: Plan first**
```
"I need a contact form. Let me think through requirements first:
- Form fields: name, email, subject, message
- Validation: email format, required fields
- Submission: send email to admin@example.com
- Logging: save to database
- UX: show success message, clear form

Create docs/plans/contact-form.md with implementation plan."

[Review plan]

"Implement docs/plans/contact-form.md"
```

**Option 2: Iterative with clear phases**
```
Phase 1: "Create basic form with validation"
[Complete]
Phase 2: "Add email sending using existing EmailService"
[Complete]
Phase 3: "Add database logging"
```

**Lesson:** Define complete scope upfront OR use clear iterative phases.

---

### Anti-Pattern 9: The Silent Constraints

**Description:** Having requirements in your head but not communicating them.

**Example:**
```
"Add user registration"
[AI implements with bcrypt]
You: "I wanted argon2, not bcrypt!"
```

**Why it fails:**
- AI makes reasonable assumptions
- You're surprised by choices
- Wasted implementation time

**Fix:**
```
"Add user registration with these specifics:

Password hashing: Use argon2 (not bcrypt) - security requirement
Database: Use our existing UserRepository pattern
Validation: Email format + password strength (8+ chars, must include number)
Email: Send welcome email using EmailService (don't implement inline)
Errors: Return 400 with field-specific errors (not generic 500)
Tests: Include integration test for full flow"
```

**Lesson:** If it matters, state it explicitly. Don't assume AI will guess your preferences.

---

### Anti-Pattern 10: The Over-Engineer Request

**Description:** Asking for more complexity than needed.

**Example:**
```
"Build a scalable microservices architecture with event sourcing,
CQRS, distributed tracing, and GraphQL for this simple blog app"
```

**Why it fails:**
- Massive scope
- Over-complicated for requirements
- Takes forever to implement
- Hard to maintain

**Fix:**
```
"Build a simple blog app:
- Monolithic architecture (one codebase)
- REST API (we know it well)
- PostgreSQL (our standard)
- Authentication with JWT

Keep it simple. We can scale later if needed.

Requirements:
- Posts: create, read, update, delete
- Comments: create, read, delete
- Users: register, login, profile
- Admin: manage all content"
```

**Lesson:** Start simple. Add complexity only when needed. YAGNI (You Aren't Gonna Need It).

---

## Prompt Evolution

### How to Refine Prompts Through Practice

**The learning loop:**

```
┌─────────────────────────────────────────┐
│  1. Write prompt                        │
│  2. Get AI response                     │
│  3. Evaluate quality                    │
│  4. Identify what was unclear           │
│  5. Refine prompt                       │
│  6. Document pattern                    │
└─────────────────────────────────────────┘
```

### Pattern Recognition

**Keep a "prompt journal":**

```markdown
## What worked:
- Referencing specific files improved accuracy 90%
- Including examples reduced iterations from 3 to 1
- Breaking into steps: AI understood complex tasks better

## What didn't work:
- Vague "make it better" prompts led nowhere
- Dumping 20 files overwhelmed context
- Mixing debugging + feature work caused confusion

## Patterns discovered:
- Template: "Implement [X] following pattern in [Y]" → 95% success rate
- For debugging: Always include error message + file:line → Faster resolution
- For new features: Write spec first, then implement → More consistent
```

### A/B Testing Your Prompts

**Experiment with variations:**

**Version A (baseline):**
```
"Add sorting to the user table"
```

**Version B (with details):**
```
"Add sorting to the user table in src/components/UserTable.tsx.
Sort by: name, email, created date. Default: name ascending.
Visual indicator: arrow icon next to sorted column."
```

**Measure:**
- How many iterations to working code?
- Was the result closer to what you wanted?
- Token usage difference?
- Time saved?

**Result:** Version B reduced iterations from 4 to 1, saved 10 minutes.

**Action:** Document Version B pattern in your template library.

---

## Measuring Prompt Quality

### Quantitative Metrics

```
┌──────────────────────────────────────────────┐
│  Prompt Quality Scorecard                    │
├──────────────────────────────────────────────┤
│  • Iterations to working code: 1-2 (good)    │
│  • Token usage: Baseline vs actual           │
│  • Time to completion: Target vs actual      │
│  • Code quality: Passes review first time    │
│  • AI confusion signals: Questions asked     │
└──────────────────────────────────────────────┘
```

### Qualitative Indicators

**Good prompt indicators:**
- ✅ AI starts implementing immediately
- ✅ No clarifying questions needed
- ✅ First implementation is close to target
- ✅ Code matches project patterns
- ✅ AI handles edge cases proactively

**Bad prompt indicators:**
- ❌ AI asks many clarifying questions
- ❌ Multiple iterations needed
- ❌ AI makes wrong assumptions
- ❌ Code doesn't match project style
- ❌ Edge cases ignored

### Self-Assessment Questions

After each prompt, ask:

```
1. Could someone else understand exactly what I wanted?
2. Did I provide all necessary context?
3. Did I specify constraints clearly?
4. Did I define success criteria?
5. Would this prompt work in a new session?
```

If any answer is "no," refine the prompt before sending.

---

## Best Practices Checklist

### Before Sending a Prompt

- [ ] **Specificity check:** Is it clear what I want?
- [ ] **Context check:** Does AI have necessary information?
- [ ] **Constraints check:** Are boundaries clearly defined?
- [ ] **Success criteria check:** Can we verify when it's done?
- [ ] **File references check:** Are relevant files/patterns mentioned?
- [ ] **Scope check:** Is this one focused task, or should it be split?
- [ ] **Example check:** Would an example clarify further?
- [ ] **Edge case check:** Have I mentioned important edge cases?

### During Implementation

- [ ] **Progress check:** Is AI on the right track after first response?
- [ ] **Course correction:** If off track, correct immediately
- [ ] **Incremental verification:** Test each piece before moving on
- [ ] **Context monitor:** Is context getting bloated?

### After Completion

- [ ] **Quality check:** Does code meet success criteria?
- [ ] **Pattern recognition:** What worked in this prompt?
- [ ] **Documentation:** Should this pattern be saved?
- [ ] **Iteration analysis:** How many rounds did it take? Why?

---

## Quick Reference

### Prompt Template (Basic)

```
[TASK]: What you want to accomplish

[CONTEXT]:
- Relevant files: [list]
- Architecture: [overview or docs link]
- Patterns to follow: [reference]

[CONSTRAINTS]:
- [constraint 1]
- [constraint 2]

[SUCCESS CRITERIA]:
- [criterion 1]
- [criterion 2]
```

### Prompt Template (Debugging)

```
[PROBLEM]: Brief description

[ERROR MESSAGE]:
[paste exact error]

[CONTEXT]:
- File: [path:line]
- What I was doing: [action]
- Expected behavior: [description]
- Actual behavior: [description]
- Already tried: [list]

[RELEVANT CODE]:
[paste relevant section if short, or reference file]
```

### Prompt Template (Feature)

```
[FEATURE]: Name and brief description

[IMPLEMENTATION PLAN]:
1. [step 1]
2. [step 2]

[REFERENCE PATTERNS]:
- Follow pattern in: [file]
- Similar feature: [description]

[REQUIREMENTS]:
- Must have: [list]
- Nice to have: [list]

[TESTING]:
- [ ] Scenario 1
- [ ] Scenario 2
```

---

## Next Steps

Once you've mastered these foundations:

1. **Task-Specific Patterns** → Learn specialized prompting for debugging, features, refactoring, etc.
2. **Advanced Techniques** → Multi-step workflows, prompt chaining, optimization
3. **Template Library** → Ready-to-use prompts for common scenarios

**Practice exercises:**

1. Take a vague prompt you've used recently and rewrite it using the 4-component framework
2. Create a prompt template for your most common task type
3. Document 3 patterns that work well in your projects
4. Set up a prompt journal to track what works

---

**Related Documentation:**
- [Task-Specific Patterns](./task-specific-patterns.md) → Specialized prompting strategies
- [Advanced Techniques](./advanced-techniques.md) → Expert-level prompting
- [Template Library](./template-library.md) → Ready-to-use prompts
- [Context Management](../context-management/README.md) → Managing AI context effectively
- [Troubleshooting Guide](../troubleshooting/README.md) → When prompts don't work

**Back to:** [Prompting Guide Home](./README.md)
