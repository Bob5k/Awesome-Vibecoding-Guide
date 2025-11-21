# Phase 3: Testing, Debugging & Code Review 🧪🔍

**Tools:** DevTools MCP + Your coding agent + Manual Testing + Code Review

## Overview

This phase combines testing, debugging, and code review into a comprehensive quality assurance process. The goal is to ensure your code works correctly, performs well, and meets quality standards before deployment.

---

## 🚀 Part 1: Automated Testing & Debugging

### The Awesome Vibecoding Advantage: Hands-Free Debugging

**Traditional debugging vs AI-powered testing:**

**Old way:**
- Manually test broken functionality
- Spend hours investigating console errors
- Manually check network requests and responses
- Waste precious time on repetitive testing

**New way with Chrome DevTools MCP:**
- **Task the AI agent** to handle all debugging automatically
- **Save your most valuable resource** - time
- **Focus on business growth** while AI fixes technical issues

### Automated Testing Process

**Step 1: Automated Testing via MCP**
```
"Use DevTools MCP to test the login page and find bugs."
```

Agent will:
- Open the browser
- Navigate the app
- Collect console errors
- Analyze network calls
- Identify issues
- Propose fixes

**Step 2: Manual Testing**
- Walk through the functionality yourself
- Document edge cases
- Check different browsers/devices

### How to Use Automated Web Debugging

**Example Scenario: Broken Contact Form**

1. **Start your local development server:**
   ```bash
   npm run dev
   # or python -m http.server, etc.
   ```

2. **Task the AI agent with specific instructions:**
   ```
   "My contact form submit button is broken. Please:
   - Navigate to http://localhost:3000
   - Fill out the contact form with test data
   - Click the submit button
   - Debug any issues using Chrome DevTools
   - Check console errors, network requests, and responses
   - Identify and fix the root cause
   - Verify the fix works"
   ```

3. **What the AI agent will do:**
   - **Navigate** to your localhost URL
   - **Take snapshots** of the page structure
   - **Interact** with form elements
   - **Monitor** network requests in real-time
   - **Analyze** console errors and warnings
   - **Inspect** API responses and status codes
   - **Debug** JavaScript execution flow
   - **Identify** the root cause of issues
   - **Suggest** and implement fixes

### Common Debugging Scenarios

**Broken User Interactions:**
- Click handlers not working
- Form validation issues
- API calls failing
- State management problems
- Responsive design bugs

**Performance Issues:**
- Slow loading times
- Memory leaks
- Inefficient JavaScript
- Large bundle sizes
- Slow API responses

**UI/UX Problems:**
- Elements not appearing
- Styling issues
- Layout problems
- Mobile responsiveness
- Accessibility barriers

### Benefits of Automated Debugging

**⏰ Time Savings:**
- No more manual testing cycles
- No need to reproduce bugs yourself
- AI can test multiple scenarios rapidly
- Focus on features, not debugging

**🎯 Accuracy:**
- AI catches edge cases humans might miss
- Systematic approach to testing
- Comprehensive error analysis
- Detailed investigation of all failure points

**🚀 Productivity Boost:**
- Debug while you work on other tasks
- Parallel development and testing
- Faster iteration cycles
- More features delivered per week

**💼 Business Value:**
- Ship features faster
- Improve code quality
- Reduce bug reports
- Better user experience

### Pro Tips for Maximum Efficiency

1. **Be specific in your instructions:**
   ```
   "The login form on /login isn't working. Test with both valid and invalid credentials,
   check the network request payload, and verify the error handling."
   ```

2. **Provide context when possible:**
   ```
   "Since I updated the authentication library, the user dashboard is broken.
   Check if the API endpoints changed and if the token handling is still correct."
   ```

3. **Let the agent work independently:**
   - Start the debugging task
   - Move to marketing, content creation, or business development
   - Come back to a detailed analysis and proposed fixes

### Real-World Example Workflow

**You:** "I need to launch my SaaS product but the payment integration is broken"

**AI Agent:** *(30 minutes later)*
```
✅ **Debugging Complete - Payment Integration Fixed**

**Issues Found:**
1. Stripe API endpoint was outdated (v3 → v4)
2. CORS headers missing on payment processing endpoint
3. Error handling not catching network failures properly

**Fixes Applied:**
- Updated API calls to Stripe v4
- Added proper CORS middleware
- Implemented comprehensive error handling
- Added retry logic for failed requests

**Testing Results:**
- ✅ Test payments: 10/10 successful
- ✅ Error handling: All edge cases covered
- ✅ Mobile responsiveness: Working perfectly
- ✅ Performance: <2s load time
```

**Result:** You spent 30 minutes on LinkedIn outreach while AI fixed your payment system.

---

## 🎯 Part 2: Chrome DevTools Mastery

### Chrome DevTools Basics

**Essential Resource:**
[Chrome DevTools Official Documentation](https://developer.chrome.com/docs/devtools)

**Why Learn DevTools:**
- AI can automate testing, but YOU need to understand what's happening
- Manual testing still required for final QA
- Essential for understanding AI-reported issues
- Professional developers know their browser tools

### Essential DevTools Knowledge

#### Console Tab Essentials

**What It Does:**
- Displays JavaScript errors and warnings
- Logs custom messages (`console.log()`)
- Allows interactive JavaScript execution
- Shows network errors

**Key Actions:**
```javascript
// Filtering
// Click "Errors" "Warnings" "Info" to filter

// Clear console
Cmd/Ctrl + K  or  Clear console button

// Search within console
Cmd/Ctrl + F

// Preserve log on navigation
☑ Preserve log
```

**Common Issues to Look For:**
```
❌ Uncaught TypeError: Cannot read property 'X' of undefined
   → Something is null/undefined when it shouldn't be

❌ 404 (Not Found) - Failed to load resource
   → File path incorrect or file missing

❌ CORS policy: No 'Access-Control-Allow-Origin' header
   → Backend not configured for cross-origin requests

⚠️  Deprecated API warning
   → Using outdated methods (won't break now, but future issue)
```

**Pro Tips:**
- Always check console first when something breaks
- `console.log()` is your friend during development
- `console.table()` for displaying arrays/objects nicely
- `console.error()` for highlighting important errors

#### Network Tab Essentials

**What It Does:**
- Shows all HTTP requests
- Displays request/response details
- Monitors loading times
- Debugs API failures

**Key Columns:**
```
Name       - Request URL
Status     - HTTP status code (200, 404, 500, etc.)
Type       - Resource type (document, script, xhr, etc.)
Initiator  - What triggered the request
Size       - Response size
Time       - How long it took
Waterfall  - Visual timeline
```

**Common Issues:**
```
❌ Status 404 - Not Found
   → Check URL spelling and file location

❌ Status 500 - Internal Server Error
   → Backend problem, check server logs

❌ Status 401/403 - Unauthorized/Forbidden
   → Authentication or permission issue

⏱️  Request taking >3 seconds
   → Performance issue, optimize or cache

🔴 Failed (red) request
   → Network error, CORS, or blocked request
```

**Inspect API Calls:**
```
1. Filter by "XHR" or "Fetch" for API calls
2. Click request to see:
   - Headers (request/response)
   - Payload (what you sent)
   - Preview (response data formatted)
   - Response (raw response)
   - Timing (breakdown of request time)
```

**Pro Tips:**
- Right-click request → "Copy as cURL" to reproduce in terminal
- "Preserve log" to keep requests across page navigations
- Throttle network (Fast 3G, Slow 3G) to test slow connections
- "Disable cache" when testing changes

#### Elements/Inspector Essentials

**What It Does:**
- Inspect HTML structure
- Modify CSS live
- Test responsive layouts
- Debug visual issues

**Key Actions:**
```
Inspect element: Right-click element → Inspect
or: Cmd/Ctrl + Shift + C (inspector mode)

Modify HTML: Double-click element in tree
Modify CSS: Add/edit styles in Styles panel
Test states: :hover :active :focus in Styles panel
```

**Responsive Design Mode:**
```
1. Click device icon (or Cmd/Ctrl + Shift + M)
2. Select device:
   - iPhone 12/13 Pro
   - iPad
   - Custom dimensions
3. Test:
   - Portrait and landscape
   - Touch events
   - Device pixel ratio
```

**Common Issues:**
```
❌ Element not visible but exists in DOM
   → CSS: display: none, opacity: 0, or positioned off-screen

❌ Layout breaking at certain width
   → Missing media query or hardcoded widths

❌ Styles not applying
   → Specificity issue (check Computed tab for overrides)
   → Wrong selector
```

**Pro Tips:**
- Use "Computed" tab to see final applied styles
- Check "Event Listeners" to see attached JavaScript events
- "Accessibility" tab shows ARIA labels and role
- Use color picker in Styles panel for quick color adjustments

#### Performance Tab Basics

**When to Use:**
- Site feels slow
- Investigating load times
- Optimizing animations
- Finding performance bottlenecks

**How to Profile:**
```
1. Open Performance tab
2. Click Record (●)
3. Perform the slow action
4. Click Stop
5. Analyze the recording
```

**What to Look For:**
```
🔴 Large red bars - Long tasks blocking main thread
🟡 Yellow sections - JavaScript execution
🟣 Purple sections - Rendering/layout
🟢 Green sections - Painting

Look for:
- Long tasks (>50ms)
- Excessive reflows
- JavaScript taking too long
- Too many function calls
```

**Quick Wins:**
```
❌ JavaScript running on every scroll
   → Debounce or throttle scroll handler

❌ Large images loading slowly
   → Compress and lazy load

❌ Too many DOM manipulations
   → Batch updates or use virtual DOM (React)
```

---

## 📱 Part 3: Mobile-First Testing Strategy

### The Critical Reality

**85%+ of traffic is mobile for most small business websites.**

**The Most Common Mistake:**
Testing on laptop (where you develop) instead of optimizing for mobile first.

**Why This Matters:**
- User experience = Mobile experience
- Google uses mobile-first indexing for SEO
- Slow mobile site = lost customers
- Most bugs appear on mobile, not desktop

### The Mobile-First Approach

**Workflow:**
```
1. Mobile testing FIRST (always)
2. Tablet testing SECOND
3. Desktop testing LAST
```

**NOT:**
```
❌ Desktop first, mobile "if I have time"
❌ Desktop only, assuming mobile "works"
❌ Mobile testing as afterthought
```

### Mobile Testing Workflow

#### Step 1: Chrome DevTools Mobile Emulation

**Open Device Mode:**
```
Cmd/Ctrl + Shift + M
or
Click device icon in DevTools toolbar
```

**Test These Devices:**
```
Priority 1 (Most Common):
- iPhone 13/14 Pro (390 x 844)
- iPhone 13/14 Pro Max (428 x 926)
- Samsung Galaxy S21/S22 (360 x 800)

Priority 2 (Common):
- iPhone SE (375 x 667) - Small screen
- iPad (768 x 1024) - Tablet
- iPad Pro (1024 x 1366) - Large tablet
```

**Test Both Orientations:**
- Portrait (default, 90% of usage)
- Landscape (especially for forms and content)

#### Step 2: Touch Interaction Testing

**Common Touch Issues:**
```
❌ Buttons too small (< 44x44 pixels)
   → Fingers can't tap accurately

❌ Links too close together
   → Accidental taps on wrong link

❌ Hover effects that don't work on touch
   → No hover on mobile, use :active or :focus

❌ Dropdown menus that need hover
   → Convert to click/tap menus
```

**Test With Touch Emulation:**
```
DevTools → Settings → Devices → Add custom device
Enable "Touch" for custom devices
```

**Touch-Friendly Design:**
```css
/* Minimum touch target size */
button, a {
  min-width: 44px;
  min-height: 44px;
  padding: 12px;
}

/* Adequate spacing between tappable elements */
.button-group button {
  margin: 8px;
}

/* Remove hover-only interactions */
.dropdown:hover .menu {
  display: block;  /* ❌ Doesn't work on mobile */
}

/* Use click/tap instead */
.dropdown.active .menu {
  display: block;  /* ✅ Works on mobile */
}
```

#### Step 3: Real Device Testing

**DevTools Emulation ≠ Real Device**

**After DevTools testing, test on real devices:**
- Your phone (at minimum)
- Tablet (if possible)
- Client's device (ideal)

**How to Test on Real Device:**

**Option 1: Local Network Access**
```bash
# Find your local IP
# macOS/Linux: ifconfig | grep "inet "
# Windows: ipconfig

# Start dev server
npm run dev
# Usually: http://localhost:3000

# Access on phone
http://192.168.1.X:3000
(Replace with your IP)
```

**Option 2: Cloudflare Tunnel (Preview)**
```bash
# Deploy branch to Cloudflare Pages
git push origin feat/your-feature

# Access preview URL from phone
https://feat-your-feature.project.pages.dev
```

**Option 3: Chrome Remote Debugging**
```
1. Enable USB debugging on Android phone
2. Connect phone via USB
3. Chrome DevTools → More tools → Remote devices
4. Inspect and debug directly on phone
```

#### Step 4: Mobile-Specific Testing Checklist

**Visual Layout:**
- [ ] All text readable without zooming
- [ ] Images scaled properly
- [ ] No horizontal scrolling (unless intentional)
- [ ] Navigation accessible and usable
- [ ] Forms fit on screen
- [ ] Buttons large enough to tap
- [ ] Spacing adequate between interactive elements

**Performance:**
- [ ] Page loads in < 3 seconds on 3G
- [ ] No layout shift during load (CLS)
- [ ] Smooth scrolling
- [ ] Fast tap responses
- [ ] Efficient image loading

**Functionality:**
- [ ] Forms submittable
- [ ] Links tappable
- [ ] Dropdown menus accessible
- [ ] Modals/popups usable
- [ ] No JavaScript errors in console
- [ ] API calls working

**User Experience:**
- [ ] Text large enough (16px minimum)
- [ ] Contrast sufficient (4.5:1 ratio)
- [ ] Forms use appropriate input types (email, tel, number)
- [ ] Keyboard shows appropriate layout (numeric for phone)
- [ ] Auto-complete works on forms
- [ ] Back button works as expected

### Common Mobile Issues and Fixes

#### Issue 1: Text Too Small

**Problem:**
```css
body {
  font-size: 14px;  /* ❌ Too small on mobile */
}
```

**Fix:**
```css
body {
  font-size: 16px;  /* ✅ Readable minimum */
}

@media (min-width: 768px) {
  body {
    font-size: 18px;  /* Larger on desktop if desired */
  }
}
```

#### Issue 2: Horizontal Scrolling

**Problem:**
```css
.container {
  width: 1200px;  /* ❌ Fixed width overflows on mobile */
}
```

**Fix:**
```css
.container {
  width: 100%;  /* ✅ Fluid width */
  max-width: 1200px;
  padding: 0 16px;  /* Add padding for edges */
}
```

#### Issue 3: Buttons Too Small

**Problem:**
```html
<a href="/contact">Contact</a>
<!-- Text link hard to tap -->
```

**Fix:**
```html
<a href="/contact" class="button">Contact</a>

<style>
.button {
  display: inline-block;
  padding: 12px 24px;  /* Large tap target */
  min-height: 44px;
  text-align: center;
}
</style>
```

#### Issue 4: Forms Difficult to Fill

**Problem:**
```html
<input type="text" name="email">
<!-- No autocomplete, wrong keyboard -->
```

**Fix:**
```html
<input
  type="email"
  name="email"
  autocomplete="email"
  placeholder="your@email.com"
>
<!-- Correct keyboard, autocomplete enabled -->
```

### Performance Testing on Mobile

**Chrome DevTools Network Throttling:**
```
Network tab → Throttling dropdown:
- Slow 3G (testing worst case)
- Fast 3G (average mobile)
- No throttling (Wi-Fi)
```

**Lighthouse Mobile Audit:**
```
1. Open Lighthouse tab in DevTools
2. Select "Mobile" device
3. Click "Analyze page load"
4. Review scores:
   - Performance (target: 90+)
   - Accessibility (target: 100)
   - Best Practices (target: 100)
   - SEO (target: 100)
```

**Target Metrics (Mobile):**
```
✅ First Contentful Paint: < 1.8s
✅ Largest Contentful Paint: < 2.5s
✅ Time to Interactive: < 3.8s
✅ Cumulative Layout Shift: < 0.1
✅ Total page size: < 1MB
```

---

## 💼 Part 4: Client-Specific Testing

### Understanding Your Client's Audience

**Critical Question to Ask Client:**
"Who is your typical customer and how do they access your website?"

**Why This Matters:**
- B2B vs. B2C have different usage patterns
- Industry affects device usage
- Audience affects testing priorities

### B2B (Business-to-Business) Clients

**Typical Scenario:**
- Office workers during business hours
- Desktop/laptop primary device
- Professional environment
- Corporate networks

**Examples:**
- Accounting firms
- Legal services
- B2B SaaS companies
- Manufacturing suppliers
- Corporate consulting

**Testing Priority:**
```
1. Desktop (60-80% of traffic)
2. Mobile (20-40% of traffic)
3. Tablet (5-10% of traffic)
```

**Desktop-Specific Considerations:**
- Larger forms are acceptable
- More complex navigation is fine
- Hover interactions work
- Detailed data tables usable
- Multiple columns in layout

**Client Communication:**
```
"Based on your B2B audience, I'm prioritizing desktop testing
since most of your customers will be accessing the site from
office computers. Mobile will work great too, but the experience
is optimized for desktop users."
```

### B2C (Business-to-Consumer) Clients

**Typical Scenario:**
- Consumers browsing anytime
- Mobile primary device (especially local businesses)
- On-the-go searching
- Quick decision making

**Examples:**
- Restaurants
- Plumbers, electricians, HVAC
- Hair salons, barbershops
- Retail stores
- Local services

**Testing Priority:**
```
1. Mobile (70-90% of traffic)
2. Desktop (10-25% of traffic)
3. Tablet (5-10% of traffic)
```

**Mobile-Specific Considerations:**
- Click-to-call prominent
- Simple navigation
- Quick loading
- Minimal form fields
- Large, tappable buttons
- Google Maps integration
- Easy-to-find hours and location

**Client Communication:**
```
"Since you're a local service business, I'm optimizing primarily
for mobile users. Most people will find you while searching on
their phone, so mobile performance and usability are critical."
```

### Industry-Specific Patterns

#### Restaurants and Food Services
```
Mobile: 85-90%
Peak times: Lunch (11am-2pm), Dinner (5pm-8pm)
Priority: Menu, phone, directions, hours
```

#### Professional Services (Lawyers, Accountants)
```
Mobile: 50-60%
Desktop: 40-50%
Priority: Credentials, services, contact forms
```

#### Home Services (Plumbers, Electricians)
```
Mobile: 80-90%
Often emergency situations
Priority: Phone number, service area, availability
```

#### E-commerce
```
Mobile: 60-70% (and growing)
Desktop: 30-40%
Priority: Product images, checkout flow, mobile payments
```

#### Healthcare
```
Mobile: 65-75%
Desktop: 25-35%
Priority: Appointments, directions, insurance, forms
```

### Client Discovery Questions

**Ask During Initial Consultation:**

**Question 1: Audience Demographics**
```
"Who is your typical customer?"
- Age range
- Tech-savviness
- When they search for services
```

**Question 2: Current Traffic Data**
```
"Do you have Google Analytics for your current site?"
- Check mobile vs. desktop split
- Review actual data vs. assumptions
```

**Question 3: Customer Journey**
```
"How do customers usually find you?"
- Google search (usually mobile)
- Referrals (mixed devices)
- Direct URL (usually desktop)
- Social media (usually mobile)
```

**Question 4: Primary Action**
```
"What do you want visitors to do on your site?"
- Call you (mobile-friendly CTA critical)
- Fill out form (desktop-friendly if complex)
- Browse products (mobile and desktop equal)
- Book appointment (works on both, but test mobile)
```

### Adjusting Testing Strategy

**For Desktop-Heavy Clients:**
```
Testing order:
1. Desktop functionality ✓
2. Desktop design ✓
3. Mobile responsive ✓
4. Mobile functionality ✓

Okay to optimize FOR desktop while ensuring mobile WORKS.
```

**For Mobile-Heavy Clients:**
```
Testing order:
1. Mobile functionality ✓
2. Mobile performance ✓
3. Mobile design ✓
4. Desktop (should just work) ✓

Optimize FOR mobile; desktop gets simpler, wider layout.
```

**When in Doubt: Mobile First**
Default assumption: **85% mobile traffic** until client data says otherwise.

---

## 🔍 Part 5: Code Review & Refactoring

### Debugging Deep Dive

**Golden rule:** Debugging is effective only when you dig deep.

**Don't:**
- "Doesn't work, fix it"
- "Still doesn't work, fix pls" (x100)

**Do:**
- Analyze the bug (manually or via MCP)
- Gather logs specific to the issue
- Identify the exact root cause
- Tell the AI what you found + ask for a fix

**If the same bug repeats 2–3 times:**
1. Stop—something is fundamentally wrong
2. Use MCP to gather precise logs
3. Analyze them before the next prompt
4. You may need to change approach, not just code

### Code Review Process

**Step 1: First Pass - AI Review**
- Claude or GPT review of the entire feature codebase
- Comprehensive analysis of code quality and architecture

**Step 2: Identify Issues**
- Performance problems
- Security holes
- Code duplication
- Convention violations
- Maintainability issues
- Documentation gaps

**Step 3: Refactoring Implementation**
- AI implements suggested improvements
- Apply best practices and design patterns
- Optimize performance bottlenecks
- Enhance security measures

**Step 4: Second Review**
- Ensure everything still works after refactoring
- Verify improvements don't break existing functionality
- Performance testing post-optimization

### Code Quality Checklist

**✅ Performance:**
- Efficient algorithms and data structures
- Minimal unnecessary computations
- Optimized database queries
- Proper caching strategies

**✅ Security:**
- Input validation and sanitization
- Proper authentication and authorization
- SQL injection prevention
- XSS protection
- CSRF protection

**✅ Maintainability:**
- Clear and descriptive naming conventions
- Proper code organization and structure
- Consistent coding style
- Adequate comments and documentation
- Single responsibility principle

**✅ Best Practices:**
- Error handling and logging
- Proper async/await usage
- Environment variable management
- Version control best practices
- Testing coverage

### Beware Over-Optimization

- If a simple bug requires a complete refactor → something's off
- Try other models (Gemini, a different Claude)—maybe there's a simpler solution
- Don't let AI over-engineer simple problems
- Balance between perfect code and practical delivery

## Pre-requisites & Next Steps

**Requires completion of:**
- [Phase 2: Development](./phase-2-development.md) — All features implemented and committed
- [Core Technologies setup](../core-technologies.md) — Astro + Tailwind + Cloudflare stack configured
- [Development Tools](../development-tools/README.md) — DevTools MCP and testing tools configured

**Prepares for:**
- [Phase 4: Deployment](./phase-4-deployment.md) — Production deployment and CI/CD setup
- [Hosting Tools](../hosting-tools/README.md) — Cloudflare infrastructure configuration
- [Business strategy](../introduction/README.md) — Client delivery and maintenance

**Related Reading:**
- [Context Management](../context-management/README.md) — Debug context and error tracking
- [AI Model Providers](../ai-model-providers/README.md) — Optimization for debugging tasks
- [Development Tools: DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) — Advanced testing capabilities

**Testing Integration:**
- Automated testing via [DevTools MCP](../development-tools/mcp-servers/devtools-mcp.md) for comprehensive debugging
- Manual testing following [Phase 2 practices](./phase-2-development.md#manual-testing)
- Code review using [AI Model Providers](../ai-model-providers/README.md) for quality analysis

---

## Debugging Troubleshooting

**Common debugging challenges and solutions during testing phase**

### AI Can't Find the Bug

**Symptom:** Despite providing error messages and code, AI can't identify the root cause.

**Root causes:**
1. Insufficient diagnostic information
2. Bug is environmental (not in code itself)
3. Complex interaction between components
4. Timing/async issue

**Solutions:**

**Solution 1: Provide Complete Diagnostic Data**
```
"Help debug this issue:

ERROR MESSAGE:
[full error text, not truncated]

STACK TRACE:
[complete stack trace with all frames]

BROWSER CONSOLE:
[all console messages, warnings, errors]

NETWORK TAB:
- Request URL: [URL]
- Status: [status code]
- Response: [response body]
- Headers: [relevant headers]

CODE AT ERROR LOCATION ([file:line]):
[10-20 lines around error]

USER ACTION THAT TRIGGERS IT:
[exact steps to reproduce]

ENVIRONMENT:
- Browser: [Chrome 120 / Firefox 115]
- OS: [macOS / Windows / Linux]
- Node version: [18.16.0]
- Framework version: [React 18.2.0]"
```

**Solution 2: Create Minimal Reproduction**
```
"I've isolated the bug to minimal reproduction:

[Minimal code that demonstrates issue]

This code alone triggers the error.
No other dependencies or components needed.

Expected: [behavior]
Actual: [behavior]

Debug this minimal case."
```

**Solution 3: Use DevTools MCP**
```
"Use DevTools MCP to debug this issue:
1. Navigate to http://localhost:3000/problem-page
2. Open DevTools and monitor:
   - Console for errors
   - Network for failed requests
   - Elements for DOM issues
3. Reproduce the bug by [steps]
4. Analyze what happens and identify root cause"
```

**Prevention:**
- Always provide complete error info (don't truncate)
- Include stack traces
- Describe reproduction steps
- Check browser compatibility

**Related:** [Can't Debug Issue Flowchart](../troubleshooting/README.md#flowchart-2-cant-debug-issue)

---

### Tests Failing After Changes

**Symptom:** Tests that previously passed now fail.

**Quick diagnosis:**
```bash
# Run tests to see failures
npm test

# Run specific failing test
npm test -- UserService.test.ts

# Check git diff
git diff HEAD~1 HEAD

# Identify what changed
git log --oneline -5
```

**Quick fix:**
```
"Tests failing after recent changes:

FAILING TEST:
[test name and description]

ERROR MESSAGE:
[test error output]

RECENT CHANGES (git diff):
[relevant code changes]

Expected behavior: [what test expects]
Actual behavior: [what's happening]

Fix options:
1. Update implementation to match test
2. Update test to match new implementation (if requirements changed)

Which is correct: [implementation or test]?"
```

**Prevention:**
- Run tests before committing
- Write tests alongside code changes
- Keep test coverage high
- Use test-driven development (TDD)

---

### Performance Issues Hard to Debug

**Symptom:** App is slow but profiling doesn't show obvious bottleneck.

**Diagnostic approach:**
```
"Analyze performance issue:

SYMPTOM:
- [Page/feature] takes [X seconds] to load
- Target: < [Y seconds]

CURRENT METRICS (from Chrome DevTools Performance tab):
- Total time: [X ms]
- Scripting: [X ms]
- Rendering: [X ms]
- Painting: [X ms]
- Network: [X ms]

PROFILING DATA:
[Screenshot or export from Performance tab]

NETWORK TAB:
- Total requests: [number]
- Largest requests: [list top 5]
- Slow requests: [>1s]

CODE:
[Relevant component/function code]

Identify:
1. Primary bottleneck
2. Quick wins for improvement
3. Recommended optimizations"
```

**Common performance issues:**
- N+1 database queries
- Large bundle sizes
- Unoptimized images
- No code splitting
- Memory leaks
- Excessive re-renders (React)

**Quick wins:**
```
1. Database:
   - Add indexes
   - Use eager loading
   - Implement pagination

2. Frontend:
   - Code splitting
   - Lazy loading
   - Image optimization
   - Memoization (React.memo, useMemo)

3. Network:
   - Enable gzip/brotli compression
   - Use CDN
   - Implement caching
   - Reduce request count
```

**Related:** [Performance Optimization](../troubleshooting/README.md#poor-performance)

---

### Race Conditions and Timing Issues

**Symptom:** Bug happens intermittently, hard to reproduce consistently.

**Indicators:**
- "Works sometimes, not others"
- "Only fails in production (fast server)"
- "Only fails on slow connections"
- Data inconsistency

**Diagnosis:**
```
"Debug race condition:

SYMPTOM:
- [Behavior happens intermittently]
- Success rate: ~[X%]

SUSPECTED RACE CONDITION:
[Describe async operations happening simultaneously]

CODE:
```typescript
// Example:
async function loadData() {
  const user = await fetchUser();  // Async 1
  const posts = await fetchPosts();  // Async 2
  // Race: If fetchPosts returns before user updates state...
  setUserPosts(posts);  // May use stale user data
}
```

EXPECTED: [ordered behavior]
ACTUAL: [race outcome]

Add proper sequencing/synchronization."
```

**Solutions:**
```typescript
// Solution 1: Sequential (when order matters)
const user = await fetchUser();
const posts = await fetchPosts(user.id);

// Solution 2: Parallel with Promise.all (when independent)
const [user, posts] = await Promise.all([
  fetchUser(),
  fetchPosts()
]);

// Solution 3: Locking/semaphore (for critical sections)
if (isLoading) return;  // Prevent concurrent execution
isLoading = true;
try {
  await doOperation();
} finally {
  isLoading = false;
}

// Solution 4: Debouncing (for rapid triggers)
const debouncedSearch = debounce(search, 500);
```

---

### Complex Debugging Failures

**Symptom:** Spending >2 hours debugging without progress.

**Emergency protocol:**

**Step 1: Take a break**
- Walk away for 15 minutes
- Fresh perspective helps

**Step 2: Rubber duck debugging**
```
"Explain this bug to me as if I know nothing:

What the code is supposed to do:
[explanation]

What it actually does:
[explanation]

Why I think this happens:
[hypothesis]

Walk through the code flow step by step."
```

Often explaining helps AI (and you) see the issue.

**Step 3: Binary search debugging**
```
"Let's debug systematically:

1. Does issue happen with feature X disabled?
   - Yes → Issue in feature X
   - No → Issue in interaction between features

2. Does issue happen with minimal data?
   - Yes → Not data-related
   - No → Specific data triggers it

3. Does issue happen in isolated environment?
   - Yes → Code problem
   - No → Environmental problem

Guide me through binary search to isolate the issue."
```

**Step 4: Ask for human help**
If still stuck after 3 hours:
- Ask teammate for code review
- Post on Stack Overflow (with MCVE)
- Check GitHub issues for libraries used
- Consider pair programming session

**Related:** [When to Ask for Help](../troubleshooting/README.md#when-to-ask-for-help)

---

### Test Generation Issues

#### Tests Don't Cover Edge Cases

**Symptom:** AI-generated tests only cover happy path.

**Quick fix:**
```
"Expand test coverage to include edge cases:

FUNCTION TO TEST:
[function code]

CURRENT TESTS:
[existing tests]

MISSING EDGE CASES:
- Null/undefined inputs
- Empty arrays/objects
- Boundary values (0, -1, MAX_INT)
- Invalid input types
- Concurrent calls
- Network failures
- Timeout scenarios

Add tests for all edge cases.
Target coverage: 90%+"
```

**Prevention:**
- Always specify edge cases in test prompt
- Use [Test Templates](../prompting/template-library.md#testing-templates)
- Review test coverage reports

---

#### Tests Are Too Slow

**Symptom:** Test suite takes >5 minutes to run.

**Quick diagnosis:**
```bash
# Identify slow tests
npm test -- --verbose

# Check for:
- Real API calls (should be mocked)
- Database operations (should use test DB)
- Sleep/wait statements
- Large data sets
```

**Quick fix:**
```
"Optimize slow tests:

SLOW TEST:
[test name] takes [X seconds]

CODE:
[test code]

Optimizations:
- Mock external API calls
- Use in-memory database for tests
- Reduce test data size
- Parallelize independent tests
- Remove unnecessary wait/sleep

Target: <100ms per test"
```

---

### Debugging Checklist

When debugging isn't working:

**Information gathering:**
- [ ] Full error message (not truncated)
- [ ] Complete stack trace
- [ ] Browser console output
- [ ] Network tab (failed requests)
- [ ] Reproduction steps (exact)
- [ ] Environment details
- [ ] Code at error location

**Isolation:**
- [ ] Can reproduce consistently?
- [ ] Minimal reproduction created?
- [ ] Works in isolation?
- [ ] Works in different browser?
- [ ] Works in different environment?

**Analysis:**
- [ ] Searched error message online?
- [ ] Checked framework/library issues?
- [ ] Reviewed recent code changes?
- [ ] Identified affected components?
- [ ] Formed hypothesis?

**Communication with AI:**
- [ ] Provided complete context?
- [ ] Used [Debug Template](../prompting/template-library.md#template-4-runtime-error-debugging)?
- [ ] Described expected vs actual?
- [ ] Listed what you've tried?

---

## 📋 Final Quality Assurance Checklist

**Before moving to deployment:**

**✅ Testing Complete:**
- All major features tested manually
- Automated tests passing
- Cross-browser compatibility verified
- Mobile responsiveness confirmed
- Edge cases covered

**✅ Debugging Resolved:**
- All known bugs fixed
- Console is clean (no errors)
- Network requests optimized
- Performance issues addressed
- Error handling implemented

**✅ Code Quality:**
- Code reviewed and refactored
- Security vulnerabilities addressed
- Performance optimizations applied
- Documentation updated
- Best practices followed

**✅ Ready for Production:**
- Environment variables configured
- Build processes tested
- Deployment scripts ready
- Monitoring and logging set up
- Rollback plan prepared

---

Next: [Phase 4 → Deployment](./phase-4-deployment.md)

Back: [Workflow overview](./README.md)