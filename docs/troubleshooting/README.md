# Vibecoding Troubleshooting Guide 🔧

**Quick solutions for common AI-assisted development problems**

---

## Table of Contents

1. [Quick Symptom Lookup](#quick-symptom-lookup)
2. [Emergency Flowcharts](#emergency-flowcharts)
3. [AI Behavior Issues](#ai-behavior-issues)
4. [Code Quality Problems](#code-quality-problems)
5. [Workflow Bottlenecks](#workflow-bottlenecks)
6. [Tool-Specific Problems](#tool-specific-problems)
7. [Common Error Patterns](#common-error-patterns)
8. [Debugging Checklist](#debugging-checklist)
9. [When to Ask for Help](#when-to-ask-for-help)

---

## Quick Symptom Lookup

**Find your problem → Get quick fix → See detailed solution**

### AI Behavior Issues

| Symptom | Likely Cause | Quick Fix | Details |
|---------|--------------|-----------|---------|
| AI forgets previous decisions | Context overflow >85% | Externalize to .md files | [Context Management](../context-management/#the-60-85-rule) |
| Generates code that doesn't compile | Missing context or incorrect syntax | Provide compiler error + context | [Error Recovery](#error-recovery-prompting) |
| Suggests outdated patterns | No project context loaded | Create .cursorrules file | [Context-Aware Prompting](../prompting/advanced-techniques.md#context-aware-prompting) |
| Makes up APIs/functions that don't exist | Hallucination | Be specific, reference real code | [Specificity Problem](#hallucination-apis-that-dont-exist) |
| Contradictory suggestions | Context confusion | Start fresh session with summary | [Session Reset](#session-reset-recovery) |
| Asks too many clarifying questions | Vague prompt | Use prompt templates | [Prompt Templates](../prompting/template-library.md) |
| Implements wrong feature | Misunderstood requirements | Add concrete examples | [Example-Driven Prompts](#ai-misunderstands-requirements) |
| Ignores constraints | Constraints not explicit | Use numbered list with emphasis | [Constraint Communication](#ai-ignores-constraints) |
| Over-engineers solution | No simplicity guidance | Add "Keep it simple" + constraints | [Over-Engineering](#over-engineering) |
| Generates insecure code | Security not mentioned | Use security checklist | [Security Review](#insecure-code-generation) |
| Slow responses | Context too large | Remove irrelevant files | [Context Optimization](#slow-ai-responses) |
| Incomplete responses (cuts off) | Context limit reached | Break into smaller prompts | [Response Truncation](#incomplete-responses) |
| Different style than project | No style guide referenced | Add style examples | [Code Style Inconsistency](#code-style-doesnt-match-project) |
| Can't debug complex issues | Insufficient data | Provide logs + stack traces | [Debugging Guide](#complex-debugging-failures) |
| Suggests wrong libraries/tools | Lacks project knowledge | Specify tech stack upfront | [Tool Selection](#wrong-library-suggestions) |

---

### Code Quality Problems

| Symptom | Likely Cause | Quick Fix | Details |
|---------|--------------|-----------|---------|
| Buggy code on first try | Vague requirements | Use detailed prompts | [Code Quality Section](#buggy-code-on-first-generation) |
| Missing error handling | Not specified in prompt | Add error handling requirement | [Error Handling](#missing-error-handling) |
| No input validation | Security not mentioned | Specify validation rules | [Input Validation](#missing-input-validation) |
| Poor variable naming | No style guide | Provide naming examples | [Naming Conventions](#poor-variable-naming) |
| Duplicated code | No DRY instruction | Request abstraction | [Code Duplication](#code-duplication) |
| Hard-coded values | No configuration guidance | Ask for config extraction | [Hard-Coded Values](#hard-coded-values) |
| Missing edge case handling | Cases not mentioned | List edge cases explicitly | [Edge Cases](#missing-edge-cases) |
| Performance issues | Efficiency not prioritized | Add performance requirements | [Performance Problems](#poor-performance) |
| No tests generated | Tests not requested | Use test templates | [Testing Templates](../prompting/template-library.md#testing-templates) |
| SQL injection vulnerability | Security not reviewed | Add security audit | [SQL Injection](#sql-injection-vulnerabilities) |
| XSS vulnerability | Input not sanitized | Specify sanitization | [XSS Prevention](#xss-vulnerabilities) |
| Memory leaks | Cleanup not specified | Add cleanup requirements | [Memory Leaks](#memory-leaks) |
| Race conditions | Concurrency not addressed | Specify sync requirements | [Race Conditions](#race-conditions) |
| Tight coupling | Architecture not defined | Request loose coupling | [Tight Coupling](#tight-coupling) |
| Missing documentation | Docs not requested | Use doc templates | [Documentation](#missing-documentation) |

---

### Workflow Bottlenecks

| Symptom | Likely Cause | Quick Fix | Details |
|---------|--------------|-----------|---------|
| Too many iterations | Poor initial prompts | Study prompt foundations | [Prompting Guide](../prompting/foundations.md) |
| Context constantly full | Not using .md files | Externalize plans to docs/ | [MD-Based Workflow](../context-management/#the-md-based-workflow-pattern) |
| Losing work between sessions | No session handoffs | Write handoff docs | [Session Handoffs](../context-management/#session-handoffs) |
| Slow development pace | Sequential instead of parallel | Use parallel prompting | [Parallel Prompting](../prompting/advanced-techniques.md#parallel-prompting) |
| Repeating same explanations | No persistent instructions | Create .cursorrules | [Project Context](#repeating-same-instructions) |
| Can't resume work easily | No documentation | Write current-state.md | [Resumability](#difficulty-resuming-work) |
| Debugging takes too long | Insufficient diagnostic info | Use debug templates | [Debug Templates](../prompting/template-library.md#debugging-templates) |
| Breaking existing features | No integration tests | Add test requirements | [Integration Testing](#breaking-existing-features) |
| Unclear next steps | No task breakdown | Use TodoWrite/Task Manager MCP | [Task Management](#unclear-next-steps) |
| Overwhelmed by complexity | Large tasks not broken down | Use multi-step workflows | [Multi-Step Workflows](../prompting/advanced-techniques.md#multi-step-workflows) |
| Inconsistent code style | No conventions documented | Write style guide | [Style Guide Creation](#inconsistent-code-style) |
| Forgetting project details | No knowledge base | Create project-knowledge.md | [Project Memory](#forgetting-project-details) |
| MCP servers not helping | Wrong MCP for task | Check MCP decision tree | [MCP Usage](../context-management/#mcp-decision-tree) |
| High AI costs | Inefficient prompting | Optimize prompts | [Cost Optimization](#high-ai-costs) |
| Team inconsistency | No shared practices | Create team templates | [Team Coordination](#team-inconsistent-results) |

---

### Tool-Specific Problems

| Tool | Symptom | Quick Fix | Details |
|------|---------|-----------|---------|
| **Claude Code CLI** | Can't find files | Use Glob tool | [File Search](#claude-code-file-search-issues) |
| **Claude Code CLI** | Slow performance | Check context usage | [Performance](#claude-code-slow-performance) |
| **Claude Code CLI** | Task agent fails | Check agent type | [Agent Selection](#claude-code-agent-issues) |
| **Cursor** | Composer fails | Reduce file count | [Composer Issues](#cursor-composer-failures) |
| **Cursor** | Wrong file changes | Be more specific | [File Selection](#cursor-wrong-files) |
| **Windsurf** | Cascade confusion | Clear context | [Cascade Reset](#windsurf-cascade-problems) |
| **Zed** | Workflow not working | Check workflow syntax | [Workflow Debug](#zed-workflow-issues) |
| **Droid CLI** | Plan mode stuck | Break into smaller plan | [Plan Issues](#droid-plan-mode-problems) |
| **Droid CLI** | Act mode fails | Review plan clarity | [Act Issues](#droid-act-mode-failures) |
| **MCP DevTools** | Can't connect | Check browser state | [DevTools Connection](#devtools-mcp-connection-issues) |
| **MCP Context7** | Wrong docs returned | Specify query better | [Context7 Queries](#context7-mcp-issues) |
| **OpenSpec** | Poor spec quality | Provide more detail | [Spec Generation](#openspec-quality-issues) |
| **Git Integration** | Commit failures | Check permissions | [Git Problems](#git-integration-issues) |

---

## Emergency Flowcharts

### Flowchart 1: AI Producing Garbage Code

```
AI generates unusable code?
│
├─ Check 1: Is context > 85% full?
│  ├─ YES → Externalize to .md files
│  │        Start new session with handoff
│  │        ✓ Problem solved
│  │
│  └─ NO → Continue to Check 2
│
├─ Check 2: Is your prompt vague?
│  ├─ YES → Use 4-component framework
│  │        - Clarity: What you want
│  │        - Context: What AI needs
│  │        - Constraints: Boundaries
│  │        - Criteria: Success metrics
│  │        ✓ Try again with better prompt
│  │
│  └─ NO → Continue to Check 3
│
├─ Check 3: Does AI have project context?
│  ├─ NO  → Load architecture docs
│  │        Reference existing patterns
│  │        Create .cursorrules
│  │        ✓ Retry with context
│  │
│  └─ YES → Continue to Check 4
│
├─ Check 4: Is this the right model for the task?
│  ├─ NO  → Switch to better model
│  │        (Claude Sonnet/Opus for complex)
│  │        (GLM/Qwen for standard tasks)
│  │        ✓ Retry with better model
│  │
│  └─ YES → Continue to Check 5
│
└─ Check 5: Is the task too complex for one prompt?
   ├─ YES → Break into multi-step workflow
   │        Verify each step
   │        ✓ Success!
   │
   └─ NO  → Problem is elsewhere
            → Check detailed sections below
```

---

### Flowchart 2: Can't Debug Issue

```
Stuck debugging for >30 minutes?
│
├─ Have you provided error message + stack trace?
│  ├─ NO  → Gather diagnostics:
│  │        - Full error message
│  │        - Stack trace
│  │        - Relevant code (file:line)
│  │        - What you were doing
│  │        ✓ Provide to AI, retry
│  │
│  └─ YES → Continue
│
├─ Have you tried minimal reproduction?
│  ├─ NO  → Create minimal test case
│  │        Remove unrelated code
│  │        Isolate the problem
│  │        ✓ Debug minimal case
│  │
│  └─ YES → Continue
│
├─ Have you checked logs/console?
│  ├─ NO  → Check:
│  │        - Browser console (F12)
│  │        - Server logs
│  │        - Network tab
│  │        - Database logs
│  │        ✓ Gather all error info
│  │
│  └─ YES → Continue
│
├─ Have you searched for similar issues?
│  ├─ NO  → Search:
│  │        - Error message in Google
│  │        - GitHub issues
│  │        - Stack Overflow
│  │        ✓ Try suggested solutions
│  │
│  └─ YES → Continue
│
├─ Have you asked AI with full context?
│  ├─ NO  → Use debug template:
│  │        - Error + stack trace
│  │        - Relevant code
│  │        - What you tried
│  │        - Expected vs actual
│  │        ✓ AI can help now
│  │
│  └─ YES → Time to ask humans
│           → See "When to Ask for Help" section
```

---

### Flowchart 3: High Token Usage / Cost

```
Token costs too high?
│
├─ Are you repeating context every prompt?
│  ├─ YES → Externalize to .md files
│  │        Reference instead of repeating
│  │        Use .cursorrules for conventions
│  │        ✓ 70-90% token savings
│  │
│  └─ NO → Continue
│
├─ Are you loading too many files?
│  ├─ YES → Progressive context loading
│  │        Include only what's needed
│  │        Add more files as needed
│  │        ✓ 50-80% token savings
│  │
│  └─ NO → Continue
│
├─ Are prompts overly verbose?
│  ├─ YES → Use templates
│  │        Reference documentation
│  │        Be concise but specific
│  │        ✓ 40-60% token savings
│  │
│  └─ NO → Continue
│
├─ Are you using multi-step when single-shot works?
│  ├─ YES → Combine related tasks
│  │        Use single comprehensive prompt
│  │        ✓ Reduce prompt count
│  │
│  └─ NO → Continue
│
└─ Using expensive model for simple tasks?
   ├─ YES → Use cheaper models:
   │        - GLM for standard coding
   │        - Qwen for boilerplate
   │        - Claude only for complex
   │        ✓ 80-95% cost savings
   │
   └─ NO  → Costs are probably justified
            Track ROI: time saved vs cost
```

---

### Flowchart 4: Breaking Changes

```
New code breaks existing features?
│
├─ Do you have tests?
│  ├─ NO  → Write tests ASAP
│  │        Run before and after changes
│  │        ✓ Prevent future breakage
│  │
│  └─ YES → Continue
│
├─ Did you run tests before merging?
│  ├─ NO  → Always run tests!
│  │        git checkout previous commit
│  │        ✓ Revert and test
│  │
│  └─ YES → Tests might be incomplete
│
├─ Did you specify "don't break existing features"?
│  ├─ NO  → Always specify:
│  │        "Maintain backward compatibility"
│  │        "Don't change existing API"
│  │        ✓ AI will be more careful
│  │
│  └─ YES → Continue
│
├─ Did you review changes before committing?
│  ├─ NO  → Always review diffs
│  │        Check for unexpected changes
│  │        ✓ Catch issues early
│  │
│  └─ YES → Continue
│
└─ Was the scope too broad?
   ├─ YES → Break into smaller changes
   │        Test incrementally
   │        ✓ Easier to isolate breakage
   │
   └─ NO  → Need better integration tests
            Add test for broken scenario
            ✓ Prevent regression
```

---

## AI Behavior Issues

### AI Misunderstands Requirements

**Symptom:** AI implements something completely different from what you wanted.

**Root causes:**
1. Ambiguous language in prompt
2. Missing examples
3. No success criteria defined
4. Technical terms used differently than AI expects

**Solutions:**

**Solution 1: Use Examples**
> **Bad:** “Create a form with validation.”
>
> **Good:** “Create a form with these exact behaviors:
> - Email field: validate format on blur, show error ‘Invalid email’ below field.
> - Submit disabled until all fields valid.
> - Example: user types ‘test@’ → blur → red border + error shown.”

**Solution 2: Define Success Criteria**
> Add to every prompt:
>
> “Success means:
> - [Specific measurable outcome 1]
> - [Specific measurable outcome 2]
> - [Specific measurable outcome 3]”

**Solution 3: Show, Don't Just Tell**
> Instead of: “Make it look professional.”
>
> Show: “Use this design: [link to screenshot or design].”
>
> Or: “Match the style of [existing component].”

**Prevention:**
- Read [Prompt Foundations](../prompting/foundations.md#principle-2-show-dont-just-tell)
- Use [Prompt Templates](../prompting/template-library.md)
- Always include concrete examples

---

### Hallucination: APIs That Don't Exist

**Symptom:** AI generates code using functions/APIs that don't exist in your project or libraries.

**Example:**
```typescript
// AI generates:
import { magicValidator } from 'my-app/validators'; // DOESN'T EXIST!

user.validateMagically(); // DOESN'T EXIST!
```

**Root causes:**
1. AI guessing based on patterns
2. Confusing your project with similar projects
3. Outdated training data

**Solutions:**

**Solution 1: Reference Real Code**
> Use the existing validation pattern from `src/utils/validation.ts`:
>
> ```typescript
> export function validateEmail(email: string): boolean {
>   return EMAIL_REGEX.test(email);
> }
> ```
>
> Don’t make up new functions. Use this exact pattern.

**Solution 2: Be Explicit About What Exists**
> Available utilities in `src/utils/`:
> - `validation.ts`: `validateEmail`, `validatePassword`
> - `crypto.ts`: `hash`, `verify`
> - `strings.ts`: `slugify`, `truncate`
>
> Use **only** these. Don’t create new utilities.

**Solution 3: Verify After Generation**
> After generating code, verify that all imported functions exist.
>
> If you’re unsure, ask before including them in your response.

**Prevention:**
- Provide explicit file references
- Use "Follow pattern in [existing file]"
- Add verification step to prompts

---

### AI Ignores Constraints

**Symptom:** AI generates code that violates specified constraints (file size limits, no external dependencies, etc.)

**Example:**
```
You: "Don't use any external libraries"
AI: *Installs 5 npm packages*
```

**Root causes:**
1. Constraints buried in long prompt
2. Constraints stated weakly ("try to avoid..." vs "MUST NOT")
3. AI prioritizes functionality over constraints

**Solutions:**

**Solution 1: Emphasize Constraints**
> CRITICAL CONSTRAINTS (must follow):
> 1. **No** external dependencies (use only Node.js built-ins).
> 2. File size **max 100 lines**.
> 3. **No** database queries (work with in-memory data).
>
> If any constraint is impossible, ask before generating code.

**Solution 2: Front-Load Constraints**
> Structure your prompt:
> 1. Constraints **first**.
> 2. Requirements second.
> 3. Implementation details last.
>
> This ensures the AI processes constraints before the solution.

**Solution 3: Use Self-Verifying Prompts**
> After generating code, verify:
> - [ ] No external dependencies used.
> - [ ] File is under 100 lines.
> - [ ] No database queries.
>
> If any check fails, revise the code before responding.

**Prevention:**
- Always list constraints first
- Use strong language ("MUST", "REQUIRED", "NEVER")
- Add verification step

---

### Over-Engineering

**Symptom:** AI generates overly complex solutions with unnecessary abstractions, design patterns, or features.

**Example:**
```
You: "Create a function to add two numbers"
AI: *Creates abstract factory pattern with interfaces, dependency injection, strategy pattern...*
```

**Root causes:**
1. No simplicity guidance
2. AI trained on enterprise codebases
3. No scope boundaries

**Solutions:**

**Solution 1: YAGNI Principle**
> “Create a simple function to add two numbers.
>
> Requirements:
> - Just add two numbers, nothing more.
> - No abstractions, interfaces, or design patterns.
> - Keep it simple (KISS principle).
> - YAGNI: You Aren’t Gonna Need It.
> - Maximum 5 lines of code.”

**Solution 2: Specify Scope Explicitly**
> “Implement **only** what’s needed for the current use case.
> Don’t add:
> - Abstract base classes.
> - Dependency injection.
> - Strategy patterns.
> - Configuration systems.
> - Logging frameworks.
>
> Just solve the immediate problem.”

**Solution 3: Reference Simple Examples**
> “Follow the simplicity of this example:
> [paste simple, direct code]
>
> Keep the same level of simplicity—no additional complexity.”

**Prevention:**
- Always add "Keep it simple"
- Specify maximum lines of code
- Reference simple examples
- Use YAGNI/KISS principles explicitly

---

### Context Overload: AI Forgets Things

**Symptom:** AI forgets previous decisions, contradicts earlier responses, or "doesn't remember" what you discussed.

**Root causes:**
1. Context window >85% full
2. Too many messages in conversation
3. Important info early in conversation (recency bias)

**Solutions:**

**Solution 1: Session Handoff**
> Write a summary of your work to `docs/context/session-handoff.md`:
> - What was implemented.
> - Decisions made (with reasoning).
> - Current state.
> - Next steps.
>
> Be comprehensive—you’ll start a new session after this.
>
> **New session prompt:** “Read `docs/context/session-handoff.md` and continue from where we left off.”

**Solution 2: Externalize Decisions**
> When the AI makes an important decision, document it in `docs/decisions/[number]-[topic].md`:
> - What you decided.
> - Why you decided it.
> - Alternatives considered.
> - Implications.
>
> Future prompts: “Per `docs/decisions/003-auth-approach.md`, implement …”

**Solution 3: Context Refresh**
> If context usage exceeds 70%:
>
> “Summarize our key decisions and current progress. Then we’ll start fresh with that summary.”

**Prevention:**
- Monitor context usage (60-85% rule)
- Externalize to .md files early
- Use [Context Management strategies](../context-management/README.md)

---

### Slow AI Responses

**Symptom:** AI takes >30 seconds to respond, or responses are delayed.

**Root causes:**
1. Context too large (>100k tokens)
2. Too many files included
3. Complex request requiring lots of processing
4. API/model provider issues

**Solutions:**

**Solution 1: Reduce Context**
> “Remove all files from context except:
> - `src/api/users.ts` (relevant to the current task).
> - `docs/architecture/api-design.md`.
>
> Now implement [task].”

**Solution 2: Progressive Loading**
> Don’t load all files at once.
> - Start with minimal context plus an architecture overview.
> - Add files only as needed for the current step.
> - Remove files when a task is complete.

**Solution 3: Use Faster Model**
> For simple tasks:
> - Use GLM (fast, cheap).
> - Use Gemini Flash.
> - Use Qwen Coder.
>
> For complex tasks:
> - Use Claude Sonnet.
> - Use Claude Opus (only when necessary).

**Prevention:**
- Keep context under 50k tokens when possible
- Use [Progressive Loading](../prompting/foundations.md#strategy-1-just-in-time-context-loading)
- Choose right model for task complexity

---

### Incomplete Responses (Cuts Off)

**Symptom:** AI response cuts off mid-sentence or mid-code block.

**Root causes:**
1. Response length limit reached
2. Context window completely full
3. Output token limit hit

**Solutions:**

**Solution 1: Ask to Continue**
> “Continue from where you left off.”
>
> Or be more specific: “Continue the function implementation from line 45.”

**Solution 2: Request Smaller Chunks**
> Instead of: “Implement entire authentication system.”
>
> Do: “Implement just the login function (Step 1 of 5).”
>
> Complete each step before moving to the next.

**Solution 3: Reduce Prompt Size**
> Shorten your prompts:
> - Use template references instead of full requirements.
> - Reference docs instead of pasting content.
> - Focus on the current subtask only.

**Prevention:**
- Break large tasks into steps
- Keep prompts concise
- Monitor context usage

---

### Code Style Doesn't Match Project

**Symptom:** AI generates code in different style (tabs vs spaces, naming conventions, patterns) than your project.

**Root causes:**
1. No style guide provided
2. No example code referenced
3. AI using generic style

**Solutions:**

**Solution 1: Create .cursorrules**

> Create `.cursorrules` in the project root:
>
> ```markdown
> # Code Style Guide
>
> ## Formatting
> - Indentation: 2 spaces (not tabs)
> - Quotes: single quotes for strings
> - Semicolons: required
> - Line length: max 100 characters
>
> ## Naming Conventions
> - Files: kebab-case (user-service.ts)
> - Components: PascalCase (UserCard)
> - Functions: camelCase (getUserById)
> - Constants: UPPER_SNAKE_CASE (API_URL)
>
> ## Patterns
> - React: functional components only (no classes)
> - Async: use async/await (no .then())
> - Errors: custom error classes (not generic Error)
> - Imports: group by type (external, internal, relative)
>
> ## Examples
> [Include code snippets showing style]
> ```
>
> Now the AI automatically follows these conventions.

**Solution 2: Reference Style Examples**
> “Follow the exact code style from `src/components/UserCard.tsx`:
> - Same formatting.
> - Same naming patterns.
> - Same import structure.
> - Same comment style.”

**Solution 3: Request Style Match**
> “Generate code matching the style of [existing file]. Specifically match:
> - Indentation.
> - Naming conventions.
> - Function structure.
> - Comment style.”

**Prevention:**
- Always create .cursorrules early
- Reference existing files for patterns
- Include style requirements in prompt templates

---

## Code Quality Problems

### Buggy Code on First Generation

**Symptom:** AI-generated code has obvious bugs, doesn't compile, or fails immediately when run.

**Root causes:**
1. Ambiguous requirements
2. Missing edge cases
3. Incomplete context
4. Model limitations

**Solutions:**

**Solution 1: Add Test Cases to Prompt**
> “Create a function to calculate factorial.
>
> Must handle:
> - `factorial(0) = 1`
> - `factorial(1) = 1`
> - `factorial(5) = 120`
> - `factorial(-1)` throws `Error('Negative numbers not allowed')`
> - `factorial(100)` uses `BigInt` for large numbers.
>
> Include test cases demonstrating all scenarios work correctly.”

**Solution 2: Request Self-Verification**
> “After generating code, verify:
> 1. Code compiles without errors.
> 2. All test cases pass.
> 3. Edge cases are handled.
> 4. No obvious bugs remain.
>
> If verification fails, fix the code before responding.”

**Solution 3: Provide More Context**
> “Implement user login.
>
> Context:
> - Uses JWT authentication (`src/utils/jwt.ts`).
> - Password hashing with bcrypt (`src/utils/crypto.ts`).
> - User model in `src/models/User.ts`.
> - Error handling pattern from `src/api/posts.ts`.
>
> Reference these files for patterns and interfaces.”

**Prevention:**
- Use detailed prompts with examples
- Include test scenarios
- Reference existing working code
- Add self-verification step

---

### Missing Error Handling

**Symptom:** AI generates happy-path code with no try-catch, no validation, no error responses.

**Root causes:**
1. Error handling not mentioned in prompt
2. AI prioritizes functionality over robustness

**Solutions:**

**Solution 1: Explicit Error Requirements**
> “Implement a file upload endpoint.
>
> Error handling requirements:
> - File too large (>10MB) → `400` with ‘File exceeds maximum size’.
> - Invalid file type → `400` with ‘Only PDF, PNG, JPG allowed’.
> - Network error during upload → `500` with ‘Upload failed, please retry’.
> - Missing file in request → `400` with ‘No file provided’.
> - S3 upload fails → `500` with ‘Storage error’ and log the error.
>
> Use try-catch blocks. Return consistent error format: `{ error: { code, message } }`.”

**Solution 2: Reference Error Patterns**
> “Follow the error handling pattern from `src/api/users.ts`:
> - Try-catch around async operations.
> - Specific error messages for different failures.
> - Proper HTTP status codes.
> - Error logging.
> - User-friendly error messages.”

**Solution 3: Add to .cursorrules**
> Add this to `.cursorrules`:
>
> ```markdown
> ## Error Handling
> - ALWAYS use try-catch for async operations.
> - ALWAYS validate input.
> - ALWAYS return user-friendly error messages.
> - ALWAYS log errors with context.
> - Use custom error classes (`ValidationError`, `NotFoundError`, etc.).
> ```

**Prevention:**
- Always mention error handling in prompts
- Create error handling template
- Reference error patterns
- Add to project conventions

---

### Missing Input Validation

**Symptom:** AI generates code that accepts any input without validation, leading to crashes or security vulnerabilities.

**Root causes:**
1. Validation not specified
2. Security not prioritized

**Solutions:**

**Solution 1: Specify Validation Rules**
> “Create a user registration endpoint.
>
> Validation requirements:
> - **Email:** required, valid format (RFC 5322), max 255 characters, unique (check database).
> - **Password:** required, minimum 8 characters, must include uppercase, lowercase, number, special character.
> - **Name:** required, 2–100 characters, letters and spaces only (no special characters).
>
> Return `400` with field-specific errors for validation failures.”

**Solution 2: Use Validation Library**
> “Use Zod for validation (already installed):
>
> ```typescript
> const registerSchema = z.object({
>   email: z.string().email().max(255),
>   password: z.string().min(8).regex(/[A-Z]/).regex(/[a-z]/).regex(/[0-9]/),
>   name: z.string().min(2).max(100).regex(/^[a-zA-Z ]+$/)
> });
> ```
>
> Validate the request body against this schema before processing.”

**Solution 3: Security-First Prompt**
> “Implement [feature] with security as the top priority.
>
> Input validation:
> - Sanitize all user input.
> - Validate types and formats.
> - Check length limits.
> - Prevent SQL injection.
> - Prevent XSS.
> - Use a whitelist approach (accept only known-good data).
>
> Fail securely: reject invalid input rather than trying to fix it.”

**Prevention:**
- Always specify validation in prompts
- Use validation libraries
- Create validation template
- Security-first mindset

---

### Poor Performance

**Symptom:** AI-generated code works but is slow (N+1 queries, inefficient algorithms, etc.)

**Root causes:**
1. Performance not mentioned
2. AI prioritizes simplicity/readability over efficiency

**Solutions:**

**Solution 1: Specify Performance Requirements**
> “Implement user search with performance requirements.
>
> Current: 5 seconds for 10,000 users.
> Target: under 500 ms for 10,000 users.
>
> Optimization requirements:
> - Use database indexes (email, name columns).
> - Pagination (20 results per page).
> - Debounce search input (500 ms).
> - Cache results (5 minutes).
> - Avoid N+1 queries.
>
> Measure and verify the performance meets the target.”

**Solution 2: Review and Optimize**
> “Review this code for performance issues:
> [paste code]
>
> Identify:
> - N+1 query problems.
> - Inefficient algorithms (O(n²) or worse).
> - Missing indexes.
> - Unnecessary computations.
> - Memory leaks.
>
> Then optimize to meet the <500 ms target.”

**Solution 3: Request Complexity Analysis**
> “Implement [algorithm] with:
> - Time complexity: `O(n log n)` or better.
> - Space complexity: `O(n)` or better.
>
> Include Big-O analysis in comments. If the complexity target can’t be met, explain why.”

**Prevention:**
- Always mention performance requirements
- Specify acceptable complexity
- Request performance analysis
- Profile before and after

---

### Insecure Code Generation

**Symptom:** AI generates code with security vulnerabilities (SQL injection, XSS, insecure authentication, etc.)

**Root causes:**
1. Security not mentioned
2. Convenience prioritized over security
3. Model trained on insecure examples

**Solutions:**

**Solution 1: Security Audit Prompt**
> “Security audit this code:
> [paste code]
>
> Check for:
> - SQL injection vulnerabilities.
> - XSS vulnerabilities.
> - CSRF vulnerabilities.
> - Insecure authentication/authorization.
> - Sensitive data exposure.
> - Insecure cryptography.
> - Injection flaws.
> - Broken access control.
>
> For each vulnerability found, provide:
> - Severity (Critical/High/Medium/Low).
> - Exploitation scenario.
> - Fix with secure code example.”

**Solution 2: Security Requirements Upfront**
> “Implement user authentication with these security requirements:
>
> **Authentication:**
> - Passwords hashed with argon2 (not bcrypt or plain).
> - Salt unique per user.
> - JWT tokens with expiration.
> - Secure random token generation.
> - HTTPS only (no HTTP).
>
> **Authorization:**
> - User can only access their own resources.
> - Admin role checked server-side.
> - No client-side auth checks.
>
> **Input validation:**
> - SQL parameterized queries (prevent injection).
> - HTML sanitization (prevent XSS).
> - CSRF tokens for state-changing operations.
>
> Follow OWASP Top 10 best practices.”

**Solution 3: Use Security Checklist**
> “After generating code, verify security:
> - [ ] No SQL injection (parameterized queries).
> - [ ] No XSS (input sanitization).
> - [ ] No CSRF (tokens for POST/PUT/DELETE).
> - [ ] Passwords hashed (argon2/bcrypt).
> - [ ] JWT secure (secret in env, expiration set).
> - [ ] Authorization checked server-side.
> - [ ] Sensitive data not logged.
> - [ ] HTTPS enforced.
>
> If any check fails, fix the code before responding.”

**Prevention:**
- Security-first prompting
- Use security templates
- Regular security audits
- Follow [OWASP guidelines](https://owasp.org/www-project-top-ten/)

---

## Workflow Bottlenecks

### Too Many Iterations

**Symptom:** Takes 5-10+ iterations to get working code.

**Root causes:**
1. Vague initial prompts
2. No examples provided
3. Missing context

**Solutions:**

**Solution 1: Study Prompt Foundations**
> Take 30 minutes to read the [Prompt Foundations Guide](../prompting/foundations.md).
>
> Learn the four-component framework:
> 1. **Clarity:** What you want (be specific).
> 2. **Context:** What the AI needs (files, patterns).
> 3. **Constraints:** Boundaries (limits, requirements).
> 4. **Criteria:** Success metrics (how to verify).
>
> Apply it to the next prompt.

**Solution 2: Use Templates**
> Don’t write prompts from scratch. Use the [Template Library](../prompting/template-library.md):
> 1. Find a template matching your task.
> 2. Fill in the `{{PLACEHOLDERS}}`.
> 3. Send it to the AI.
>
> First-try success rate: 70–90%.

**Solution 3: Add Examples**
> Every prompt should include examples:
> - Example 1: [Input] → [Expected output].
> - Example 2: [Input] → [Expected output].
> - Example 3: [Edge case] → [Expected handling].
>
> Examples eliminate ambiguity.

**Prevention:**
- Always use detailed prompts
- Include examples
- Define success criteria
- Use templates

---

### Repeating Same Instructions

**Symptom:** You find yourself explaining the same conventions, patterns, or requirements in every prompt.

**Root causes:**
1. No persistent project configuration
2. Each session starts fresh

**Solutions:**

**Solution 1: Create .cursorrules**
> Create `.cursorrules` in the project root with all conventions:
>
> ```markdown
> # Project Conventions
>
> ## Tech Stack
> - Frontend: React + TypeScript + Tailwind + Vite
> - Backend: Node.js + Express + TypeScript
> - Database: PostgreSQL + Prisma ORM
> - Testing: Jest + React Testing Library
>
> ## Code Style
> [Your style guide]
>
> ## Patterns
> [Your common patterns]
>
> ## Don’t Repeat
> - Always use argon2 for passwords (not bcrypt).
> - Always use Prisma (not raw SQL).
> - Always use functional components (not classes).
> - [Other frequent instructions]
> ```
>
> Now the AI automatically knows these without you repeating.

**Solution 2: Create docs/conventions.md**
> Create a detailed conventions directory:
>
> ```text
> docs/conventions/
> ├── code-style.md
> ├── api-design.md
> ├── database-patterns.md
> ├── testing-guidelines.md
> └── security-requirements.md
> ```
>
> Reference it in prompts: “Follow conventions in `docs/conventions/api-design.md`.”

**Solution 3: Session Setup Prompt**
> At the start of each session:
>
> “Project setup:
> - Read `.cursorrules`.
> - Read `docs/architecture/overview.md`.
> - Follow patterns from `src/api/users.ts`.
>
> Confirm you understand the project structure.”
>
> Then proceed with the specific task.

**Prevention:**
- Create .cursorrules early
- Document conventions
- Reference docs in prompts

---

### Difficulty Resuming Work

**Symptom:** When you come back to a project after days/weeks, it takes a long time to figure out where you left off.

**Root causes:**
1. No session documentation
2. No current-state tracking
3. Relying on memory

**Solutions:**

**Solution 1: Session Handoff Pattern**
> At the end of each work session:
>
> “Create a session handoff document at `docs/context/session-[date].md`:
>
> ## Completed Today
> - [What was implemented]
> - [What was fixed]
> - [What was decided]
>
> ## Current State
> - [Feature X]: 80% complete (needs task A, task B)
> - [Feature Y]: Not started
> - [Bug Z]: Fixed and tested
>
> ## Important Context
> - [Architectural decisions made]
> - [Technical challenges encountered]
> - [Workarounds implemented]
>
> ## Next Session
> 1. [First task to tackle]
> 2. [Second task]
> 3. [Third task]
>
> ## Files Modified
> - [List of files changed]
> ”

**Solution 2: Current State Document**
> Maintain `docs/context/current-state.md`.
>
> After major changes: “Update `docs/context/current-state.md` with:
> - Recently completed features.
> - In-progress features.
> - Known issues.
> - Next priorities.”

**Solution 3: Git Commit History**
> Write detailed commit messages, e.g.:
>
> ```text
> feat(auth): implement JWT token refresh
>
> - Added refresh token to user model
> - Created /auth/refresh endpoint
> - Tokens expire after 24h, refresh extends
> - Tests added for token refresh flow
>
> Related to feature spec: docs/plans/auth-feature.md
> Next: Implement logout (invalidate tokens)
> ```

**Prevention:**
- End-of-session handoffs
- Maintain current-state.md
- Detailed commit messages
- Use TodoWrite/Task Manager MCP

---

### High AI Costs

**Symptom:** Monthly AI bills are surprisingly high.

**Root causes:**
1. Inefficient prompting (repeating context)
2. Using expensive models for simple tasks
3. Not optimizing context

**Solutions:**

**Solution 1: Track Usage**
> Monitor:
> - Tokens per feature (prompt + response).
> - Model used for each task.
> - Context size per session.
>
> Baseline: “Feature X took 50k tokens with Claude Sonnet = $1.50.”
> Target: “Feature X should take 10k tokens = $0.30.”

**Solution 2: Use Right Model for Task**
> Task complexity vs. model cost:
>
> **Simple (boilerplate, templates):**
> → GLM (super cheap, 5h coding time limit).
> → Qwen Coder (cheap).
> → Gemini Flash (cheap).
>
> **Standard (most features):**
> → Claude Sonnet (balanced).
> → GLM (great price/performance).
>
> **Complex (architecture, debugging):**
> → Claude Sonnet (reliable).
> → Claude Opus (only when necessary).
>
> Cost difference: 10–50× between models.

**Solution 3: Optimize Prompts**
> Apply token optimization:
>
> **Before (50k tokens):**
> “[Paste entire architecture doc]
> [Paste 10 code files]
> [Detailed explanation]
> Now implement feature X.”
>
> **After (5k tokens):**
> “Reference `docs/architecture/overview.md` (read earlier).
> Implement feature X following the pattern in `src/api/users.ts`.
> Requirements: [concise list].”
>
> 90% token reduction!

**Prevention:**
- Use [Prompt Optimization](../prompting/advanced-techniques.md#prompt-optimization)
- Choose appropriate models
- Externalize context to .md files
- Use templates

---

## Tool-Specific Problems

### Claude Code: File Search Issues

**Symptom:** Claude Code CLI can't find files you know exist.

**Solutions:**

- Use the **Glob** tool (not bash `find`): “Find files matching `src/components/*.tsx`.”
- Be specific with patterns: “Find files matching `src/api/**/*.ts`.”
- Check the current directory: “What is the current working directory? List files in this directory.”

---

### Claude Code: Agent Issues

**Symptom:** Task/Explore agents fail or return poor results.

**Solutions:**

- Choose the right agent:
  - Explore agent: “Quick search for authentication files.”
  - Plan agent: “Plan multi-step feature implementation.”
  - General: “Complex research requiring multiple tools.”
- Specify thoroughness: “Use Explore agent with ‘very thorough’ mode to find all test files.”
- Break down tasks if too complex:
  - Instead of: “Agent: research entire codebase.”
  - Do: “Agent: find authentication-related files in `src/`.”
  - Then: “Agent: analyze authentication flow in [found files].”

---

### Cursor: Composer Failures

**Symptom:** Cursor Composer times out or produces poor results.

**Solutions:**

- Reduce file count in Composer:
  - Include a maximum of 5–10 files.
  - Use `@codebase` sparingly (very expensive).
  - Reference specific files with `@file`.
- Clear context: press `Cmd+K` → Clear context → start fresh.
- Use Chat instead for complex tasks:
  - Composer: quick edits, small changes.
  - Chat: research, planning, complex features.

---

### Droid CLI: Plan Mode Problems

**Symptom:** Droid's plan mode gets stuck or generates poor plans.

**Solutions:**
 
- Be specific with planning requests: `droid plan "Implement JWT authentication with refresh tokens, including user registration, login, token refresh endpoints"`.
- Break large plans into phases:
  - `droid plan "Phase 1: User registration and login"`.
  - After completing Phase 1, run `droid plan "Phase 2: JWT refresh token mechanism"`.
- Review and edit the generated plan before executing:
  - Plans are stored in the `.tasks/` directory.
  - Edit them manually if needed.

---

### MCP DevTools: Connection Issues

**Symptom:** DevTools MCP can't connect to browser.

**Solutions:**

1. Check that Chrome or Edge is running.
2. Ensure the DevTools protocol is enabled (`--remote-debugging-port=9222`).
3. Restart the MCP server.
4. Verify MCP configuration in settings.
5. Confirm no firewall is blocking `localhost:9222`.

---

## Common Error Patterns

### Pattern 1: "Cannot read property 'X' of undefined"

**What it means:** Accessing property on null/undefined object.

**Common causes:**
- API returned null but not checked
- Array/object destructuring on undefined
- Async timing issue (accessing before loaded)

**AI prompting fix:**
> “Fix null pointer error:
> [paste error + code]
>
> Add null checks:
> - Check if the object exists before accessing.
> - Use optional chaining (`?.`).
> - Provide default values.
> - Handle loading/error states.”

---

### Pattern 2: "Module not found"

**What it means:** Import can't find the file/package.

**Common causes:**
- Typo in import path
- File doesn't exist
- Package not installed
- Incorrect relative path

**AI prompting fix:**
> “Fix module not found error:
> Error: Cannot find module './components/UserCard'
>
> Context:
> - File structure: [describe].
> - Trying to import from: [file].
> - Target file location: [path].
>
> Verify the file exists and fix the import path.”

---

### Pattern 3: "Maximum call stack size exceeded"

**What it means:** Infinite recursion.

**Common causes:**
- Recursive function with no base case
- Circular dependency
- useEffect with missing dependency array

**AI prompting fix:**
> “Fix infinite recursion:
> [paste error + code]
>
> Find and fix:
> - Missing base case in recursion.
> - Circular dependencies.
> - `useEffect` causing an infinite loop.”

---

## Debugging Checklist

When stuck, go through this systematically:

### Basic Checks
- [ ] Read the error message completely
- [ ] Check the stack trace for file:line
- [ ] Look at the code at that line
- [ ] Verify file exists and is where expected
- [ ] Check for typos in variable/function names

### Context Gathering
- [ ] Reproduce the error reliably
- [ ] Note what triggers it (specific action/input)
- [ ] Check browser console (F12)
- [ ] Check server logs
- [ ] Check network tab for failed requests
- [ ] Check database logs if applicable

### Isolation
- [ ] Create minimal reproduction
- [ ] Remove unrelated code
- [ ] Test with simple input
- [ ] Check if works in isolation

### AI Assistance
- [ ] Prepare complete error info
- [ ] Gather relevant code
- [ ] Note what you've tried
- [ ] Use [Debug Template](../prompting/template-library.md#template-4-runtime-error-debugging)

---

## When to Ask for Help

### Time-Based Triggers

**Ask for help if:**
- Stuck on same issue for >2 hours
- Tried 5+ different solutions, none worked
- Error makes no sense despite research

### Complexity Triggers

**Ask for help if:**
- Bug only in production, not reproducible locally
- Involves complex system interactions
- Related to infrastructure/deployment (outside codebase)
- Performance issue despite profiling

### Knowledge Triggers

**Ask for help if:**
- Completely new technology/framework
- Security-critical implementation
- Database migration/architecture decision
- Legal/compliance concerns

### Where to Ask

1. **Project Documentation**
   - Check `docs/` for answers.
   - Search commit history.
   - Review architecture decisions.
2. **AI Assistance**
   - Use comprehensive debug prompts.
   - Provide all context.
   - Try different models.
3. **Search Online**
   - Google the error message.
   - Check Stack Overflow.
   - Review GitHub issues for libraries.
   - Read official documentation.
4. **Community Help**
   - Project Discord/Slack.
   - Stack Overflow (with MCVE).
   - Reddit communities.
   - Framework-specific forums.
5. **Professional Help**
   - Hire an expert for consultation.
   - Use a code review service.
   - Ask a mentor/senior developer.

---

## Summary

### Quick Decision Trees

**"My code doesn't work"**
1. Do I have the error message? → Use Debug Template
2. Is the prompt vague? → Use detailed template
3. Is context too full? → Externalize to .md
4. Am I using right model? → Check task complexity

**"It's taking too long"**
1. Too many iterations? → Improve prompts
2. Context management issues? → Use .md files
3. Wrong workflow? → Use multi-step approach
4. High costs? → Optimize tokens, use cheaper models

**"AI behaves weirdly"**
1. Forgets things? → Check context usage
2. Ignores constraints? → Emphasize constraints
3. Over-engineers? → Add simplicity requirements
4. Hallucinates? → Reference real code

---

**Related Documentation:**
- [Prompting Guide](../prompting/README.md) → Improve prompt quality
- [Context Management](../context-management/README.md) → Manage AI context
- [Development Workflow](../workflow/README.md) → Integrated workflow
- [Development Tools](../development-tools/README.md) → Tool setup and usage

**Back to:** [Main Guide](../../README.md)
