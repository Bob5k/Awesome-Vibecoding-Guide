# Prompt Template Library 📚

**Copy-paste ready prompts for common development scenarios**

**How to use:** Find your scenario, copy template, fill in the {{PLACEHOLDERS}}, send to AI.

---

## Table of Contents

1. [Feature Implementation Templates](#feature-implementation-templates)
2. [Debugging Templates](#debugging-templates)
3. [Refactoring Templates](#refactoring-templates)
4. [Testing Templates](#testing-templates)
5. [Documentation Templates](#documentation-templates)
6. [Code Review Templates](#code-review-templates)
7. [Performance Templates](#performance-templates)
8. [Security Templates](#security-templates)

---

## Feature Implementation Templates

### Template 1: Simple Feature Addition

```
Implement {{FEATURE_NAME}} in {{FILE_PATH}}.

Requirements:
- {{REQUIREMENT_1}}
- {{REQUIREMENT_2}}
- {{REQUIREMENT_3}}

Follow the pattern used in {{REFERENCE_FEATURE}} in {{REFERENCE_FILE}}.

Success criteria:
- {{CRITERION_1}}
- {{CRITERION_2}}
- {{CRITERION_3}}
```

**Example filled in:**
```
Implement email validation in src/components/RegisterForm.tsx.

Requirements:
- Validate on blur (not on every keystroke)
- Show error message below input field
- Check format using standard email regex
- Required field (empty = error)

Follow the pattern used for password validation in src/components/RegisterForm.tsx (lines 45-67).

Success criteria:
- Invalid email → red border + error message
- Valid email → green border, no error
- Empty field on blur → error message 'Email is required'
```

---

### Template 2: API Endpoint Creation

```
Create {{HTTP_METHOD}} {{ENDPOINT_PATH}} endpoint.

FILE: {{FILE_PATH}}

Request:
{{REQUEST_SCHEMA}}

Response:
Success ({{SUCCESS_STATUS_CODE}}): {{SUCCESS_RESPONSE_SCHEMA}}
Error ({{ERROR_STATUS_CODE}}): {{ERROR_RESPONSE_SCHEMA}}

Business logic:
- {{LOGIC_1}}
- {{LOGIC_2}}

Validation:
- {{VALIDATION_1}}
- {{VALIDATION_2}}

Follow the pattern from {{REFERENCE_ENDPOINT}} in {{REFERENCE_FILE}}.

Include:
- Input validation (express-validator)
- Error handling (try-catch)
- {{ADDITIONAL_MIDDLEWARE}} middleware
```

**Example filled in:**
```
Create POST /api/posts endpoint.

FILE: src/api/posts.ts

Request:
{
  title: string (required, max 200 chars),
  content: string (required, max 5000 chars),
  tags: string[] (optional, max 5 tags)
}

Response:
Success (201): { data: { id, title, content, tags, authorId, createdAt } }
Error (400): { error: { code: 'VALIDATION_ERROR', message: string } }

Business logic:
- Associate post with authenticated user (req.user.id)
- Sanitize HTML in content
- Normalize tags (lowercase, trim)

Validation:
- Title required, max length
- Content required, max length
- Tags array, max 5 items

Follow the pattern from POST /api/users in src/api/users.ts.

Include:
- Input validation (express-validator)
- Error handling (try-catch)
- Authentication middleware (requireAuth)
```

---

### Template 3: React Component Creation

```
Create {{COMPONENT_NAME}} component.

FILE: {{FILE_PATH}}

Props:
{{PROPS_INTERFACE}}

Behavior:
- {{BEHAVIOR_1}}
- {{BEHAVIOR_2}}
- {{BEHAVIOR_3}}

Styling:
- {{STYLING_APPROACH}}
- {{SPECIFIC_STYLES}}

State management (if needed):
- {{STATE_DESCRIPTION}}

Follow {{PATTERN_DESCRIPTION}} pattern from {{REFERENCE_COMPONENT}}.

Use existing components:
- {{EXISTING_COMPONENT_1}}
- {{EXISTING_COMPONENT_2}}
```

**Example filled in:**
```
Create UserCard component.

FILE: src/components/UserCard.tsx

Props:
{
  user: {
    id: string,
    name: string,
    email: string,
    avatar?: string,
    role: 'user' | 'admin'
  },
  onClick?: (userId: string) => void,
  showRole?: boolean
}

Behavior:
- Display user avatar (or default if not provided)
- Display name and email
- Optionally display role badge
- Click card → call onClick with userId
- Hover effect (scale slightly)

Styling:
- Tailwind CSS utility classes
- Card: white background, rounded, shadow on hover
- Avatar: circular, 48x48px
- Role badge: small pill, blue for admin, gray for user

Follow card component pattern from PostCard (src/components/PostCard.tsx).

Use existing components:
- Avatar (src/components/common/Avatar.tsx)
- Badge (src/components/common/Badge.tsx)
```

---

## Debugging Templates

### Template 4: Runtime Error Debugging

```
Fix {{ERROR_TYPE}} in {{FILE_PATH}}.

ERROR MESSAGE:
{{ERROR_MESSAGE}}

STACK TRACE:
{{RELEVANT_STACK_TRACE}}

CONTEXT:
- File: {{FILE}}:{{LINE}}
- Action: {{USER_ACTION}}
- Environment: {{ENVIRONMENT}}
- Started happening: {{WHEN}}
- {{ADDITIONAL_CONTEXT}}

EXPECTED vs ACTUAL:
- Expected: {{EXPECTED_BEHAVIOR}}
- Actual: {{ACTUAL_BEHAVIOR}}

ALREADY TRIED:
- {{ATTEMPT_1}} → {{RESULT_1}}
- {{ATTEMPT_2}} → {{RESULT_2}}

RELEVANT CODE:
{{CODE_SNIPPET}}

{{HYPOTHESIS}} (if you have one)
```

**Example filled in:**
```
Fix null pointer error in login flow.

ERROR MESSAGE:
TypeError: Cannot read property 'id' of undefined

STACK TRACE:
  at handleLogin (src/api/auth.ts:45:31)
  at validateAndLogin (src/api/auth.ts:23:12)

CONTEXT:
- File: src/api/auth.ts:45
- Action: User submitted login form
- Environment: Development
- Started happening: After adding email verification yesterday
- Only affects unverified users

EXPECTED vs ACTUAL:
- Expected: Return 401 for unverified users
- Actual: 500 error crash

ALREADY TRIED:
- Added console.log → user is undefined
- Checked User.findByEmail → returns null for unverified

RELEVANT CODE:
```typescript
async function handleLogin(req, res) {
  const { email, password } = req.body;
  const user = await User.findByEmail(email);
  const isValid = await bcrypt.compare(password, user.password);
  if (!isValid) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }
  const token = jwt.sign({ id: user.id }, SECRET); // LINE 45 ERROR
  return res.json({ token });
}
```

HYPOTHESIS: User.findByEmail returns null for unverified users, but we're not checking before accessing user.id.
```

---

### Template 5: Logic Bug Debugging

```
Fix incorrect {{BEHAVIOR}} in {{FUNCTION/COMPONENT}}.

BUG DESCRIPTION:
{{WHAT'S_WRONG}}

EXPECTED BEHAVIOR:
{{DETAILED_EXPECTED}}

ACTUAL BEHAVIOR:
{{DETAILED_ACTUAL}}

TEST CASE:
Input: {{INPUT}}
Expected output: {{EXPECTED_OUTPUT}}
Actual output: {{ACTUAL_OUTPUT}}

CODE ({{FILE}}):
{{CODE_SNIPPET}}

ANALYSIS:
{{YOUR_ANALYSIS}} (if you've identified the issue)
```

---

## Refactoring Templates

### Template 6: Component Refactoring

```
Refactor {{COMPONENT_NAME}} from {{OLD_APPROACH}} to {{NEW_APPROACH}}.

FILE: {{FILE_PATH}}

CURRENT PROBLEMS:
- {{PROBLEM_1}}
- {{PROBLEM_2}}

DESIRED STATE:
- {{GOAL_1}}
- {{GOAL_2}}

MUST PRESERVE:
- {{PRESERVATION_1}} (critical - reason: {{REASON}})
- {{PRESERVATION_2}}

CHANGES ALLOWED:
- {{ALLOWED_CHANGE_1}}
- {{ALLOWED_CHANGE_2}}

CURRENT CODE:
{{CODE_SNIPPET}}

SUCCESS CRITERIA:
- Tests still pass
- {{SPECIFIC_REQUIREMENT_1}}
- {{SPECIFIC_REQUIREMENT_2}}
```

**Example filled in:**
```
Refactor UserProfile from class component to functional component with hooks.

FILE: src/components/UserProfile.tsx

CURRENT PROBLEMS:
- Verbose (200 lines)
- Lifecycle methods scattered
- Hard to extract reusable logic

DESIRED STATE:
- Functional component
- Consolidated useEffect hooks
- Custom hooks for reusable logic
- ~100 lines

MUST PRESERVE:
- All functionality (critical - other components depend on it)
- Props interface unchanged
- Subscription cleanup on unmount (critical - prevents memory leaks)

CHANGES ALLOWED:
- Convert to functional component
- Use hooks (useState, useEffect)
- Extract custom hooks

CURRENT CODE:
[class component code]

SUCCESS CRITERIA:
- Tests pass without modification
- Subscription cleanup verified
- Code < 100 lines
```

---

### Template 7: Architecture Refactoring

```
Refactor {{SYSTEM}} architecture from {{OLD_PATTERN}} to {{NEW_PATTERN}}.

PHASE {{N}} of {{TOTAL}}: {{PHASE_NAME}}

RATIONALE:
{{WHY_REFACTORING}}

SCOPE (this phase):
Files affected:
- {{FILE_1}} ({{ACTION}})
- {{FILE_2}} ({{ACTION}})

Files NOT changing:
- {{UNCHANGED_FILE_1}}
- {{UNCHANGED_FILE_2}}

REQUIREMENTS:
{{DETAILED_PHASE_REQUIREMENTS}}

BACKWARD COMPATIBILITY:
{{HOW_TO_MAINTAIN}}

TESTING:
- {{TEST_REQUIREMENT_1}}
- {{TEST_REQUIREMENT_2}}
```

---

## Testing Templates

### Template 8: Unit Test Generation

```
Write comprehensive tests for {{FUNCTION/CLASS/COMPONENT}}.

CODE TO TEST ({{FILE}}):
{{CODE_SNIPPET}}

TEST FILE: {{TEST_FILE_PATH}}
TEST FRAMEWORK: {{FRAMEWORK}}

SCENARIOS TO COVER:

Happy path:
- [ ] {{HAPPY_SCENARIO_1}}
- [ ] {{HAPPY_SCENARIO_2}}

Error cases:
- [ ] {{ERROR_SCENARIO_1}}
- [ ] {{ERROR_SCENARIO_2}}

Edge cases:
- [ ] {{EDGE_SCENARIO_1}}
- [ ] {{EDGE_SCENARIO_2}}

{{ADDITIONAL_CATEGORY}}:
- [ ] {{ADDITIONAL_SCENARIO_1}}

MOCKING:
- Mock {{DEPENDENCY_1}}
- Mock {{DEPENDENCY_2}}

TEST STRUCTURE:
```typescript
describe('{{NAME}}', () => {
  describe('{{FUNCTIONALITY}}', () => {
    it('{{TEST_CASE}}', () => {});
  });
});
```

Please write complete, runnable tests.
```

---

### Template 9: Integration Test

```
Write integration test for {{FEATURE}}.

FEATURE DESCRIPTION:
{{DESCRIPTION}}

TEST FILE: {{TEST_FILE_PATH}}
TEST FRAMEWORK: {{FRAMEWORK}}

SETUP:
- {{SETUP_REQUIREMENT_1}}
- {{SETUP_REQUIREMENT_2}}

TEST FLOW:
1. {{STEP_1}}
2. {{STEP_2}}
3. {{STEP_3}}

ASSERTIONS:
- {{ASSERTION_1}}
- {{ASSERTION_2}}

CLEANUP:
- {{CLEANUP_1}}
- {{CLEANUP_2}}
```

---

## Documentation Templates

### Template 10: Function/API Documentation

```
Generate {{DOC_TYPE}} documentation for {{FUNCTION/API}}.

CODE:
{{CODE_SNIPPET}}

DOCUMENTATION FORMAT: {{FORMAT}}

INCLUDE:
- {{ELEMENT_1}}
- {{ELEMENT_2}}
- {{ELEMENT_3}}

EXAMPLES:
Provide {{N}} usage examples showing:
- {{EXAMPLE_SCENARIO_1}}
- {{EXAMPLE_SCENARIO_2}}

{{ADDITIONAL_REQUIREMENTS}}
```

**Example filled in:**
```
Generate JSDoc documentation for calculateDiscount function.

CODE:
```typescript
function calculateDiscount(subtotal: number, discountCode?: string) {
  if (!discountCode) return 0;
  const discount = DISCOUNTS[discountCode];
  if (!discount) throw new Error('Invalid discount code');
  return subtotal * (discount.percentage / 100);
}
```

DOCUMENTATION FORMAT: JSDoc

INCLUDE:
- Function description
- @param documentation for each parameter
- @returns documentation
- @throws documentation (for invalid code)
- @example with 3 usage examples

EXAMPLES:
Provide 3 usage examples showing:
- No discount code
- Valid discount code
- Invalid discount code (error case)
```

---

### Template 11: README/Guide Creation

```
Create {{DOC_TYPE}} for {{SYSTEM/FEATURE}}.

FILE: {{FILE_PATH}}

TARGET AUDIENCE: {{AUDIENCE}}

SECTIONS TO INCLUDE:
1. {{SECTION_1}}
2. {{SECTION_2}}
3. {{SECTION_3}}

TONE: {{TONE}} (e.g., technical, beginner-friendly, tutorial-style)

INCLUDE:
- {{REQUIREMENT_1}}
- {{REQUIREMENT_2}}

FORMAT: Markdown

{{ADDITIONAL_CONTEXT}}
```

---

## Code Review Templates

### Template 12: Pull Request Review

```
Review PR #{{NUMBER}}: {{TITLE}}

FILES CHANGED:
- {{FILE_1}} ({{CHANGES}})
- {{FILE_2}} ({{CHANGES}})

REVIEW CRITERIA:

{{CATEGORY_1}} (priority: {{PRIORITY}}):
- [ ] {{CRITERION_1}}
- [ ] {{CRITERION_2}}

{{CATEGORY_2}}:
- [ ] {{CRITERION_3}}
- [ ] {{CRITERION_4}}

CONTEXT:
{{FEATURE_DESCRIPTION}}

SPECIFIC CONCERNS:
1. {{CONCERN_1}}
2. {{CONCERN_2}}

OUTPUT FORMAT:
1. Critical Issues (must fix before merge)
2. {{CATEGORY_1}} Issues
3. {{CATEGORY_2}} Issues
4. Test Coverage Gaps
5. Overall Assessment (approve/request changes)
```

---

### Template 13: Security Audit

```
Security audit of {{SYSTEM/FEATURE}}.

SCOPE:
- {{FILE_1}}
- {{FILE_2}}

AUDIT FOR:

{{SECURITY_CATEGORY_1}}:
- [ ] {{CHECK_1}}
- [ ] {{CHECK_2}}

{{SECURITY_CATEGORY_2}}:
- [ ] {{CHECK_3}}
- [ ] {{CHECK_4}}

CURRENT IMPLEMENTATION:
{{CODE_OR_DESCRIPTION}}

Please provide:
1. Critical vulnerabilities (must fix immediately)
2. Medium-priority issues
3. Best practice improvements
4. Specific code changes needed

For each issue:
- What the vulnerability is
- How it can be exploited
- How to fix it
- Code example of fix
```

---

## Performance Templates

### Template 14: Performance Optimization

```
Optimize {{SYSTEM/FEATURE}} performance.

PROBLEM:
{{CURRENT_PERFORMANCE_ISSUE}}

TARGET:
Current: {{CURRENT_METRIC}}
Target: {{TARGET_METRIC}}

PERFORMANCE DATA:
- {{MEASUREMENT_1}}: {{VALUE}}
- {{MEASUREMENT_2}}: {{VALUE}}

FILES:
- {{FILE_1}}
- {{FILE_2}}

CURRENT IMPLEMENTATION:
{{CODE_OR_DESCRIPTION}}

CONSTRAINTS:
- {{CONSTRAINT_1}}
- {{CONSTRAINT_2}}

OPTIMIZATION IDEAS:
- {{IDEA_1}}
- {{IDEA_2}}

What's the best approach? Please implement the most effective solution.
```

---

### Template 15: Performance Analysis

```
Analyze performance of {{SYSTEM/FEATURE}}.

CONTEXT:
{{DESCRIPTION}}

CURRENT METRICS:
- {{METRIC_1}}: {{VALUE}}
- {{METRIC_2}}: {{VALUE}}

FILES TO ANALYZE:
- {{FILE_1}}
- {{FILE_2}}

FOCUS ON:
- {{AREA_1}}
- {{AREA_2}}

Please identify:
1. Performance bottlenecks
2. Improvement opportunities
3. Estimated impact of each optimization
4. Recommended implementation order
```

---

## Security Templates

### Template 16: Security Fix

```
Fix security vulnerability in {{SYSTEM/FEATURE}}.

VULNERABILITY TYPE: {{TYPE}}
SEVERITY: {{SEVERITY}}

ISSUE:
{{VULNERABILITY_DESCRIPTION}}

EXPLOIT SCENARIO:
{{HOW_IT_CAN_BE_EXPLOITED}}

AFFECTED CODE ({{FILE}}):
{{CODE_SNIPPET}}

FIX REQUIREMENTS:
- {{REQUIREMENT_1}}
- {{REQUIREMENT_2}}

TESTING:
- {{TEST_REQUIREMENT_1}}
- {{TEST_REQUIREMENT_2}}

Please provide:
1. Fixed code
2. Explanation of fix
3. Test cases to verify fix
```

---

### Template 17: Input Validation

```
Add comprehensive input validation to {{ENDPOINT/FUNCTION}}.

CURRENT CODE ({{FILE}}):
{{CODE_SNIPPET}}

INPUTS TO VALIDATE:
- {{INPUT_1}}: {{TYPE}} - {{VALIDATION_RULES}}
- {{INPUT_2}}: {{TYPE}} - {{VALIDATION_RULES}}
- {{INPUT_3}}: {{TYPE}} - {{VALIDATION_RULES}}

VALIDATION LIBRARY: {{LIBRARY}}

ERROR HANDLING:
- Invalid input → return {{ERROR_RESPONSE}}
- Validation error format: {{FORMAT}}

SECURITY CONSIDERATIONS:
- {{CONSIDERATION_1}}
- {{CONSIDERATION_2}}
```

---

## Quick Reference: Template Selection

```
┌──────────────────────────────────────────┐
│  Choose Your Template                    │
├──────────────────────────────────────────┤
│  New feature        → Template 1, 2, 3   │
│  Bug fix            → Template 4, 5      │
│  Code improvement   → Template 6, 7      │
│  Add tests          → Template 8, 9      │
│  Write docs         → Template 10, 11    │
│  Review code        → Template 12, 13    │
│  Speed up code      → Template 14, 15    │
│  Security fix       → Template 16, 17    │
└──────────────────────────────────────────┘
```

---

## Usage Tips

### 1. Customize Templates

**Don't use templates blindly:**
- Remove irrelevant sections
- Add project-specific requirements
- Adjust to your code style
- Reference your actual files/patterns

### 2. Save Your Own Templates

**Create project-specific templates:**

```
/docs/templates/prompts/
├── feature-api-endpoint.md
├── feature-react-component.md
├── debug-backend.md
├── refactor-component.md
└── test-integration.md
```

Each tailored to your project.

### 3. Template Variables

**Common placeholders:**

```
{{FILE_PATH}} → src/components/UserCard.tsx
{{COMPONENT_NAME}} → UserCard
{{HTTP_METHOD}} → POST
{{ENDPOINT_PATH}} → /api/users
{{REQUIREMENT_N}} → Specific requirement description
{{CRITERION_N}} → Success criterion
{{ERROR_TYPE}} → NullPointerError, ValidationError, etc.
{{REFERENCE_FILE}} → src/components/ExampleComponent.tsx
```

### 4. Combining Templates

**Mix elements from multiple templates:**

Example: Feature + Testing
```
[Use Template 3 for component creation]
[Then use Template 8 for test generation]
```

Result: Component + comprehensive tests in two prompts.

---

## Template Maintenance

### Update Templates When:

- ✅ You discover a better prompting pattern
- ✅ Project conventions change
- ✅ New tools/libraries adopted
- ✅ Repeated prompts could be templated
- ✅ Template produces poor results

### Template Quality Checklist:

- [ ] Has clear placeholders ({{VARIABLE_NAME}})
- [ ] Includes all necessary context
- [ ] References project patterns
- [ ] Defines success criteria
- [ ] Specifies constraints
- [ ] Provides example usage

---

## Next Steps

1. **Try a template** → Copy one, fill in placeholders, test it
2. **Measure results** → How many iterations needed? Quality of output?
3. **Refine template** → Improve based on results
4. **Create custom templates** → For your common tasks
5. **Share with team** → Consistent prompting across team

---

**Related Documentation:**
- [Foundations](./foundations.md) → Core prompting principles
- [Task-Specific Patterns](./task-specific-patterns.md) → Detailed examples
- [Advanced Techniques](./advanced-techniques.md) → Expert strategies
- [Troubleshooting Guide](../troubleshooting/README.md) → When prompts fail

**Back to:** [Prompting Guide Home](./README.md)
