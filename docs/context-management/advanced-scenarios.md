# Advanced Context Management Scenarios

## Overview

This guide covers complex context management patterns for specialized development scenarios. These strategies help maintain effective AI assistance in challenging project structures.

## Monorepo Context Management

### Challenge

Monorepos contain multiple packages/apps sharing code. Loading entire monorepo context overwhelms AI and slows responses.

### Strategy: Isolated Package Context

**Structure example:**
```
monorepo/
├── packages/
│   ├── web-app/
│   ├── mobile-app/
│   ├── shared-ui/
│   └── shared-utils/
└── package.json
```

**Package-specific .cursorrules:**

```markdown
# packages/web-app/.cursorrules

# Web App Context

This is the web application package in our monorepo.

## This Package
- Location: /packages/web-app
- Purpose: Customer-facing web application
- Tech: Astro, React islands, Tailwind

## Dependencies
- Shared UI: /packages/shared-ui (component library)
- Shared Utils: /packages/shared-utils (business logic)

## When working here:
1. Import shared components from @repo/ui
2. Import utilities from @repo/utils
3. Never duplicate code from shared packages
4. Follow web-specific patterns (SSG, islands)

## Related packages:
- Mobile app uses similar patterns but different framework
- Coordinate API changes with mobile team

## Common tasks:
- Add new pages (src/pages/)
- Create island components (src/components/)
- Integrate shared components

## Do NOT load:
- Mobile app code (/packages/mobile-app)
- Other packages unless explicitly needed
```

### Shared Dependencies Strategy

**In shared package (.cursorrules):**
```markdown
# packages/shared-ui/.cursorrules

# Shared UI Component Library

This package is used by both web and mobile apps.

## Usage
Apps import as: `import { Button } from '@repo/ui'`

## Guidelines
- Components must work in both web and mobile contexts
- No framework-specific code (pure React)
- Fully typed (TypeScript strict mode)
- Each component has Storybook story
- Accessibility (WCAG 2.1 AA)

## Breaking changes:
- Always major version bump
- Document migration in CHANGELOG
- Notify web and mobile teams

## Testing:
- Unit tests required
- Visual regression tests in Storybook
- Test in both web and mobile apps before releasing
```

### Workspace-Level Context

**Root .cursorrules (monorepo guidelines):**
```markdown
# Monorepo Guidelines

## Structure
- /packages/* - Individual packages
- Each package has own package.json, .cursorrules
- Shared config in /config

## Working in monorepo:
1. Always work in specific package directory
2. Don't load entire monorepo context
3. Reference shared packages by import path
4. Coordinate changes across packages

## Package types:
- Applications (web-app, mobile-app)
- Libraries (shared-ui, shared-utils)
- Tools (build-tools, dev-tools)

## Cross-package changes:
1. Update shared package first
2. Version bump and publish
3. Update consuming packages
4. Test integration

## Commands:
- `npm run dev:web` - Run web app
- `npm run dev:mobile` - Run mobile app
- `npm run build` - Build all packages
- `npm run test` - Test all packages
```

### Progressive Context Loading

When you need cross-package context:

1. **Start narrow:**
   ```
   I'm working in /packages/web-app.
   Focus only on this package for now.
   ```

2. **Add dependencies as needed:**
   ```
   Now I need context from /packages/shared-ui/src/Button.tsx
   Load only this file.
   ```

3. **Expand selectively:**
   ```
   Also load /packages/shared-utils/src/formatDate.ts
   ```

**Never:**
```
Load entire monorepo
↓ Overwhelms context, slow responses, worse quality
```

## Microservices Context Strategy

### Challenge

Multiple services with different languages, frameworks, and responsibilities. AI needs context about service boundaries and contracts.

### Per-Service Context

**Service-specific .cursorrules:**
```markdown
# services/user-service/.cursorrules

# User Service

## Responsibilities
- User CRUD operations
- Authentication
- User profile management

## Tech Stack
- Node.js + Express
- PostgreSQL
- Redis (caching)

## API Endpoints
- POST /api/users - Create user
- GET /api/users/:id - Get user
- PUT /api/users/:id - Update user
- DELETE /api/users/:id - Delete user
- POST /api/auth/login - Login
- POST /api/auth/logout - Logout

## Depends On
- None (root service)

## Depended On By
- Order service (user info)
- Notification service (user preferences)

## Database Schema
- users table (id, email, password_hash, created_at, updated_at)
- sessions table (id, user_id, token, expires_at)

## When working here:
- Don't load other services
- Use API contracts for inter-service communication
- Run tests before committing
- Update API docs if changing endpoints

## Common tasks:
- Add new endpoints
- Update user schema
- Improve authentication
```

### API Contract Documentation

**Maintain API contracts separately:**

```typescript
// shared/contracts/user-service.ts

/**
 * User Service API Contract
 *
 * Other services should reference this for user service integration.
 */

export interface User {
  id: string;
  email: string;
  name: string;
  created_at: string;
}

export interface UserServiceAPI {
  // Get user by ID
  'GET /api/users/:id': {
    params: { id: string };
    response: { user: User } | { error: string };
    status: 200 | 404 | 500;
  };

  // Create user
  'POST /api/users': {
    body: { email: string; name: string; password: string };
    response: { user: User; token: string } | { error: string };
    status: 201 | 400 | 500;
  };
}
```

Reference in dependent services:

```markdown
# services/order-service/.cursorrules

## Depends On: User Service
- Contract: /shared/contracts/user-service.ts
- Fetches user info when creating orders
- Validates user IDs exist before processing
```

### Debugging Across Services

When debugging requires multiple services:

**Explicit context boundary:**
```
I'm debugging an issue in order-service that involves user-service.

Primary context: /services/order-service
Secondary context: User service API contract only (/shared/contracts/user-service.ts)

DO NOT load user service implementation.
Focus on how order-service calls user service and handles responses.
```

**If you need implementation details:**
```
Now load specific file: /services/user-service/src/controllers/userController.ts
Just this file, not entire user service.
```

## Long-Running Projects (6+ Months)

### Challenge

Context decays over time. Initial decisions forgotten, patterns drift, documentation outdates.

### Strategy: Living Documentation

**Architecture Decision Records (ADRs):**

```markdown
# docs/adr/0001-use-astro-for-frontend.md

# Use Astro for Frontend Framework

Date: 2024-01-15
Status: Accepted

## Context
We need a frontend framework for our marketing site and blog.

## Decision
Use Astro with React islands.

## Rationale
- Static site generation (fast, SEO-friendly)
- Islands architecture (minimal JavaScript)
- React for interactive components (team familiar)
- Good DX, fast builds

## Consequences
- Positive: Fast sites, good SEO, low hosting cost
- Negative: Learning curve for islands pattern
- Trade-off: Less dynamic than SPA, but we don't need that

## Alternatives Considered
- Next.js: More complex, heavier JS, overkill for our needs
- Vanilla HTML: Too limited for dynamic components
- SvelteKit: Team not familiar with Svelte

## References
- Astro docs: https://docs.astro.build
- Islands architecture: https://jasonformat.com/islands-architecture/
```

**Monthly context refresh:**

```markdown
# docs/context-refresh/2025-01-monthly.md

# January 2025 Context Refresh

## What Changed
- Migrated from D1 to PostgreSQL (performance)
- Added user authentication (email + password)
- Redesigned homepage (new hero section)

## Current Architecture
- Frontend: Astro + React islands
- Backend: Cloudflare Workers + Pages Functions
- Database: PostgreSQL (via Neon)
- Auth: Custom JWT implementation
- Hosting: Cloudflare Pages

## Active Patterns
- Use server endpoints for API routes
- Use React islands for interactive components
- Use PostgreSQL for relational data
- Use KV for caching
- Use R2 for file uploads

## Deprecated Patterns
- ❌ D1 database (migrated to PostgreSQL)
- ❌ Direct database queries in components (use API now)

## Current Priorities
1. Add payment integration (Stripe)
2. Improve mobile performance
3. Add admin dashboard

## Team Notes
- John: Working on payment integration
- Sarah: Handling mobile optimization
- Mike: Building admin dashboard
```

**Update .cursorrules quarterly:**

```markdown
# .cursorrules (Updated 2025-01-15)

## Current State (Q1 2025)

### Tech Stack (Updated)
- Frontend: Astro 4.0
- Database: PostgreSQL via Neon (migrated from D1 in Dec 2024)
- Auth: Custom JWT (added Jan 2025)
- Payments: Stripe (in progress)

### Recent Changes
- Dec 2024: Migrated from D1 to PostgreSQL
- Jan 2025: Added authentication
- Jan 2025: Redesigned homepage

### Active Work
- Payment integration (John)
- Mobile optimization (Sarah)
- Admin dashboard (Mike)

[Rest of .cursorrules...]
```

### Periodic Context Audits

**Every 3 months:**

1. **Review .cursorrules** - Update for current state
2. **Review ADRs** - Mark superseded decisions
3. **Review docs/** - Update architecture diagrams
4. **Review prompts/** - Update prompt templates
5. **Review patterns/** - Document new patterns

**Audit checklist:**
```markdown
# Quarterly Context Audit Checklist

## .cursorrules
☐ Updated tech stack versions
☐ Added new patterns
☐ Removed deprecated patterns
☐ Updated team info
☐ Updated file structure

## ADRs
☐ Reviewed all ADRs
☐ Marked superseded ADRs
☐ Created ADRs for recent major decisions

## Documentation
☐ Updated README
☐ Updated architecture diagram
☐ Updated API documentation
☐ Updated deployment docs

## Context Files
☐ Monthly refresh docs up to date
☐ Prompt templates current
☐ Pattern library current

## Git
☐ All branches merged or cleaned up
☐ Tags for major releases
☐ Changelog updated
```

## Cross-Project Context Sharing

### Challenge

Patterns, components, and knowledge from one project could benefit others. But each project is unique.

### Strategy: Pattern Library

**Create shared pattern library:**

```
~/dev/patterns/
├── astro-patterns/
│   ├── auth-pattern.md
│   ├── api-routes-pattern.md
│   └── islands-pattern.md
├── cloudflare-patterns/
│   ├── d1-patterns.md
│   ├── kv-patterns.md
│   └── workers-patterns.md
└── README.md
```

**Pattern template:**

```markdown
# Pattern: Authentication with JWT

## Context
When you need user authentication in an Astro + Cloudflare Pages project.

## Problem
Need secure, stateless authentication that works with serverless architecture.

## Solution
Use JWT tokens stored in httpOnly cookies.

## Implementation

### 1. Create auth utility
[Code example]

### 2. Create login endpoint
[Code example]

### 3. Protect routes
[Code example]

## Pros
- Stateless (works in serverless)
- Secure (httpOnly cookies)
- Scalable (no session storage)

## Cons
- Can't invalidate tokens (use short expiry)
- Token size (keep payload small)

## Alternatives
- Session-based auth (requires session storage)
- OAuth (more complex, better for SSO)

## Used In
- Project A (e-commerce site)
- Project B (SaaS dashboard)

## References
- [JWT docs]
- [Security considerations]
```

### Reusable Components Library

**Maintain component library for copy-paste:**

```
~/dev/components/
├── astro/
│   ├── ContactForm.astro
│   ├── Newsletter.astro
│   └── PricingTable.astro
└── react/
    ├── Modal.tsx
    ├── Tooltip.tsx
    └── Dropdown.tsx
```

**Each component has usage notes:**

```typescript
/**
 * Modal Component
 *
 * Reusable modal with keyboard navigation and focus management.
 *
 * Used in:
 * - Project A (product previews)
 * - Project B (form dialogs)
 *
 * To use in new project:
 * 1. Copy this file
 * 2. Adjust styling to match project
 * 3. Test keyboard navigation
 * 4. Test with screen readers
 *
 * Dependencies:
 * - @headlessui/react (for accessibility)
 *
 * Customization points:
 * - Background color
 * - Border radius
 * - Animation timing
 */

export function Modal({ children, isOpen, onClose }: ModalProps) {
  // Implementation
}
```

### Project Templates

**Maintain project starter templates:**

```
~/dev/templates/
├── astro-static-site/
├── astro-saas/
└── astro-ecommerce/
```

Each template includes:
- Pre-configured .cursorrules
- ADR template
- Folder structure
- Example patterns
- Common components

## Team Collaboration Context

### Challenge

Multiple developers working on same codebase. AI needs to understand team conventions and work-in-progress.

### Strategy: Shared Context Standards

**Team .cursorrules (in repo):**

```markdown
# .cursorrules

## Team Context Standards

### Team Members
- John (Lead): @johnsmith - Architecture, database
- Sarah (Senior): @sarahdev - Frontend, performance
- Mike (Mid): @mikedev - Features, testing

### Work In Progress
Check /docs/wip/ for features in development.

### Code Style
- ESLint config in root
- Prettier for formatting
- TypeScript strict mode
- Functional components (React)

### Patterns
- API routes in /src/pages/api/
- Components in /src/components/
- Utils in /src/utils/
- Types in /src/types/

### Branch Strategy
- main - Production
- develop - Integration
- feature/* - New features
- fix/* - Bug fixes

### Before Asking AI
1. Read relevant ADR in /docs/adr/
2. Check patterns in /docs/patterns/
3. Review recent changes in CHANGELOG
4. Check WIP docs in /docs/wip/

### AI Usage Guidelines
- Provide context about your task
- Reference existing patterns
- Ask for explanations, not just code
- Review AI output before committing
```

### Work-In-Progress Documentation

**Active feature docs:**

```markdown
# docs/wip/payment-integration.md

# Payment Integration (WIP)

Owner: John (@johnsmith)
Status: In Progress (60% complete)
Target: 2025-02-01

## What's Done
- ✅ Stripe account setup
- ✅ API keys configured
- ✅ Test mode working
- ✅ Checkout flow UI

## What's Next
- ⏳ Webhook handling (in progress)
- ☐ Production testing
- ☐ Error handling
- ☐ Admin dashboard integration

## Files Changed
- /src/pages/api/checkout.ts (new)
- /src/components/CheckoutButton.tsx (new)
- /src/pages/pricing.astro (modified)

## Dependencies
- stripe npm package
- Environment variables: STRIPE_SECRET_KEY, STRIPE_WEBHOOK_SECRET

## Notes for Team
- Don't modify checkout.ts yet, major refactor coming
- Webhook endpoint will be /api/webhooks/stripe
- Use test card: 4242 4242 4242 4242

## Questions/Blockers
- Need production Stripe account approval
- Waiting on design feedback for error states
```

### Handoff Context

When handing off work:

```markdown
# docs/handoffs/authentication-to-mike.md

# Authentication Feature Handoff

From: John
To: Mike
Date: 2025-01-15

## What I Did
Implemented basic email/password authentication:
- Login/logout endpoints (/src/pages/api/auth/)
- JWT token generation and validation
- Protected route middleware
- User registration flow

## Files to Know
- /src/pages/api/auth/* - Auth endpoints
- /src/middleware/auth.ts - Route protection
- /src/utils/jwt.ts - Token utilities
- /src/components/LoginForm.tsx - Login UI

## How It Works
1. User submits login form
2. API validates credentials
3. JWT token issued in httpOnly cookie
4. Protected routes check token in middleware
5. Token expires after 7 days

## What's Left
- Password reset flow (priority)
- Email verification
- OAuth integration (Google, GitHub)
- Rate limiting on login attempts
- Admin user management

## Known Issues
- None currently

## Tests
- Unit tests in /src/__tests__/auth/
- Run: `npm test auth`
- All passing

## How to Test Locally
1. Register: POST /api/auth/register
2. Login: POST /api/auth/login
3. Access protected route: /dashboard
4. Should see user info

## Questions?
Slack me or check /docs/adr/0005-authentication-approach.md
```

## Context for Different AI Models

### Challenge

Different AI models have different context window sizes and capabilities. Strategies must adapt.

### Model-Specific Strategies

**Claude Sonnet 4 (200k tokens):**
- Can handle large codebases
- Load multiple related files
- Comprehensive project context
- Full .cursorrules without condensing

**GPT-4 (128k tokens):**
- More selective file loading
- Condense .cursorrules slightly
- Focus on active files
- Use summaries for dependencies

**Qwen/GLM (128k tokens):**
- Similar to GPT-4
- Prioritize current task files
- Minimal historical context
- Clear, structured instructions

**Smaller models (32k-64k tokens):**
- Very focused context
- Only immediate task files
- Abbreviated .cursorrules
- Reference docs by summary, not full content

### Adaptive .cursorrules

**Create model-specific versions if needed:**

```
.cursorrules (full version, 5000 tokens)
.cursorrules-compact (condensed, 2000 tokens)
```

**Switch based on model:**
```
Using Claude Sonnet 4? Use .cursorrules
Using GPT-3.5 or small models? Use .cursorrules-compact
```

**Compact version focuses on:**
- Essential patterns only
- Current architecture
- Critical constraints
- Active conventions

## Summary: Advanced Context Principles

### 1. Progressive Disclosure
Start narrow, expand as needed. Never load everything.

### 2. Clear Boundaries
Define what's in scope, what's out of scope.

### 3. Living Documentation
Keep context fresh. Monthly reviews, quarterly audits.

### 4. Shared Standards
Team-wide conventions. Documented and enforced.

### 5. Context Hygiene
Remove outdated info. Mark deprecated patterns.

### 6. Purpose-Built Context
Different tasks need different context. Don't reuse blindly.

### 7. Model Awareness
Adapt strategy to model capabilities.

---

**Remember:** Context management is not set-and-forget. It's ongoing maintenance critical to effective AI-assisted development.
