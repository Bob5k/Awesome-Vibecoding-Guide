# Advanced Prompting Techniques 🚀

**Expert-level strategies for complex development scenarios**

---

## Table of Contents

1. [Multi-Step Workflows](#multi-step-workflows)
2. [Prompt Chaining](#prompt-chaining)
3. [Error Recovery Prompting](#error-recovery-prompting)
4. [Context-Aware Prompting](#context-aware-prompting)
5. [Prompt Optimization](#prompt-optimization)
6. [Meta-Prompting](#meta-prompting)
7. [Parallel Prompting](#parallel-prompting)
8. [Self-Correcting Prompts](#self-correcting-prompts)

---

## Multi-Step Workflows

### Overview

**When to use:** Complex features that are too large for single-shot prompting.

**Core principle:** Break into phases, build incrementally, verify at each step.

---

### Strategy 1: Linear Multi-Step

**Pattern:** Each step depends on the previous one.

```
Step 1 → Verify → Step 2 → Verify → Step 3 → Verify → Complete
```

**Example: Building Authentication System**

**Step 1: Database Schema**
```
"Create database schema for authentication system.

FILE: src/models/User.ts

Requirements:
- id: UUID primary key
- email: string, unique, indexed
- password: string (will store bcrypt hash)
- name: string
- role: enum ('user', 'admin')
- emailVerified: boolean, default false
- createdAt: timestamp
- updatedAt: timestamp

Also create migration file in src/database/migrations/

Success criteria:
- TypeScript types defined
- Database migration creates table
- Indexes on email for performance"
```

↓ *Verify: Run migration, check schema*

**Step 2: User Repository**
```
"Create UserRepository for database operations.

FILE: src/repositories/UserRepository.ts

Use the User model from Step 1 (src/models/User.ts).

Methods:
- findById(id: string): Promise<User | null>
- findByEmail(email: string): Promise<User | null>
- create(data: CreateUserDTO): Promise<User>
- update(id: string, data: UpdateUserDTO): Promise<User>
- updatePassword(id: string, hashedPassword: string): Promise<void>
- markEmailVerified(id: string): Promise<void>

Follow repository pattern from src/repositories/PostRepository.ts.

Include error handling for:
- Not found
- Unique constraint violations
- Database connection errors"
```

↓ *Verify: Write unit tests, test each method*

**Step 3: Authentication Service**
```
"Create authentication service with business logic.

FILE: src/services/AuthService.ts

Use UserRepository from Step 2.

Methods:
- register(email, password, name): Creates user, hashes password, sends verification email
- login(email, password): Verifies credentials, returns JWT token
- verifyEmail(token): Marks email as verified
- requestPasswordReset(email): Generates reset token, sends email
- resetPassword(token, newPassword): Validates token, updates password

Security requirements:
- Hash passwords with bcrypt (10 rounds)
- Generate secure random tokens (32 bytes)
- Tokens expire after 1 hour
- JWT tokens expire after 24 hours

Use our existing EmailService (src/services/EmailService.ts) for sending emails.

Error handling:
- Invalid credentials → return clear error (don't reveal which field)
- User already exists → return ConflictError
- Invalid token → return UnauthorizedError"
```

↓ *Verify: Unit tests, mock dependencies*

**Step 4: API Routes**
```
"Create authentication API routes.

FILE: src/api/auth.ts

Use AuthService from Step 3.

Routes:
- POST /api/auth/register
- POST /api/auth/login
- POST /api/auth/verify-email
- POST /api/auth/request-reset
- POST /api/auth/reset-password

Each route:
- Validates input (express-validator)
- Calls appropriate AuthService method
- Returns appropriate HTTP status code
- Handles errors with consistent format

Follow the pattern from src/api/posts.ts (our existing routes).

Rate limiting:
- Login: 5 attempts per 15 minutes per IP
- Register: 3 attempts per hour per IP
- Password reset: 3 attempts per hour per email

Use our existing rateLimitMiddleware (src/middleware/rateLimit.ts)."
```

↓ *Verify: Integration tests, test all endpoints*

**Step 5: Frontend Integration**
```
"Create authentication UI components.

FILES:
- src/components/auth/LoginForm.tsx
- src/components/auth/RegisterForm.tsx
- src/components/auth/PasswordResetForm.tsx

Connect to API routes from Step 4.

Use React Hook Form for form handling.
Use our existing FormError component for error display.

State management:
- Store JWT in localStorage
- Store user data in Zustand store (src/stores/authStore.ts - create this)
- Handle token expiration (redirect to login)

Follow form patterns from src/components/forms/PostForm.tsx."
```

↓ *Verify: Manual testing, E2E tests*

**Why this works:**
- ✅ Each step has clear scope
- ✅ Verification points prevent errors from compounding
- ✅ Can pause/resume between steps
- ✅ Debugging is easier (know where failure occurred)
- ✅ Can parallelize some steps (frontend + backend)

---

### Strategy 2: Branching Multi-Step

**Pattern:** Multiple parallel paths that converge.

```
           ┌─ Step 2a ─┐
Step 1 ────┼─ Step 2b ─┼──── Step 3 (merge)
           └─ Step 2c ─┘
```

**Example: Building Dashboard with Multiple Widgets**

**Step 1: Dashboard Shell**
```
"Create dashboard layout shell.

FILE: src/pages/Dashboard.tsx

Layout:
- Header (user info, logout)
- Sidebar (navigation)
- Main content area (4 widget slots in 2x2 grid)
- Footer

No widgets yet, just placeholders:
<WidgetPlaceholder name='Analytics' />
<WidgetPlaceholder name='Recent Activity' />
<WidgetPlaceholder name='User Stats' />
<WidgetPlaceholder name='Quick Actions' />

Use Tailwind grid for responsive layout.
Follow our app layout pattern (src/layouts/AppLayout.tsx)."
```

↓ *Verify: Layout renders correctly*

**Then parallelize:**

**Step 2a: Analytics Widget**
```
"Create Analytics widget for dashboard.

FILE: src/components/widgets/AnalyticsWidget.tsx

Shows:
- Total views (last 30 days)
- Total users
- Revenue trend (line chart)

Data from: GET /api/analytics/summary
Chart library: Chart.js (already installed)

Widget frame: Use WidgetContainer from src/components/widgets/WidgetContainer.tsx
Loading state: Use our Skeleton component"
```

**Step 2b: Recent Activity Widget (parallel)**
```
"Create Recent Activity widget for dashboard.

FILE: src/components/widgets/RecentActivityWidget.tsx

Shows:
- Last 10 user activities
- Activity type icon + description + timestamp
- 'View all' link to activity page

Data from: GET /api/activities/recent
Real-time updates: Use WebSocket connection (ws://localhost:8080/activities)

Widget frame: Use WidgetContainer from src/components/widgets/WidgetContainer.tsx
Loading state: Use our Skeleton component"
```

**Step 2c: User Stats Widget (parallel)**
```
"Create User Stats widget for dashboard.

FILE: src/components/widgets/UserStatsWidget.tsx

Shows:
- Active users (today)
- New signups (this week)
- Churn rate
- User satisfaction score

Data from: GET /api/users/stats
Refresh: Every 5 minutes (useInterval hook)

Widget frame: Use WidgetContainer from src/components/widgets/WidgetContainer.tsx
Loading state: Use our Skeleton component"
```

↓ *All three can be developed simultaneously*

**Step 3: Integration**
```
"Integrate all widgets into Dashboard.

Update src/pages/Dashboard.tsx:
- Replace placeholders with actual widgets
- Add loading states (show skeleton while widgets load)
- Add error boundaries (if one widget fails, others still work)
- Add refresh button (refreshes all widgets)

Use Promise.all to fetch all widget data in parallel (faster loading).

Error handling:
- Widget fails to load → show error message in widget frame, don't crash dashboard
- Network error → show retry button
- No data → show empty state

Follow dashboard pattern from our admin panel (src/pages/admin/Dashboard.tsx)."
```

**Why this works:**
- ✅ Parallel development (widgets can be built simultaneously)
- ✅ Isolated failures (one widget error doesn't break others)
- ✅ Each widget is independently testable
- ✅ Easy to add/remove widgets
- ✅ Clear integration point at the end

---

## Prompt Chaining

### Overview

**Concept:** Output of one prompt becomes input to the next.

**Use cases:**
- Complex workflows requiring multiple specialized tasks
- Progressive refinement
- Pipeline processing

---

### Pattern 1: Sequential Refinement Chain

**Use when:** Need to progressively improve or transform output.

**Example: Code Generation → Optimization → Documentation Chain**

**Prompt 1: Generate Initial Code**
```
"Generate a function to calculate factorial.

Language: TypeScript
Handle: negative numbers (return error), zero (return 1), large numbers (use BigInt)
Include: input validation

Return just the code, no explanation."
```

↓ *AI generates code*

**Prompt 2: Optimize (chained)**
```
"Optimize this factorial function for performance:

[paste code from Prompt 1]

Optimizations to apply:
- Memoization for repeated calculations
- Iterative instead of recursive (avoid stack overflow)
- Early return for 0 and 1

Return optimized code only."
```

↓ *AI optimizes*

**Prompt 3: Add Tests (chained)**
```
"Write comprehensive tests for this factorial function:

[paste optimized code from Prompt 2]

Test framework: Jest

Cover:
- Happy path (0, 1, 5, 10)
- Edge cases (negative, large numbers)
- Performance (verify memoization works)

Return complete test file."
```

↓ *AI writes tests*

**Prompt 4: Generate Documentation (chained)**
```
"Generate JSDoc documentation for this factorial function:

[paste final code from Prompt 2]

Include:
- Description
- @param documentation
- @returns documentation
- @throws documentation
- @example with 3 usage examples
- @complexity notation (time and space)

Return code with inline documentation."
```

**Final result:** Optimized, tested, documented function.

**Why chaining works here:**
- Each step has a single focus
- Quality improves at each stage
- Can verify/adjust at each step
- Pipeline is reusable

---

### Pattern 2: Data Transformation Chain

**Use when:** Processing data through multiple transformations.

**Example: API Response → Transform → Filter → Format → Display**

**Prompt 1: Transform Raw API Data**
```
"Transform raw API response to normalized format:

Raw data:
[paste API response]

Transform to:
{
  id: string,
  name: string,
  email: string,
  role: 'user' | 'admin',
  active: boolean,
  lastLogin: Date
}

Return TypeScript code for transformation function."
```

**Prompt 2: Filter Data (chained)**
```
"Add filtering to this transformation function:

[paste code from Prompt 1]

Filters to add:
- Only active users
- Last login within 30 days
- Role is 'user' (exclude admins)

Return updated function with filters applied."
```

**Prompt 3: Sort and Paginate (chained)**
```
"Add sorting and pagination to this function:

[paste code from Prompt 2]

Sorting:
- Sort by lastLogin (most recent first)

Pagination:
- Page size: 20
- Accept page number parameter
- Return { data: User[], totalPages: number, currentPage: number }

Return final function."
```

**Result:** Complete data processing pipeline.

---

## Error Recovery Prompting

### Overview

**When AI generates wrong code, how to correct effectively.**

**Anti-pattern:**
```
"That's wrong, try again"
[AI makes different mistakes]
```

**Better pattern:** Explicit correction with explanation.

---

### Strategy 1: Identify and Correct

**Pattern:**

```
"The code you generated has [SPECIFIC ISSUE].

Specifically:
- [What's wrong]
- [Why it's wrong]
- [Expected behavior]

Please fix by:
1. [Step 1]
2. [Step 2]

Keep everything else the same."
```

**Example:**

**AI generates code with bug:**
```typescript
function calculateTotal(items) {
  let total = 0;
  items.forEach(item => {
    total += item.price; // BUG: Doesn't consider quantity
  });
  return total;
}
```

**Bad correction:**
```
"This is wrong, fix it"
```

**Good correction:**
```
"The calculateTotal function has a bug.

Issue:
Line 4: total += item.price doesn't multiply by item.quantity

This means:
- 2 items at $10 each → calculates $10 instead of $20

Fix:
Change line 4 to: total += item.price * item.quantity

Keep everything else the same (function signature, loop structure, return)."
```

**Result:** Precise fix, no other changes.

---

### Strategy 2: Provide Correct Example

**Pattern:**

```
"The output doesn't match requirements.

Expected output:
[exact example]

Actual output:
[what AI generated]

Difference:
[what's different]

Please update to match expected output exactly."
```

**Example:**

**Requirement:** Format currency as "$1,234.56"

**AI generates:**
```typescript
function formatCurrency(amount) {
  return `$${amount.toFixed(2)}`; // Outputs: $1234.56 (no comma)
}
```

**Correction:**
```
"The formatCurrency function doesn't add thousand separators.

Expected output: $1,234.56
Actual output: $1234.56

Missing: Comma thousand separator

Update to use Intl.NumberFormat:
const formatter = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD'
});

This will format 1234.56 → $1,234.56 correctly."
```

---

### Strategy 3: Reference Correct Pattern

**Pattern:**

```
"The implementation doesn't follow our project pattern.

Current implementation:
[what AI generated]

Should follow pattern from:
[reference file:function]

Specifically:
- [pattern element 1]
- [pattern element 2]

Please update to match our pattern."
```

**Example:**

**AI generates custom validation:**
```typescript
function validateEmail(email) {
  const regex = /^[^@]+@[^@]+\.[^@]+$/;
  if (!regex.test(email)) {
    throw new Error('Invalid email');
  }
}
```

**Correction:**
```
"The validateEmail function doesn't follow our error handling pattern.

Current implementation:
- Throws generic Error
- Uses simple regex

Our pattern (from src/utils/validation.ts):
- Throws ValidationError (custom class)
- Uses our standardized email regex
- Returns validation result object

Example from src/utils/validation.ts:

```typescript
function validateEmail(email): ValidationResult {
  const isValid = EMAIL_REGEX.test(email);
  return {
    isValid,
    error: isValid ? null : 'Please enter a valid email address'
  };
}
```

Please update your implementation to match this pattern."
```

**Result:** AI generates code consistent with project.

---

## Context-Aware Prompting

### Overview

**Leverage project-specific context for better results.**

---

### Strategy 1: Reference Architecture Docs

**Pattern:**

```
"Before implementing, read docs/architecture/[topic].md

Confirm you understand:
- [key principle 1]
- [key principle 2]

Then implement following that architecture."
```

**Example:**

```
"Before implementing the new API endpoint, read docs/architecture/api-design.md

Confirm you understand:
- Our REST conventions (resource naming, HTTP methods)
- Error response format
- Pagination pattern
- Authentication requirements

Then implement POST /api/articles following that architecture.

Requirements: [...]"
```

**Why this works:**
- AI loads architecture first
- Confirms understanding before coding
- Implementation follows established patterns

---

### Strategy 2: Use .cursorrules Effectively

**Create project-specific instructions:**

**.cursorrules:**
```
# Project conventions

## Code Style
- Use functional components (no class components)
- Use TypeScript strict mode
- Use arrow functions
- Async/await (no .then())

## Error Handling
- Always use our custom error classes (ValidationError, NotFoundError, etc.)
- Never throw generic Error
- Always include error codes

## Testing
- Every feature must have tests
- Use Jest + React Testing Library
- Test file naming: ComponentName.test.tsx
- Coverage target: 80%

## API Design
- REST conventions: GET /resource, POST /resource, PUT /resource/:id, DELETE /resource/:id
- Always return JSON
- Use our standard response format:
  Success: { data: {...} }
  Error: { error: { code: string, message: string } }

## Database
- Use Prisma ORM
- All queries in repository layer (not in routes or services)
- Always use transactions for multi-step operations

## Components
- One component per file
- Props interface always defined
- Use our component template: docs/templates/component.tsx
```

**Prompts can now be shorter:**

**Without .cursorrules:**
```
"Create a Button component. Use TypeScript, functional component, arrow function,
props interface, one component per file, use Tailwind for styling, include
variants (primary, secondary, danger), include size (sm, md, lg), include
disabled state, include loading state, follow our naming conventions..."
```

**With .cursorrules:**
```
"Create a Button component with variants (primary, secondary, danger)
and sizes (sm, md, lg). Include disabled and loading states."
```

AI automatically follows the conventions in .cursorrules.

---

### Strategy 3: Project Memory Pattern

**Maintain a project knowledge base:**

**docs/context/project-knowledge.md:**
```markdown
# Project Knowledge Base

## Decisions Made
- 2024-01-15: Switched from bcrypt to argon2 for better security
- 2024-01-10: Using PostgreSQL instead of MongoDB (better for relational data)
- 2024-01-05: Cloudflare Pages for hosting (free, fast, edge computing)

## Tech Stack
- Frontend: React + TypeScript + Tailwind + Vite
- Backend: Node.js + Express + TypeScript
- Database: PostgreSQL + Prisma ORM
- Hosting: Cloudflare Pages + Workers
- Authentication: JWT tokens
- Email: SendGrid
- File storage: Cloudflare R2

## Conventions
- File naming: kebab-case (user-profile.tsx)
- Component naming: PascalCase (UserProfile)
- Function naming: camelCase (getUserById)
- CSS: Tailwind utility classes only (no custom CSS unless absolutely necessary)

## Common Patterns
- Authentication: JWT middleware in src/middleware/auth.ts
- Validation: express-validator in routes, detailed validation in services
- Error handling: Custom error classes, centralized error handler
- Database: Repository pattern, Prisma for all queries
- Forms: React Hook Form + Zod validation

## Known Issues
- Email sending is slow in development (use mailtrap)
- Database migrations must be run manually (not automatic)
- File uploads limited to 10MB (Cloudflare R2 restriction)
```

**Prompts can reference this:**

```
"Read docs/context/project-knowledge.md for our tech stack and conventions.

Then implement user registration following our established patterns."
```

AI gets complete project context from one file.

---

## Prompt Optimization

### Overview

**Reduce token usage while maintaining quality.**

---

### Strategy 1: Template + Variables

**Instead of:**
```
"Create a user registration form with email, password, name fields.
Validate email format, password min 8 characters, name required.
Show errors below fields. Submit to POST /api/users. Show success message.
Use React Hook Form. Use our FormError component."

[Send this full prompt every time for similar forms]
```

**Better:**

**Create template (docs/templates/prompt-form.md):**
```markdown
# Form Creation Template

Create a {{FORM_NAME}} form with {{FIELDS}} fields.

Validation:
{{VALIDATION_RULES}}

Submit to: {{API_ENDPOINT}}
Success message: {{SUCCESS_MESSAGE}}

Use React Hook Form.
Use our FormError component (src/components/common/FormError.tsx).
Follow form pattern from src/components/forms/{{REFERENCE_FORM}}.tsx.
```

**Prompt becomes:**
```
"Use template docs/templates/prompt-form.md:

FORM_NAME: User Registration
FIELDS: email, password, name
VALIDATION_RULES: email format, password min 8 chars, name required
API_ENDPOINT: POST /api/users
SUCCESS_MESSAGE: Account created! Check email to verify.
REFERENCE_FORM: LoginForm"
```

**Benefits:**
- Shorter prompts
- Consistent results
- Reusable pattern
- Token savings

---

### Strategy 2: Reference Instead of Repeating

**Instead of:**
```
[Paste entire architecture document every time]

"Now implement feature X following this architecture..."
```

**Better:**
```
"Reference docs/architecture/api-design.md (you read it earlier this session).

Implement feature X following that architecture."
```

If within same session, AI has architecture in context. No need to repeat.

---

### Strategy 3: Progressive Disclosure

**Don't dump all information at once. Provide as needed.**

**Instead of:**
```
"Here's my entire user model, database schema, validation rules, business
logic constraints, UI requirements, API documentation, testing strategy,
deployment configuration, and error handling patterns. Now add a field."
```

**Better:**

**Prompt 1:**
```
"Add 'phoneNumber' field to User model (src/models/User.ts).
Type: string, optional, format: E.164 international format."
```

**Prompt 2 (if needed):**
```
"Add validation for phoneNumber field (src/services/UserService.ts).
Use libphonenumber-js for validation."
```

**Prompt 3 (if needed):**
```
"Add phoneNumber input to registration form (src/components/RegisterForm.tsx).
Use react-phone-number-input component."
```

Load context progressively as needed.

---

## Meta-Prompting

### Overview

**Get AI to help write better prompts.**

---

### Pattern: Prompt Improvement

**Ask AI to improve your prompt before using it:**

```
"I want to ask an AI to implement a feature. Here's my draft prompt:

[your prompt]

Please improve this prompt to be:
- More specific
- Include necessary context
- Define success criteria clearly
- Follow best practices for AI prompting

Return the improved prompt."
```

**Example:**

**Draft prompt:**
```
"Create a form for users to submit feedback"
```

**Meta-prompt:**
```
"Improve this prompt for an AI coding assistant:

'Create a form for users to submit feedback'

Make it more specific and include necessary context."
```

**AI improves it to:**
```
"Create a user feedback form component.

FILE: src/components/FeedbackForm.tsx

Fields:
- Category: dropdown (Bug Report, Feature Request, General Feedback)
- Subject: text input (required, max 100 chars)
- Message: textarea (required, max 500 chars)
- Email: text input (optional, for follow-up)

Validation:
- Category required
- Subject required, max length
- Message required, max length
- Email format validation if provided

Submit to: POST /api/feedback
Success: Show toast 'Thank you for your feedback!', clear form
Error: Show error message below form

Use React Hook Form for form handling.
Use our Toast component (src/components/Toast.tsx).
Follow form pattern from ContactForm (src/components/ContactForm.tsx)."
```

Much better!

---

## Parallel Prompting

### Overview

**Execute multiple independent prompts simultaneously.**

**Use when:** Multiple tasks that don't depend on each other.

---

### Strategy: Parallel Development

**Example: Building User Profile Page**

**Sequential (slow):**
```
1. Create user data fetching hook → wait
2. Create profile header component → wait
3. Create profile stats component → wait
4. Create profile activity component → wait
5. Assemble page → wait

Total: 5 sequential waits
```

**Parallel (fast):**

**Session 1 (Backend):**
```
"Create user profile API endpoint.

GET /api/users/:id/profile

Returns:
- User basic info
- Stats (posts count, followers, following)
- Recent activity

[detailed requirements]"
```

**Session 2 (Data Hook - depends on Session 1 completion):**
```
"Create useUserProfile hook for fetching profile data.

Uses GET /api/users/:id/profile
Returns { profile, loading, error }

[detailed requirements]"
```

**Session 3 (Component 1 - can run parallel with 2):**
```
"Create ProfileHeader component.

Mock data for now (API will come later).

Displays: avatar, name, bio, edit button

[detailed requirements]"
```

**Session 4 (Component 2 - parallel with 2, 3):**
```
"Create ProfileStats component.

Mock data for now.

Displays: posts count, followers, following

[detailed requirements]"
```

**Session 5 (Component 3 - parallel with 2, 3, 4):**
```
"Create ProfileActivity component.

Mock data for now.

Displays: recent posts, comments

[detailed requirements]"
```

**Session 6 (Integration - after all complete):**
```
"Integrate all profile components into UserProfile page.

Use useUserProfile hook from Session 2.
Layout: ProfileHeader + ProfileStats + ProfileActivity

Replace mocks with real data."
```

**Result:** 3-4 parallel sessions instead of 6 sequential = faster development.

---

## Self-Correcting Prompts

### Overview

**Build verification into prompts so AI checks its own work.**

---

### Pattern: Built-in Verification

**Template:**

```
[Task description]

After implementation, verify:
- [check 1]
- [check 2]
- [check 3]

If any check fails, fix it before responding.

Return: code + verification results.
```

**Example:**

```
"Create a function to merge two sorted arrays into one sorted array.

Language: TypeScript
Time complexity: O(n + m)
Space complexity: O(n + m)

After implementation, verify:
1. Function handles empty arrays ([], [1,2] → [1,2])
2. Function handles one empty array ([1,2], [] → [1,2])
3. Function handles identical elements ([1,1], [1,1] → [1,1,1,1])
4. Function maintains sort order (verify with test case)
5. Time complexity is O(n + m) (no nested loops)
6. Space complexity is O(n + m) (one result array)

If any verification fails, fix the implementation.

Return:
1. The function
2. Verification results (all checks passed)
3. Test cases demonstrating correctness"
```

**AI response includes:**
```typescript
function mergeSorted Arrays(arr1: number[], arr2: number[]): number[] {
  // Implementation
  [...]
}

// Verification Results:
✓ Empty array handling: PASS
✓ One empty array: PASS
✓ Identical elements: PASS
✓ Sort order maintained: PASS
✓ Time complexity O(n+m): PASS (single pass through both arrays)
✓ Space complexity O(n+m): PASS (one result array of size n+m)

// Test cases:
[test cases demonstrating all checks]
```

**Benefits:**
- AI self-checks before responding
- Reduces back-and-forth iterations
- Higher quality first output

---

## Summary

### When to Use Each Technique

| Technique | Use Case | Benefit |
|-----------|----------|---------|
| **Multi-Step Workflows** | Complex features | Manageable scope, verification points |
| **Prompt Chaining** | Progressive refinement | Output improves at each stage |
| **Error Recovery** | AI generates wrong code | Precise corrections, avoid frustration |
| **Context-Aware** | Project-specific work | Consistent with conventions |
| **Optimization** | High token usage | Cost savings, faster prompts |
| **Meta-Prompting** | Unsure how to prompt | AI helps write better prompts |
| **Parallel Prompting** | Independent tasks | Faster development |
| **Self-Correcting** | Need high quality | Built-in verification |

---

### Advanced Prompt Patterns Reference

```
┌─────────────────────────────────────────────┐
│  Advanced Prompt Pattern Selection          │
├─────────────────────────────────────────────┤
│  Simple feature       → Single prompt       │
│  Complex feature      → Multi-step workflow │
│  Multiple components  → Branching workflow  │
│  Pipeline processing  → Prompt chaining     │
│  AI made mistake      → Error recovery      │
│  Project-specific     → Context-aware       │
│  High token cost      → Optimization        │
│  Unclear requirements → Meta-prompting      │
│  Speed critical       → Parallel prompting  │
│  Quality critical     → Self-correcting     │
└─────────────────────────────────────────────┘
```

---

**Next Steps:**
- [Template Library](./template-library.md) → Ready-to-use prompt templates
- [Task-Specific Patterns](./task-specific-patterns.md) → Specialized prompting
- [Foundations](./foundations.md) → Core principles review

**Back to:** [Prompting Guide Home](./README.md)
