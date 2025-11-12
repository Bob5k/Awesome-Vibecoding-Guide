# Task-Specific Prompting Patterns 🎨

**Master specialized prompting strategies for different development scenarios**

---

## Table of Contents

1. [Feature Implementation](#feature-implementation)
2. [Debugging & Error Resolution](#debugging--error-resolution)
3. [Refactoring](#refactoring)
4. [Code Review](#code-review)
5. [Documentation](#documentation)
6. [Testing](#testing)
7. [Performance Optimization](#performance-optimization)
8. [Security Hardening](#security-hardening)

---

## Feature Implementation

### Overview

**Goal:** Get AI to build new functionality that integrates seamlessly with existing code.

**Key challenges:**
- Understanding existing patterns
- Maintaining consistency
- Handling integration points
- Anticipating edge cases

**Success pattern:**

```
Clear requirements + Architecture context + Pattern references + Examples
= High-quality implementation on first try
```

---

### Pattern 1: Simple Feature Addition

**Use when:** Adding standalone feature to existing module

**Template:**

```
Implement [FEATURE_NAME] in [FILE_PATH].

Requirements:
- [requirement 1]
- [requirement 2]
- [requirement 3]

Follow the pattern used in [REFERENCE_FEATURE] in [REFERENCE_FILE].

Success criteria:
- [criterion 1]
- [criterion 2]
```

**Real Example 1: Add Email Validation**

**Bad prompt:**
```
"Add email validation"
```

**Good prompt:**
```
"Add email validation to the user registration form in src/components/RegisterForm.tsx.

Requirements:
- Validate on blur (not on every keystroke)
- Show error message below input field
- Check format: standard email regex
- Required field (empty = error)

Follow the pattern used for password validation in the same file (lines 45-67).

Success criteria:
- Invalid email → red border + error message 'Please enter a valid email'
- Valid email → green border, no error message
- Empty field on blur → error message 'Email is required'
- Submit disabled if email invalid

Use our existing FormError component from src/components/common/FormError.tsx."
```

**Why the good prompt works:**
- ✅ Specific file and location
- ✅ Clear validation rules
- ✅ UX behavior defined
- ✅ References existing pattern
- ✅ Uses existing component
- ✅ Measurable success criteria

**Outcome:** AI generates validation that matches existing code style, handles all cases, integrates with FormError component.

---

**Real Example 2: Add Sorting Feature**

**Bad prompt:**
```
"Add sorting to the table"
```

**Good prompt:**
```
"Add sorting functionality to the UserTable component in src/components/tables/UserTable.tsx.

Requirements:
- Sort by: name (alphabetical), email (alphabetical), created date (chronological)
- Click column header to sort
- Default sort: name ascending
- Second click: reverse sort order
- Third click: remove sort (back to default)

Visual indicators:
- Unsorted: no icon
- Sorted ascending: ↑ icon next to header
- Sorted descending: ↓ icon next to header

State management:
- Use existing Zustand store pattern (see src/stores/tableStore.ts)
- Persist sort state in URL query params (?sort=name&order=asc)

Follow the pattern from PostTable in src/components/tables/PostTable.tsx (lines 89-145).

Success criteria:
- Click header → data reorders correctly
- URL updates on sort change
- Page load with sort params → applies sort automatically
- Sorting works with pagination (sorts entire dataset, not just current page)
- Icons update correctly

Use Heroicons for arrow icons (we use them throughout the app)."
```

**Why this works:**
- ✅ Detailed interaction behavior
- ✅ Visual feedback specified
- ✅ State management approach defined
- ✅ Integration with URL routing
- ✅ Handles pagination interaction
- ✅ References specific pattern
- ✅ Consistent icon library

**Outcome:** Complete sorting implementation that works exactly as specified, maintains project patterns, no follow-up fixes needed.

---

### Pattern 2: Complex Feature with Multiple Components

**Use when:** Feature requires multiple files/components working together

**Template:**

```
Implement [FEATURE_NAME] across multiple files.

Architecture:
[High-level component breakdown]

Implementation order:
1. [step 1]
2. [step 2]
3. [step 3]

For this prompt, implement: [STEP_N]

[Detailed requirements for this step]

Integration points:
- [interface 1]
- [interface 2]

Reference: [similar feature] in [files]
```

**Real Example 3: Real-Time Notifications System**

**Bad prompt:**
```
"Create a notification system"
```

**Good prompt (Step 1):**
```
"Implement real-time notifications system. This is STEP 1 of 4 - Backend WebSocket setup.

Architecture overview:
├─ Backend: WebSocket server (src/websocket/notifications.ts)
├─ State: Zustand store (src/stores/notificationStore.ts)
├─ UI: NotificationCenter component (src/components/NotificationCenter.tsx)
└─ Backend API: Notification CRUD (src/api/notifications.ts)

For this step: Create the WebSocket server.

Requirements:
- File: src/websocket/notifications.ts
- Library: Use 'ws' (already installed)
- Port: 8080 (separate from main app on 3000)
- Authentication: Verify JWT token on connection
- Events to handle:
  - 'notification:new' → broadcast to specific user
  - 'notification:read' → mark as read
  - 'notification:delete' → remove notification

Message format:
{
  type: 'notification:new' | 'notification:read' | 'notification:delete',
  payload: {
    id: string,
    userId: string,
    message: string,
    type: 'info' | 'success' | 'warning' | 'error',
    timestamp: number
  }
}

Follow the WebSocket pattern in src/websocket/chat.ts (our existing chat feature).

Error handling:
- Invalid JWT → close connection with code 4001
- Malformed message → log error, send error response, don't close connection
- Connection errors → implement exponential backoff reconnection client-side (later step)

Success criteria:
- Server starts on port 8080
- Accepts WebSocket connections
- Validates JWT on connect
- Broadcasts messages to correct user
- Handles disconnections gracefully"
```

**Good prompt (Step 2):**
```
"Notification system STEP 2 of 4 - Frontend state management.

Create Zustand store in src/stores/notificationStore.ts.

Store shape:
{
  notifications: Notification[],
  unreadCount: number,
  isConnected: boolean,
  socket: WebSocket | null
}

Actions:
- connect(token: string) → establish WebSocket connection
- disconnect() → close connection
- addNotification(notification: Notification) → add to array, increment unread
- markAsRead(id: string) → update notification, decrement unread
- deleteNotification(id: string) → remove from array
- clearAll() → empty notifications array

WebSocket integration:
- connect() establishes connection to ws://localhost:8080
- Listens for 'notification:new' → calls addNotification
- Sends 'notification:read' on markAsRead
- Sends 'notification:delete' on deleteNotification
- Handles reconnection on disconnect (exponential backoff: 1s, 2s, 4s, 8s, max 30s)

Follow our Zustand patterns in src/stores/userStore.ts and src/stores/chatStore.ts.

Success criteria:
- Store connects to WebSocket server
- Actions update state correctly
- WebSocket messages trigger state updates
- Reconnection works after disconnect
- No memory leaks on unmount"
```

**Why this works:**
- ✅ Breaks complex feature into manageable steps
- ✅ Each step has clear, focused scope
- ✅ Shows architecture overview for context
- ✅ Step-by-step implementation prevents overwhelm
- ✅ Each step can be verified independently
- ✅ References existing patterns

**Outcome:** Clean, working implementation at each step. Easy to debug. Maintainable code structure.

---

### Pattern 3: Feature Integration

**Use when:** Adding feature that integrates with multiple existing systems

**Template:**

```
Implement [FEATURE] that integrates with [SYSTEMS].

Feature requirements:
[core functionality]

Integration points:
1. [System 1]: [how it integrates]
2. [System 2]: [how it integrates]
3. [System 3]: [how it integrates]

Maintain compatibility with:
- [constraint 1]
- [constraint 2]

Testing approach:
- [test scenario 1]
- [test scenario 2]
```

**Real Example 4: Two-Factor Authentication**

**Bad prompt:**
```
"Add 2FA"
```

**Good prompt:**
```
"Implement two-factor authentication (2FA) that integrates with our existing auth system.

Feature requirements:
- TOTP-based 2FA (Time-based One-Time Password)
- Users can enable/disable 2FA in account settings
- Required on login after password verification
- Backup codes (10) generated when enabling 2FA
- QR code for easy setup with authenticator apps

Integration points:

1. User Model (src/models/User.ts):
   - Add fields: twoFactorEnabled: boolean, twoFactorSecret: string | null, backupCodes: string[]
   - Migration: Create new migration file in src/database/migrations/

2. Auth API (src/api/auth.ts):
   - Modify POST /api/auth/login:
     - After password verification, check twoFactorEnabled
     - If true: return { requiresTwoFactor: true, tempToken: string } instead of JWT
     - If false: continue normal flow (return JWT)
   - Add POST /api/auth/verify-2fa:
     - Accepts: tempToken, code (6 digits)
     - Validates TOTP code or backup code
     - Returns: JWT on success
   - Don't break existing OAuth flow (src/api/auth/oauth.ts)

3. Settings Page (src/pages/Settings.tsx):
   - Add 2FA section
   - Enable 2FA button → shows QR code + secret + backup codes
   - Disable 2FA button → requires password confirmation
   - Regenerate backup codes button

Libraries:
- Use 'otplib' for TOTP generation/verification (add to package.json)
- Use 'qrcode' for QR code generation (add to package.json)

Security requirements:
- Store twoFactorSecret encrypted (use our existing encrypt/decrypt utils in src/utils/crypto.ts)
- Hash backup codes before storing (use bcrypt, like passwords)
- Rate limit 2FA verification: 5 attempts per 15 minutes per user
- Temp tokens expire in 5 minutes

UX requirements:
- Show remaining backup codes count
- Warn when <3 backup codes remaining
- Success/error messages match our existing toast pattern (src/components/Toast.tsx)
- Loading states during verification

Edge cases:
- User loses access to authenticator → can use backup codes
- User loses backup codes → must disable 2FA via email recovery (separate feature, not in this scope)
- Clock drift → allow 1-step window tolerance (otplib handles this)

Testing:
- Manual test: Enable 2FA → login with 2FA → use backup code → disable 2FA
- Test rate limiting works
- Test temp token expiration

Success criteria:
- 2FA can be enabled/disabled without errors
- Login flow works with and without 2FA
- Backup codes work correctly
- All existing auth flows still work (OAuth, email/password)
- No security vulnerabilities (secrets encrypted, codes hashed)
- UI matches existing design patterns"
```

**Why this works:**
- ✅ Comprehensive integration points mapped out
- ✅ Security requirements explicit
- ✅ UX behavior defined
- ✅ Edge cases considered
- ✅ Compatibility maintained
- ✅ Libraries specified
- ✅ Testing approach included

**Outcome:** Complete 2FA implementation that integrates seamlessly, maintains security standards, doesn't break existing features.

---

## Debugging & Error Resolution

### Overview

**Goal:** Get AI to quickly identify and fix bugs with minimal back-and-forth.

**Key principle:** More data = faster resolution

**Success pattern:**

```
Error message + Context + Expected vs Actual + Already tried
= Quick, accurate fix
```

---

### Pattern 1: Runtime Error Debugging

**Use when:** App crashes or throws errors during execution

**Template:**

```
[PROBLEM]: Brief description

[ERROR MESSAGE]:
[exact error message]

[STACK TRACE]:
[relevant stack trace lines]

[CONTEXT]:
- File: [path:line where error occurs]
- Action: [what user was doing]
- Environment: [dev/staging/prod]
- Started happening: [when]

[EXPECTED vs ACTUAL]:
- Expected: [behavior]
- Actual: [behavior]

[ALREADY TRIED]:
- [attempt 1] → [result]
- [attempt 2] → [result]

[RELEVANT CODE]:
[paste or reference]
```

**Real Example 1: Null Pointer Error**

**Bad prompt:**
```
"Fix the bug in login"
```

**Good prompt:**
```
"Fix null pointer error in login flow.

ERROR MESSAGE:
TypeError: Cannot read property 'id' of undefined
  at handleLogin (src/api/auth.ts:45:31)

STACK TRACE:
  at handleLogin (src/api/auth.ts:45:31)
  at validateAndLogin (src/api/auth.ts:23:12)
  at /src/middleware/validation.ts:15:5

CONTEXT:
- File: src/api/auth.ts line 45
- Action: User submitted login form with valid email/password
- Environment: Development
- Started happening: After we added email verification feature yesterday
- Only affects users with emailVerified: false
- Users with emailVerified: true can login fine

CODE (src/api/auth.ts lines 40-50):
```typescript
async function handleLogin(req, res) {
  const { email, password } = req.body;

  const user = await User.findByEmail(email);
  const isValid = await bcrypt.compare(password, user.password);

  if (!isValid) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }

  const token = jwt.sign({ id: user.id }, SECRET); // LINE 45 - ERROR HERE
  return res.json({ token });
}
```

EXPECTED vs ACTUAL:
- Expected: Return 401 for unverified users OR allow login and prompt verification
- Actual: 500 error crash

ALREADY TRIED:
- Added console.log before line 45 → user is undefined for unverified emails
- Checked User.findByEmail → returns null for unverified users (correct)
- Looked at recent changes → email verification PR modified User.findByEmail

HYPOTHESIS:
User.findByEmail now returns null for unverified users, but we're not checking for null before accessing user.id.

Please fix this and handle unverified users properly (return clear error message)."
```

**Why this works:**
- ✅ Exact error message provided
- ✅ Stack trace shows error location
- ✅ Context narrows down cause
- ✅ Code snippet included
- ✅ Already tried shows investigation done
- ✅ Hypothesis guides AI

**AI response:**
```
"Your hypothesis is correct. User.findByEmail returns null for unverified users.

Fix:
```typescript
async function handleLogin(req, res) {
  const { email, password } = req.body;

  const user = await User.findByEmail(email);

  // Fix: Check if user exists
  if (!user) {
    return res.status(401).json({
      error: 'Email not verified or invalid credentials'
    });
  }

  const isValid = await bcrypt.compare(password, user.password);

  if (!isValid) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }

  const token = jwt.sign({ id: user.id }, SECRET);
  return res.json({ token });
}
```
```

**Outcome:** Bug fixed in one iteration with clear explanation.

---

**Real Example 2: Async/Race Condition Bug**

**Bad prompt:**
```
"Data doesn't load correctly sometimes"
```

**Good prompt:**
```
"Fix race condition causing stale data in user profile.

PROBLEM:
User profile sometimes shows outdated information after update. Happens ~30% of the time.

ERROR MESSAGE:
No error thrown, but data is incorrect.

CONTEXT:
- File: src/pages/UserProfile.tsx
- Action: User updates profile (name/email) → navigates to profile page
- Environment: Production
- Started happening: After we switched from REST to optimistic updates with React Query

EXPECTED vs ACTUAL:
- Expected: Profile page shows updated name/email immediately
- Actual: Sometimes shows old data, refresh shows new data

REPRODUCTION:
1. Update profile name
2. Click save
3. Navigate to profile page immediately (< 100ms after save)
4. ~30% of time: old name still shown

RELEVANT CODE:

src/pages/UserProfile.tsx:
```typescript
function UserProfile() {
  const { data: user } = useQuery(['user', userId], fetchUser);
  return <div>{user?.name}</div>;
}
```

src/api/userApi.ts:
```typescript
export async function updateUser(userId, data) {
  const response = await fetch(`/api/users/${userId}`, {
    method: 'PUT',
    body: JSON.stringify(data)
  });
  return response.json();
}
```

src/hooks/useUpdateUser.ts:
```typescript
export function useUpdateUser() {
  const queryClient = useQueryClient();

  return useMutation(updateUser, {
    onSuccess: (data, variables) => {
      // Optimistic update
      queryClient.setQueryData(['user', variables.userId], data);
    }
  });
}
```

ALREADY TRIED:
- Added console.logs → confirmed API returns new data
- React Query devtools → sometimes shows old data in cache
- Delay navigation by 500ms → problem goes away (but bad UX)

HYPOTHESIS:
Race condition: Profile page query runs before mutation updates cache, fetches old data from server, overwrites cache with stale data.

How can we ensure mutation updates cache before profile page query runs?"
```

**Why this works:**
- ✅ Intermittent bug clearly described
- ✅ Reproduction steps provided
- ✅ Relevant code from multiple files
- ✅ Investigation results included
- ✅ Clear hypothesis
- ✅ Specific question

**AI response:**
```
"Your hypothesis is correct. Classic React Query race condition.

The problem: Profile page query runs independently and overwrites the optimistic update.

Solution: Invalidate queries instead of manually setting data:

```typescript
export function useUpdateUser() {
  const queryClient = useQueryClient();

  return useMutation(updateUser, {
    onSuccess: (data, variables) => {
      // Instead of setQueryData, invalidate to trigger refetch
      queryClient.invalidateQueries(['user', variables.userId]);
    }
  });
}
```

This ensures:
1. Mutation completes
2. Cache is marked stale
3. Any active queries refetch fresh data
4. No race condition

Alternative (if refetch is too slow):
```typescript
onMutate: async (variables) => {
  // Cancel outgoing queries
  await queryClient.cancelQueries(['user', variables.userId]);

  // Snapshot current data
  const snapshot = queryClient.getQueryData(['user', variables.userId]);

  // Optimistically update
  queryClient.setQueryData(['user', variables.userId], (old) => ({
    ...old,
    ...variables.data
  }));

  return { snapshot };
},
onError: (err, variables, context) => {
  // Rollback on error
  queryClient.setQueryData(['user', variables.userId], context.snapshot);
},
onSettled: (data, error, variables) => {
  // Refetch to ensure consistency
  queryClient.invalidateQueries(['user', variables.userId]);
}
```

This cancels racing queries and handles rollback."
```

**Outcome:** Two solutions provided - simple fix and robust optimistic update pattern. Race condition eliminated.

---

### Pattern 2: Logic Bug Debugging

**Use when:** Code runs but produces wrong results

**Template:**

```
[BUG]: What's wrong

[EXPECTED BEHAVIOR]:
[detailed description]

[ACTUAL BEHAVIOR]:
[detailed description]

[TEST CASE]:
Input: [data]
Expected output: [result]
Actual output: [result]

[CODE]:
[relevant function]

[ANALYSIS]:
[what you've discovered]
```

**Real Example 3: Calculation Bug**

**Bad prompt:**
```
"The total is wrong"
```

**Good prompt:**
```
"Fix incorrect total calculation in shopping cart.

BUG:
Cart total doesn't match sum of item prices when discount codes are applied.

EXPECTED BEHAVIOR:
1. Calculate subtotal: sum of (item.price × item.quantity)
2. Apply discount: subtotal × (discount.percentage / 100)
3. Calculate total: subtotal - discount
4. Add tax: total × 1.08 (8% tax)
5. Final total: total + tax

ACTUAL BEHAVIOR:
When discount code applied, tax is calculated on subtotal (before discount) instead of discounted total.

TEST CASE:
Input:
- Items: 2 × $10 product = $20 subtotal
- Discount code: 50% off
- Expected discount: $10
- Expected total before tax: $10
- Expected tax (8% of $10): $0.80
- Expected final total: $10.80

Actual:
- Subtotal: $20 ✓
- Discount: $10 ✓
- Total before tax: $10 ✓
- Tax: $1.60 (8% of $20 - WRONG, should be 8% of $10)
- Final total: $11.60 (WRONG, should be $10.80)

CODE (src/utils/cartCalculations.ts):
```typescript
export function calculateCartTotal(items, discountCode) {
  const subtotal = items.reduce((sum, item) => {
    return sum + (item.price * item.quantity);
  }, 0);

  let discount = 0;
  if (discountCode) {
    discount = subtotal * (discountCode.percentage / 100);
  }

  const total = subtotal - discount;
  const tax = subtotal * 0.08; // BUG: Should be total * 0.08

  return {
    subtotal,
    discount,
    total,
    tax,
    finalTotal: total + tax
  };
}
```

ANALYSIS:
Line 16: `const tax = subtotal * 0.08` should be `const tax = total * 0.08`.

Tax should be calculated on discounted total, not original subtotal.

Please fix this bug and add a test case to prevent regression."
```

**Why this works:**
- ✅ Clear expected vs actual behavior
- ✅ Concrete test case with numbers
- ✅ Code included with bug location marked
- ✅ Root cause identified
- ✅ Requests test to prevent regression

**Outcome:** Bug fixed immediately, test added, no future regressions.

---

## Refactoring

### Overview

**Goal:** Improve code structure without changing behavior.

**Key principle:** Clarity about what changes and what stays the same.

**Success pattern:**

```
Current problems + Desired state + Migration path + Behavior preservation
= Safe, effective refactor
```

---

### Pattern 1: Component Refactoring

**Use when:** Simplifying or restructuring component code

**Template:**

```
Refactor [COMPONENT] from [OLD_APPROACH] to [NEW_APPROACH].

CURRENT PROBLEMS:
- [problem 1]
- [problem 2]

DESIRED STATE:
- [goal 1]
- [goal 2]

MUST PRESERVE:
- [behavior 1]
- [behavior 2]

CHANGES ALLOWED:
- [change 1]
- [change 2]

SUCCESS CRITERIA:
- Tests still pass
- [specific requirement]
```

**Real Example 1: Class to Hooks**

**Bad prompt:**
```
"Convert this component to use hooks"
```

**Good prompt:**
```
"Refactor UserProfile component from class component to functional component with hooks.

FILE: src/components/UserProfile.tsx

CURRENT PROBLEMS:
- Class component is verbose (200 lines)
- Lifecycle methods scattered (componentDidMount, componentDidUpdate, componentWillUnmount)
- Logic duplicated between lifecycle methods
- Hard to extract reusable logic
- setState calls are hard to track

DESIRED STATE:
- Functional component with hooks
- useEffect for lifecycle logic (consolidated)
- Custom hooks for reusable logic (user fetching, subscription)
- Cleaner, more readable code
- ~100 lines after refactor

MUST PRESERVE:
- All functionality exactly the same
- Props interface unchanged (other components depend on it)
- Subscription cleanup on unmount (critical - no memory leaks)
- Loading/error states work identically
- Component still exports UserProfile as default

REFACTORING APPROACH:
1. Convert state to useState hooks
2. Convert componentDidMount + componentDidUpdate → useEffect
3. Convert componentWillUnmount cleanup → useEffect cleanup
4. Extract user fetching → custom useUser hook
5. Extract subscription → custom useUserSubscription hook

CURRENT CODE:
```typescript
class UserProfile extends React.Component<Props, State> {
  subscription: any = null;

  state = {
    user: null,
    loading: true,
    error: null
  };

  componentDidMount() {
    this.fetchUser();
    this.setupSubscription();
  }

  componentDidUpdate(prevProps) {
    if (prevProps.userId !== this.props.userId) {
      this.fetchUser();
      this.teardownSubscription();
      this.setupSubscription();
    }
  }

  componentWillUnmount() {
    this.teardownSubscription();
  }

  fetchUser = async () => {
    this.setState({ loading: true, error: null });
    try {
      const user = await api.getUser(this.props.userId);
      this.setState({ user, loading: false });
    } catch (error) {
      this.setState({ error, loading: false });
    }
  };

  setupSubscription = () => {
    this.subscription = userUpdates.subscribe(
      this.props.userId,
      (update) => {
        this.setState({ user: update });
      }
    );
  };

  teardownSubscription = () => {
    if (this.subscription) {
      this.subscription.unsubscribe();
      this.subscription = null;
    }
  };

  render() {
    const { user, loading, error } = this.state;

    if (loading) return <Loading />;
    if (error) return <Error error={error} />;
    if (!user) return null;

    return (
      <div className="profile">
        <Avatar src={user.avatar} />
        <h1>{user.name}</h1>
        <p>{user.email}</p>
      </div>
    );
  }
}
```

CUSTOM HOOKS TO CREATE:
1. useUser(userId) → { user, loading, error }
2. useUserSubscription(userId, onUpdate) → handles subscription lifecycle

SUCCESS CRITERIA:
- Component works identically
- Tests pass without modification
- Subscription cleanup verified (check with React DevTools)
- Code is <100 lines
- Logic extracted to reusable custom hooks
- ESLint passes (no warnings)"
```

**Why this works:**
- ✅ Clear problems identified
- ✅ Desired outcome described
- ✅ Critical behavior preservation listed
- ✅ Refactoring approach outlined
- ✅ Current code provided
- ✅ Success criteria measurable

**Outcome:** Clean refactor that maintains all functionality, improves code quality, extracts reusable hooks.

---

### Pattern 2: Architecture Refactoring

**Use when:** Restructuring multiple files or modules

**Template:**

```
Refactor [SYSTEM] architecture from [OLD] to [NEW].

RATIONALE:
[why refactoring is needed]

SCOPE:
Files affected: [list]
Files NOT changing: [list]

MIGRATION PLAN:
Phase 1: [step]
Phase 2: [step]
Phase 3: [step]

For this prompt: Implement Phase [N]

[Detailed phase requirements]

BACKWARD COMPATIBILITY:
[how to maintain during migration]
```

**Real Example 2: Service Layer Introduction**

**Bad prompt:**
```
"Add service layer pattern"
```

**Good prompt:**
```
"Refactor API routes to use service layer pattern. PHASE 1 of 3.

RATIONALE:
Current problem:
- Business logic mixed in route handlers
- No code reuse between routes
- Hard to test (requires HTTP mocks)
- Difficult to add new API versions
- Transaction management scattered

Desired state:
- Routes → thin controllers (validation, response formatting)
- Services → business logic (reusable, testable)
- Repositories → data access
- Clear separation of concerns

ARCHITECTURE:

Current:
```
routes/userRoutes.ts → direct database access
```

New:
```
routes/userRoutes.ts → services/UserService.ts → repositories/UserRepository.ts
```

SCOPE:

Phase 1 (this prompt): User module
- Refactor src/api/users.ts routes
- Create src/services/UserService.ts
- Create src/repositories/UserRepository.ts

Phase 2 (later): Post module
Phase 3 (later): Comment module

Files affected (Phase 1):
- src/api/users.ts (routes - modify)
- src/services/UserService.ts (new)
- src/repositories/UserRepository.ts (new)
- src/models/User.ts (unchanged, just reference)

Files NOT changing yet:
- All other routes (posts, comments, etc.)
- Database connection (src/database/connection.ts)
- Middleware (validation, auth)

PHASE 1 REQUIREMENTS:

1. Create src/repositories/UserRepository.ts:
```typescript
export class UserRepository {
  async findById(id: string): Promise<User | null>
  async findByEmail(email: string): Promise<User | null>
  async create(data: CreateUserDTO): Promise<User>
  async update(id: string, data: UpdateUserDTO): Promise<User>
  async delete(id: string): Promise<void>
  async findMany(filters: UserFilters): Promise<User[]>
}
```

2. Create src/services/UserService.ts:
```typescript
export class UserService {
  constructor(private userRepo: UserRepository) {}

  async createUser(data: CreateUserDTO): Promise<User>
  async updateUser(id: string, data: UpdateUserDTO): Promise<User>
  async deleteUser(id: string): Promise<void>
  async getUser(id: string): Promise<User>
  async listUsers(filters: UserFilters): Promise<User[]>
}
```

Business logic goes here:
- Email uniqueness check
- Password hashing
- Validation beyond schema validation
- Welcome email sending

3. Refactor src/api/users.ts:
Update routes to use UserService instead of direct database calls.

Keep in routes:
- Request validation (express-validator)
- Response formatting
- HTTP status codes
- Error handling (try-catch)

Move to service:
- Database queries
- Business logic
- Transaction management

EXAMPLE TRANSFORMATION:

Before (src/api/users.ts):
```typescript
router.post('/users', async (req, res) => {
  try {
    const { email, password, name } = req.body;

    // Business logic mixed in route
    const existingUser = await db.users.findOne({ email });
    if (existingUser) {
      return res.status(400).json({ error: 'Email already exists' });
    }

    const hashedPassword = await bcrypt.hash(password, 10);

    const user = await db.users.create({
      email,
      password: hashedPassword,
      name
    });

    await emailService.sendWelcomeEmail(user.email);

    return res.status(201).json(user);
  } catch (error) {
    return res.status(500).json({ error: 'Internal server error' });
  }
});
```

After (src/api/users.ts):
```typescript
router.post('/users', async (req, res) => {
  try {
    const { email, password, name } = req.body;

    // Route just orchestrates
    const user = await userService.createUser({ email, password, name });

    return res.status(201).json(user);
  } catch (error) {
    if (error instanceof ValidationError) {
      return res.status(400).json({ error: error.message });
    }
    return res.status(500).json({ error: 'Internal server error' });
  }
});
```

UserService.createUser:
```typescript
async createUser(data: CreateUserDTO): Promise<User> {
  // Business logic now in service
  const existingUser = await this.userRepo.findByEmail(data.email);
  if (existingUser) {
    throw new ValidationError('Email already exists');
  }

  const hashedPassword = await bcrypt.hash(data.password, 10);

  const user = await this.userRepo.create({
    ...data,
    password: hashedPassword
  });

  await emailService.sendWelcomeEmail(user.email);

  return user;
}
```

BACKWARD COMPATIBILITY:
- Routes maintain same API contract (no breaking changes)
- Response formats unchanged
- Status codes unchanged
- Error messages unchanged

TESTING:
- Existing route tests should still pass
- Add new service unit tests
- Add new repository unit tests

SUCCESS CRITERIA:
- All user routes refactored to use UserService
- Business logic moved to service layer
- Data access moved to repository layer
- Existing API tests pass without modification
- New service/repository tests added
- Code is more maintainable and testable"
```

**Why this works:**
- ✅ Clear rationale for refactoring
- ✅ Phased approach prevents overwhelm
- ✅ Scope clearly defined
- ✅ Before/after examples provided
- ✅ Backward compatibility considered
- ✅ Testing strategy included

**Outcome:** Systematic refactor that improves architecture while maintaining functionality. Can be applied to other modules in phases.

---

## Code Review

### Overview

**Goal:** Get AI to thoroughly review code against specific criteria.

**Key principle:** Provide context and checklist for focused review.

**Success pattern:**

```
Code to review + Review criteria + Context + Specific concerns
= Thorough, actionable review
```

---

### Pattern 1: Pull Request Review

**Use when:** Reviewing code changes before merge

**Template:**

```
Review PR #[NUMBER]: [TITLE]

FILES CHANGED:
[list]

REVIEW CRITERIA:
- [criterion 1]
- [criterion 2]

CONTEXT:
[what feature/fix this is]

SPECIFIC CONCERNS:
[areas to focus on]

Output format:
- Issues found (categorized by severity)
- Security concerns
- Suggested improvements
```

**Real Example 1: Feature PR Review**

**Bad prompt:**
```
"Review this PR"
```

**Good prompt:**
```
"Review PR #142: Add password reset functionality

FILES CHANGED:
- src/api/auth/passwordReset.ts (new, 150 lines)
- src/models/User.ts (modified, added resetToken fields)
- src/services/EmailService.ts (modified, added resetEmail method)
- src/middleware/rateLimit.ts (modified, added reset endpoint limits)
- tests/auth/passwordReset.test.ts (new, 80 lines)

REVIEW CRITERIA:

Security (high priority):
- [ ] Reset tokens are cryptographically random
- [ ] Tokens expire appropriately
- [ ] No timing attacks (compare timing-safe)
- [ ] Rate limiting properly configured
- [ ] Email sent over secure channel
- [ ] Tokens are single-use
- [ ] Old tokens invalidated on new request

Code Quality:
- [ ] Follows our API patterns (see src/api/auth/login.ts)
- [ ] Error handling comprehensive
- [ ] Validation proper (email format, etc.)
- [ ] Tests cover edge cases
- [ ] No sensitive data in logs

Business Logic:
- [ ] Email contains secure reset link
- [ ] Link works only once
- [ ] Expired link shows appropriate message
- [ ] Success/failure doesn't reveal if email exists (security)

Performance:
- [ ] Database queries optimized (no n+1)
- [ ] Expensive operations (token generation) done efficiently

CONTEXT:
This implements user-requested password reset via email. User enters email → receives link → clicks link → sets new password.

SPECIFIC CONCERNS:
1. Security is critical here - this is authentication-related
2. Make sure we don't leak information about whether email exists in system
3. Rate limiting must prevent abuse
4. Token generation must be secure (not predictable)
5. Check if tests cover the security edge cases

OUTPUT FORMAT:
Please provide:

1. Critical Issues (must fix before merge)
2. Security Concerns (even minor ones)
3. Code Quality Issues (nice to fix)
4. Test Coverage Gaps
5. Overall Assessment (approve/request changes)"
```

**Why this works:**
- ✅ Specific files listed
- ✅ Detailed review checklist
- ✅ Security focus appropriate for feature
- ✅ Context explains what feature does
- ✅ Specific concerns highlighted
- ✅ Output format structured

**Outcome:** Thorough review identifying security issues, code quality problems, and test gaps that human reviewer might miss.

---

## Performance Optimization

### Overview

**Goal:** Get AI to identify and fix performance bottlenecks.

**Key principle:** Provide performance data, not just code.

---

### Pattern 1: Performance Analysis

**Real Example:**

**Good prompt:**
```
"Optimize slow user list page performance.

PROBLEM:
Page takes 3 seconds to load with 1000 users. Target: <500ms.

PERFORMANCE DATA:
- Network tab: GET /api/users takes 2800ms
- React DevTools: UserList render takes 400ms
- Database query time: 2500ms (from logs)

FILES:
- src/api/users.ts (API endpoint)
- src/components/UserList.tsx (frontend component)
- src/database/queries/users.ts (database query)

CURRENT IMPLEMENTATION:

API (src/api/users.ts):
```typescript
router.get('/api/users', async (req, res) => {
  const users = await User.findAll({
    include: [Profile, Posts, Comments] // Eager loading
  });
  return res.json(users);
});
```

Component (src/components/UserList.tsx):
```typescript
function UserList() {
  const { data: users } = useQuery('users', fetchUsers);

  return (
    <div>
      {users.map(user => (
        <UserCard
          key={user.id}
          user={user}
          posts={user.posts}
          profile={user.profile}
        />
      ))}
    </div>
  );
}
```

Database query logs show:
- 1 query for users: 100ms
- 1000 queries for profiles: 2000ms (n+1 problem!)
- 1000 queries for posts: 400ms (n+1 problem!)

CONSTRAINTS:
- Must still show user profile data
- Must show post count per user
- Don't need individual post details
- Pagination is acceptable if needed
- Virtual scrolling is acceptable
- Must work with existing database (PostgreSQL)

OPTIMIZATION IDEAS:
1. Fix n+1 queries (eager loading or separate joined queries)
2. Add pagination (20 users per page)
3. Use virtual scrolling on frontend
4. Cache results (React Query already configured)
5. Return only needed fields (not full post objects)

What's the best approach? Please implement the most effective solution."
```

**Outcome:** AI identifies n+1 problem, suggests pagination + proper eager loading, implements solution.

---

## Testing

### Overview

**Goal:** Get AI to write comprehensive, meaningful tests.

---

### Pattern 1: Test Generation

**Real Example:**

**Good prompt:**
```
"Write comprehensive tests for UserService.createUser method.

CODE TO TEST (src/services/UserService.ts):
```typescript
async createUser(data: CreateUserDTO): Promise<User> {
  // Validate email format
  if (!isValidEmail(data.email)) {
    throw new ValidationError('Invalid email format');
  }

  // Check if email already exists
  const existingUser = await this.userRepo.findByEmail(data.email);
  if (existingUser) {
    throw new ConflictError('Email already exists');
  }

  // Hash password
  const hashedPassword = await bcrypt.hash(data.password, 10);

  // Create user
  const user = await this.userRepo.create({
    ...data,
    password: hashedPassword
  });

  // Send welcome email (async, don't wait)
  emailService.sendWelcomeEmail(user.email).catch(err => {
    logger.error('Failed to send welcome email', err);
  });

  return user;
}
```

TEST FILE: tests/services/UserService.test.ts

TEST FRAMEWORK: Jest
MOCKING: Use jest.mock() for dependencies

SCENARIOS TO COVER:

Happy path:
- [ ] Valid data → creates user successfully
- [ ] Password is hashed (not stored plain)
- [ ] Welcome email is sent
- [ ] Returns created user

Validation errors:
- [ ] Invalid email format → throws ValidationError
- [ ] Missing required fields → throws ValidationError
- [ ] Empty email → throws ValidationError
- [ ] Empty password → throws ValidationError

Conflict errors:
- [ ] Duplicate email → throws ConflictError
- [ ] Case-insensitive email check (John@example.com == john@example.com)

Edge cases:
- [ ] Very long email → handles appropriately
- [ ] Special characters in name → handles appropriately
- [ ] Email sending fails → user still created, error logged
- [ ] Database error → throws appropriate error

Security:
- [ ] Password not returned in response
- [ ] Password is actually hashed (not plain text)
- [ ] Hash is bcrypt format

TEST STRUCTURE:
```typescript
describe('UserService', () => {
  describe('createUser', () => {
    describe('when data is valid', () => {
      it('creates user successfully', () => {});
      it('hashes password', () => {});
      it('sends welcome email', () => {});
    });

    describe('when data is invalid', () => {
      it('throws ValidationError for invalid email', () => {});
      // ...
    });

    describe('when email exists', () => {
      it('throws ConflictError', () => {});
    });

    describe('edge cases', () => {
      // ...
    });
  });
});
```

MOCKING SETUP:
- Mock UserRepository methods (findByEmail, create)
- Mock emailService.sendWelcomeEmail
- Mock logger
- Mock bcrypt.hash

Please write complete, runnable tests following this structure."
```

**Outcome:** Comprehensive test suite covering all scenarios, properly mocked, following project patterns.

---

## Documentation

### Overview

**Goal:** Get AI to write clear, useful documentation.

---

### Pattern 1: API Documentation

**Real Example:**

**Good prompt:**
```
"Generate API documentation for user endpoints.

ENDPOINTS TO DOCUMENT:
- POST /api/users (create user)
- GET /api/users/:id (get user)
- PUT /api/users/:id (update user)
- DELETE /api/users/:id (delete user)
- GET /api/users (list users)

DOCUMENTATION FORMAT: OpenAPI 3.0 (Swagger)

LOCATION: docs/api/users.yaml

REQUIREMENTS:

For each endpoint, include:
- Description
- Request body schema (if applicable)
- Query parameters (if applicable)
- Response schemas (success + errors)
- Example requests/responses
- Authentication requirements
- Error codes with explanations

SPECIFIC DETAILS:

POST /api/users:
- Public endpoint (no auth)
- Required fields: email, password, name
- Email must be unique
- Password min 8 characters
- Returns 201 on success
- Errors: 400 (validation), 409 (email exists)

GET /api/users/:id:
- Requires authentication (JWT token)
- Returns user object (without password)
- Errors: 401 (unauthorized), 404 (not found)

PUT /api/users/:id:
- Requires authentication (JWT token)
- Can only update own user (unless admin)
- Updatable fields: name, email (email must still be unique)
- Errors: 401 (unauthorized), 403 (forbidden), 404 (not found), 409 (email exists)

DELETE /api/users/:id:
- Requires authentication (JWT token)
- Admin only
- Soft delete (sets deletedAt timestamp)
- Errors: 401 (unauthorized), 403 (forbidden), 404 (not found)

GET /api/users:
- Requires authentication (JWT token)
- Pagination: ?page=1&limit=20 (default: page 1, limit 20)
- Filtering: ?search=john (searches name and email)
- Sorting: ?sort=name&order=asc (default: createdAt desc)
- Returns array of users + pagination metadata

Use our existing User schema from src/models/User.ts:
```typescript
interface User {
  id: string;
  email: string;
  name: string;
  role: 'user' | 'admin';
  createdAt: Date;
  updatedAt: Date;
  deletedAt: Date | null;
}
```

EXAMPLE STYLE:
Follow the format used in docs/api/auth.yaml (our existing API docs)."
```

**Outcome:** Complete, accurate API documentation in OpenAPI format, ready to use with Swagger UI.

---

## Security Hardening

### Overview

**Goal:** Get AI to identify and fix security vulnerabilities.

---

### Pattern 1: Security Audit

**Real Example:**

**Good prompt:**
```
"Security audit of authentication system.

SCOPE:
- src/api/auth/ (all auth endpoints)
- src/middleware/auth.ts (JWT verification)
- src/models/User.ts (user model)

AUDIT FOR:

Authentication:
- [ ] Password storage (should be bcrypt/argon2)
- [ ] Password minimum requirements enforced
- [ ] JWT secret is strong and env variable
- [ ] JWT expiration set appropriately
- [ ] Refresh token mechanism secure

Authorization:
- [ ] Role-based access control enforced
- [ ] User can only access own resources
- [ ] Admin routes properly protected

Input Validation:
- [ ] SQL injection prevention
- [ ] XSS prevention (input sanitization)
- [ ] Email validation
- [ ] Parameter validation

Session Management:
- [ ] Sessions expire appropriately
- [ ] Logout invalidates tokens
- [ ] Concurrent session handling

Rate Limiting:
- [ ] Login endpoint rate limited
- [ ] Password reset rate limited
- [ ] API endpoints rate limited

Information Disclosure:
- [ ] Errors don't leak sensitive info
- [ ] Stack traces not returned in production
- [ ] Timing attacks prevented (equal-time comparison)

CURRENT IMPLEMENTATION:
[Include relevant code files]

Please provide:
1. Critical vulnerabilities (must fix immediately)
2. Medium-priority issues
3. Best practice improvements
4. Specific code changes needed

For each issue:
- What the vulnerability is
- How it can be exploited
- How to fix it
- Code example of fix"
```

**Outcome:** Detailed security audit identifying vulnerabilities, exploitation scenarios, and specific fixes.

---

## Summary

### When to Use Each Pattern

| Task Type | Use When | Key Elements |
|-----------|----------|--------------|
| **Feature Implementation** | Building new functionality | Requirements + Context + Patterns + Examples |
| **Debugging** | Fixing errors/bugs | Error + Stack trace + Context + Already tried |
| **Refactoring** | Improving code structure | Problems + Goals + Preservation + Migration |
| **Code Review** | Reviewing changes | Files + Criteria + Context + Concerns |
| **Testing** | Writing tests | Code + Scenarios + Structure + Mocking |
| **Documentation** | Writing docs | Scope + Format + Details + Examples |
| **Performance** | Optimizing speed | Data + Bottlenecks + Constraints + Goals |
| **Security** | Hardening security | Scope + Checklist + Standards + Severity |

---

**Next Steps:**
- [Advanced Techniques](./advanced-techniques.md) → Multi-step workflows, prompt chaining
- [Template Library](./template-library.md) → Copy-paste ready prompts
- [Foundations](./foundations.md) → Core prompting principles

**Back to:** [Prompting Guide Home](./README.md)
