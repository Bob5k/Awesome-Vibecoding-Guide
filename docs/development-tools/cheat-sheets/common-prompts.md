# Common AI Prompts Cheat Sheet

Quick-copy prompt templates for frequent development tasks. Customize placeholders in [brackets].

## Feature Implementation

### Basic Feature Prompt
```
Create a [feature name] that [description of functionality].

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Technical details:
- Use [technology/framework]
- Follow [pattern/architecture]
- Include [specific implementation detail]

Please provide:
1. Component code
2. Any required types/interfaces
3. Example usage
4. Brief explanation of approach
```

**Example:**
```
Create a contact form component that sends emails via Cloudflare Email Worker.

Requirements:
- Name, email, message fields
- Client-side validation
- Rate limiting (1 submission per minute per IP)
- Success/error feedback

Technical details:
- Use Astro components
- Follow accessibility best practices
- Include proper error handling

Please provide:
1. Component code
2. TypeScript types
3. Example usage
4. Brief explanation of approach
```

### User Authentication Feature
```
Implement user authentication for [application type].

Features needed:
- User registration (email + password)
- Login/logout
- Password hashing (bcrypt)
- Session management
- Protected routes

Tech stack:
- [Framework: Astro/Next/etc]
- [Database: D1/PostgreSQL/etc]
- [Session storage: KV/cookies/etc]

Security requirements:
- Secure password hashing
- CSRF protection
- Rate limiting on login attempts
- Secure session management

Please provide:
1. Authentication logic
2. Database schema
3. Protected route example
4. Security best practices followed
```

### CRUD Operations
```
Create CRUD operations for [entity name].

Entity fields:
- [field1]: [type]
- [field2]: [type]
- [field3]: [type]

Operations needed:
- Create [entity]
- Read/list [entities]
- Update [entity]
- Delete [entity]

Tech stack:
- Database: [D1/PostgreSQL/etc]
- API: [REST/GraphQL]
- Framework: [Astro/Express/etc]

Please include:
1. Database schema/migration
2. API endpoints
3. Validation logic
4. Error handling
5. Example usage
```

### API Integration
```
Integrate [API name] API into [application].

What I need:
- Fetch [data type] from API
- Handle authentication ([auth type])
- Cache responses ([caching strategy])
- Handle errors gracefully

API details:
- Endpoint: [URL]
- Auth method: [API key/OAuth/etc]
- Rate limits: [limit details]

Please provide:
1. API client code
2. Type definitions for responses
3. Error handling
4. Caching implementation
5. Usage examples
```

## Debugging

### Debug Specific Error
```
I'm getting this error:

[Paste exact error message]

Context:
- Code: [paste relevant code]
- What I was doing: [description]
- What I expected: [expected behavior]
- What happened: [actual behavior]

Environment:
- Framework: [Astro/Next/etc]
- Browser: [if relevant]
- Node version: [if relevant]

Please:
1. Explain what's causing the error
2. Provide a fix
3. Explain why the fix works
```

### Debug Performance Issue
```
My [page/component/function] is running slowly.

Performance metrics:
- Current: [metric and value]
- Target: [desired metric]

Code:
[Paste relevant code]

What I've tried:
- [Attempt 1]
- [Attempt 2]

Please:
1. Identify performance bottlenecks
2. Suggest optimizations
3. Show optimized code
4. Explain performance improvements
```

### Debug Unexpected Behavior
```
My [feature] isn't working as expected.

Expected behavior:
[Describe what should happen]

Actual behavior:
[Describe what's happening]

Code:
[Paste relevant code]

Steps to reproduce:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Please:
1. Identify the issue
2. Explain why it's happening
3. Provide a fix
4. Suggest tests to prevent regression
```

### Debug Console Error
```
I see this error in the console:

[Paste console error]

Browser console shows:
[Paste stack trace if available]

What I'm doing when it happens:
[Description]

Relevant code:
[Paste code]

Please help me:
1. Understand what's causing this
2. Fix the error
3. Prevent similar errors
```

## Refactoring

### Code Cleanup
```
Refactor this code to improve [quality aspect]:

[Paste code]

Goals:
- Improve readability
- Reduce complexity
- Follow best practices
- Maintain same functionality

Please provide:
1. Refactored code
2. Explanation of changes
3. Why the new version is better
```

### Extract Reusable Component
```
This code appears in multiple places:

[Paste repeated code]

Please:
1. Extract a reusable component/function
2. Show how to use it in both locations
3. Include proper TypeScript types
4. Suggest a good name
```

### Performance Optimization
```
Optimize this code for performance:

[Paste code]

Current issues:
- [Issue 1: e.g., "Renders too often"]
- [Issue 2: e.g., "Large bundle size"]
- [Issue 3: e.g., "Slow on mobile"]

Please provide:
1. Optimized code
2. Explanation of optimizations
3. Performance comparison
4. Trade-offs (if any)
```

### Modernize Legacy Code
```
Modernize this code using current best practices:

[Paste legacy code]

Current issues:
- [Issue 1: e.g., "Uses var instead of const/let"]
- [Issue 2: e.g., "Callbacks instead of async/await"]
- [Issue 3: e.g., "Old API usage"]

Target:
- Use modern JavaScript/TypeScript
- Follow current best practices
- Maintain backward compatibility [if needed]

Please provide:
1. Modernized code
2. Explanation of changes
3. Migration notes
```

## Testing

### Write Unit Tests
```
Write unit tests for this code:

[Paste code to test]

Test framework: [Jest/Vitest/etc]

Please test:
- Happy path (expected inputs)
- Edge cases
- Error conditions
- Boundary conditions

Please provide:
1. Complete test file
2. Test descriptions
3. Any test utilities/helpers needed
4. Coverage report interpretation
```

### Write Integration Tests
```
Write integration tests for this feature:

[Description of feature]

Components involved:
- [Component 1]
- [Component 2]
- [Component 3]

Test framework: [Playwright/Cypress/etc]

Please test:
- User workflows
- Error scenarios
- Edge cases
- Accessibility

Please provide:
1. Test file
2. Test setup instructions
3. Any fixtures/mocks needed
```

### Test Debugging
```
This test is failing:

[Paste test code]

Error:
[Paste error message]

Code being tested:
[Paste relevant code]

Please:
1. Identify why test is failing
2. Fix the test (or the code if that's the issue)
3. Explain the fix
```

## Documentation

### Write Documentation
```
Write documentation for this code:

[Paste code]

Audience: [Developers/end-users/team members]

Please include:
- Overview of what it does
- How to use it
- Parameters/props explanation
- Return values
- Examples
- Common pitfalls
- Related functions/components
```

### API Documentation
```
Document this API endpoint:

[Paste endpoint code]

Please create:
- Endpoint description
- HTTP method
- URL path
- Request parameters
- Request body (if applicable)
- Response format
- Status codes
- Error responses
- Example requests
- Example responses
```

### README Template
```
Create a README.md for this project:

Project name: [name]
Description: [brief description]
Tech stack: [technologies used]

Please include:
- Project overview
- Features
- Prerequisites
- Installation instructions
- Usage examples
- Configuration
- Deployment
- Contributing guidelines
- License
```

## Code Review

### Review My Code
```
Please review this code:

[Paste code]

Focus on:
- Code quality
- Best practices
- Potential bugs
- Performance
- Security
- Accessibility (if UI)

Please provide:
1. Specific issues found
2. Severity (critical/major/minor)
3. Suggested fixes
4. General feedback
```

### Security Review
```
Review this code for security vulnerabilities:

[Paste code]

Context:
- Purpose: [what it does]
- User input: [what users can input]
- Data handling: [how data is processed]

Please check for:
- SQL injection
- XSS vulnerabilities
- CSRF issues
- Authentication/authorization issues
- Data exposure
- Input validation
- Sensitive data handling

Provide:
1. Vulnerabilities found
2. Severity level
3. Exploit scenarios
4. Fixes
```

### Accessibility Review
```
Review this component for accessibility:

[Paste component code]

Please check:
- WCAG 2.1 Level AA compliance
- Keyboard navigation
- Screen reader support
- Color contrast
- ARIA attributes
- Focus management
- Form accessibility

Provide:
1. Issues found
2. WCAG criteria violated
3. Specific fixes
4. Testing recommendations
```

## General

### Explain Code
```
Explain how this code works:

[Paste code]

Please explain:
- What it does (high level)
- How it works (step by step)
- Why it's written this way
- Any gotchas or edge cases
- How to modify it if needed

Audience level: [Beginner/Intermediate/Advanced]
```

### Best Practices
```
What are the best practices for [topic]?

Context:
- Tech stack: [technologies]
- Use case: [description]
- Team size: [if relevant]

Please cover:
- Industry standards
- Common pitfalls to avoid
- Tools and resources
- Code examples
- When to deviate from best practices
```

### Architecture Decision
```
Help me decide between [Option A] and [Option B] for [use case].

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Constraints:
- [Constraint 1: e.g., "Budget: $0-20/mo"]
- [Constraint 2: e.g., "Team size: 2"]
- [Constraint 3: e.g., "Timeline: 2 weeks"]

Please provide:
1. Comparison of both options
2. Pros and cons of each
3. Recommendation with reasoning
4. Implementation considerations
```

### Migration Strategy
```
Help me migrate from [Old Technology] to [New Technology].

Current setup:
- [Current architecture]
- [Current tech stack]
- [Current data]

Target:
- [New architecture]
- [New tech stack]
- [Requirements]

Constraints:
- Zero downtime required: [Yes/No]
- Data migration needed: [Yes/No]
- Timeline: [duration]

Please provide:
1. Step-by-step migration plan
2. Risks and mitigations
3. Testing strategy
4. Rollback plan
5. Timeline estimate
```

## Astro-Specific

### Create Astro Component
```
Create an Astro component for [purpose].

Props:
- [prop1]: [type] - [description]
- [prop2]: [type] - [description]

Features:
- [Feature 1]
- [Feature 2]
- Responsive design
- Accessible (WCAG 2.1 AA)

Please provide:
1. Component code (.astro file)
2. TypeScript interface for props
3. CSS/Tailwind styles
4. Usage example
```

### Astro API Route
```
Create an Astro API route for [purpose].

Endpoint: /api/[route]
Method: [GET/POST/etc]

Request:
- [Request details]

Response:
- [Response format]

Features needed:
- Validation
- Error handling
- Rate limiting (if needed)
- Authentication (if needed)

Please provide:
1. API route code
2. TypeScript types
3. Error responses
4. Usage example
```

### Astro with D1
```
Create an Astro page that uses D1 database.

Page purpose: [description]

Database operations:
- [Operation 1: e.g., "Fetch all posts"]
- [Operation 2: e.g., "Filter by category"]

Please provide:
1. Astro page component
2. D1 query code
3. Type definitions
4. Error handling
5. Example output
```

## Prompt Enhancement Tips

### Make Prompts More Effective

**Be specific:**
```
❌ "Create a form"
✅ "Create a contact form with name, email, message fields, client-side validation, and accessible error messages"
```

**Provide context:**
```
❌ "Fix this bug"
✅ "Fix this bug in my Astro site's contact form. Error occurs when submitting without filling required fields. Expected: show error message. Actual: form submits anyway."
```

**Include technical details:**
```
❌ "Add authentication"
✅ "Add email/password authentication using Astro server endpoints, D1 database for user storage, bcrypt for password hashing, and httpOnly cookies for sessions"
```

**Specify output format:**
```
❌ "Help me with this"
✅ "Please provide: 1) The complete fixed code, 2) Explanation of what was wrong, 3) Why your fix works, 4) How to prevent this in future"
```

**Break down complex requests:**
```
❌ "Build a complete user dashboard with auth, profiles, and settings"
✅ Break into steps:
  1. "Create user authentication system"
  2. "Create user profile page"
  3. "Create settings page"
  4. "Integrate all three components"
```

## Saving Your Own Prompts

Create a prompts file in your project:

```markdown
# My Project Prompts

## Add New Feature
Create a [type] feature for the [project area].
Requirements:
- Uses D1 database
- Follows existing code patterns in src/[directory]
- Includes TypeScript types
- Has error handling

## Debug Performance
This [component/function] is slow:
[code]
Expected: [metric]
Actual: [metric]
Please optimize.

## Review Code
Review this code for:
- Project-specific patterns
- Our team's style guide
- Cloudflare-specific optimizations
[code]
```

---

**Remember:** Good prompts are:
- Specific (exactly what you need)
- Contextual (relevant background)
- Complete (all necessary information)
- Clear (easy to understand)
- Actionable (AI can act on it)
