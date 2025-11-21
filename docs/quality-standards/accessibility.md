# Accessibility Standards

## Overview

Web accessibility ensures that websites and applications are usable by everyone, including people with disabilities. This guide focuses on WCAG 2.1 Level AA compliance, which is the standard required by many laws and regulations worldwide (including ADA, Section 508, and European accessibility laws).

**Why this matters for your clients:**
- **Legal compliance** - Avoid lawsuits and penalties (US ADA lawsuits cost $5,000-$30,000+ to settle)
- **Market reach** - 15% of the global population has some form of disability
- **SEO benefits** - Many accessibility practices improve search rankings
- **Better UX for everyone** - Accessible sites are easier to use for all users
- **Modern standards** - Professional sites meet accessibility standards

## The POUR Principles

WCAG is built on four foundational principles. Every accessibility requirement fits into one of these:

### 1. Perceivable
Information and UI components must be presentable to users in ways they can perceive.

**Key practices:**
- Provide text alternatives for non-text content (images, icons, audio)
- Provide captions and transcripts for video and audio
- Ensure content can be presented in different ways without losing meaning
- Make it easy to see and hear content (color contrast, text size, audio clarity)

### 2. Operable
UI components and navigation must be operable by all users.

**Key practices:**
- Make all functionality available via keyboard
- Give users enough time to read and use content
- Don't design content that causes seizures (no flashing more than 3 times per second)
- Help users navigate and find content (clear headings, skip links, breadcrumbs)
- Support multiple input methods beyond just mouse/touch

### 3. Understandable
Information and UI operation must be understandable.

**Key practices:**
- Make text readable and understandable (clear language, define jargon)
- Make content appear and operate in predictable ways
- Help users avoid and correct mistakes (clear error messages, form validation)
- Provide clear instructions and labels

### 4. Robust
Content must be robust enough to be interpreted by a wide variety of user agents, including assistive technologies.

**Key practices:**
- Use valid, semantic HTML
- Ensure compatibility with current and future assistive technologies
- Provide proper ARIA attributes when HTML semantics aren't sufficient
- Test with actual screen readers and assistive technologies

## WCAG 2.1 Level AA Compliance Checklist

This checklist covers the most important Level AA requirements. Use it when building or reviewing any website.

### Visual Design & Color

#### ✅ Color Contrast (1.4.3, 1.4.11)
- **Regular text**: Minimum 4.5:1 contrast ratio with background
- **Large text** (18pt+, or 14pt+ bold): Minimum 3:1 contrast ratio
- **UI components** (buttons, form borders, focus indicators): Minimum 3:1 contrast ratio
- **Graphics and icons**: Minimum 3:1 contrast ratio for meaningful elements

**Testing:** Use browser DevTools or online contrast checkers

**Common mistakes:**
```html
<!-- ❌ Poor contrast - light gray on white -->
<p style="color: #CCCCCC; background: #FFFFFF;">Hard to read text</p>

<!-- ✅ Good contrast - dark gray on white (7:1) -->
<p style="color: #595959; background: #FFFFFF;">Easy to read text</p>
```

#### ✅ Don't Rely on Color Alone (1.4.1)
Use multiple visual cues (color + icon, color + text, color + pattern):

```html
<!-- ❌ Color only to indicate error -->
<input type="email" style="border-color: red;">

<!-- ✅ Color + icon + error text -->
<div class="form-field">
  <input type="email" aria-invalid="true" aria-describedby="email-error">
  <p id="email-error" class="error">
    <span class="error-icon" aria-hidden="true">⚠</span>
    Please enter a valid email address
  </p>
</div>
```

#### ✅ Resize Text (1.4.4)
Text must be resizable up to 200% without loss of content or functionality:

```css
/* ✅ Use relative units, not fixed pixels */
body {
  font-size: 1rem; /* 16px default */
}

h1 {
  font-size: 2.5rem; /* Scales with user's font settings */
}

/* ❌ Avoid fixed pixel sizes for text */
.bad-text {
  font-size: 14px; /* Doesn't respect user preferences */
}
```

### Semantic HTML & Document Structure

#### ✅ Proper Heading Hierarchy (1.3.1, 2.4.6)
Headings must follow logical order (h1 → h2 → h3) without skipping levels:

```html
<!-- ✅ Correct hierarchy -->
<h1>Page Title</h1>
  <h2>Main Section</h2>
    <h3>Subsection</h3>
    <h3>Another Subsection</h3>
  <h2>Another Main Section</h2>
    <h3>Subsection</h3>

<!-- ❌ Incorrect - skips from h1 to h3 -->
<h1>Page Title</h1>
  <h3>Section</h3> <!-- Should be h2 -->
```

**Why it matters:** Screen reader users navigate by headings. A clear hierarchy helps them understand page structure.

#### ✅ Semantic HTML Elements (1.3.1, 4.1.2)
Use the correct HTML elements for their intended purpose:

```html
<!-- ✅ Semantic markup -->
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>

<main>
  <article>
    <h1>Article Title</h1>
    <p>Article content...</p>
  </article>

  <aside>
    <h2>Related Links</h2>
    <ul>...</ul>
  </aside>
</main>

<footer>
  <p>&copy; 2025 Company Name</p>
</footer>

<!-- ❌ Non-semantic divs -->
<div class="nav">
  <div class="nav-item">Home</div>
  <div class="nav-item">About</div>
</div>
```

**Key semantic elements:**
- `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`
- `<button>` for clickable actions (not `<div onclick="">`)
- `<a>` for navigation (not `<div>` or `<span>`)
- `<ul>`/`<ol>` for lists
- `<table>` for tabular data (not for layout)

#### ✅ Landmarks and Page Regions (1.3.1, 2.4.1)
Use ARIA landmarks to define page regions:

```html
<!-- ✅ Clear page structure with landmarks -->
<body>
  <a href="#main" class="skip-link">Skip to main content</a>

  <header role="banner">
    <nav aria-label="Main navigation">...</nav>
  </header>

  <main id="main" role="main">
    <h1>Page Title</h1>
    <!-- Main content -->
  </main>

  <aside role="complementary" aria-label="Sidebar">
    <!-- Sidebar content -->
  </aside>

  <footer role="contentinfo">
    <!-- Footer content -->
  </footer>
</body>
```

### Keyboard Navigation

#### ✅ Keyboard Accessible (2.1.1, 2.1.2)
All interactive elements must be accessible via keyboard (Tab, Enter, Space, Arrow keys):

**Testing checklist:**
1. Can you Tab through all interactive elements?
2. Is the focus order logical?
3. Can you activate buttons/links with Enter or Space?
4. Can you close modals with Escape?
5. Can you navigate dropdowns with arrow keys?
6. Are there no keyboard traps (you can always Tab out)?

```html
<!-- ✅ Keyboard accessible button -->
<button onclick="submitForm()">Submit</button>

<!-- ❌ Not keyboard accessible -->
<div onclick="submitForm()">Submit</div>

<!-- ✅ Make divs keyboard accessible (if you must use div) -->
<div role="button" tabindex="0" onclick="submitForm()"
     onkeydown="if(event.key==='Enter'||event.key===' ')submitForm()">
  Submit
</div>
```

#### ✅ Visible Focus Indicator (2.4.7)
Users must be able to see which element has keyboard focus:

```css
/* ✅ Clear focus indicator */
a:focus,
button:focus,
input:focus {
  outline: 3px solid #0066cc;
  outline-offset: 2px;
}

/* ❌ NEVER remove focus outlines without replacement */
*:focus {
  outline: none; /* Don't do this! */
}

/* ✅ Custom focus style (if you don't like browser default) */
.custom-button:focus {
  outline: 3px solid #0066cc;
  box-shadow: 0 0 0 4px rgba(0, 102, 204, 0.2);
}
```

**Tailwind CSS approach:**
```html
<button class="focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-offset-2">
  Click Me
</button>
```

#### ✅ Skip Links (2.4.1)
Provide a way for keyboard users to skip repetitive content:

```html
<!-- ✅ Skip link (first focusable element on page) -->
<a href="#main" class="skip-link">Skip to main content</a>

<style>
  .skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: #000;
    color: #fff;
    padding: 8px 16px;
    text-decoration: none;
    z-index: 100;
  }

  .skip-link:focus {
    top: 0;
  }
</style>
```

### Images & Alternative Text

#### ✅ Alt Text for Images (1.1.1)
Every `<img>` must have an `alt` attribute:

```html
<!-- ✅ Informative image - describe what's important -->
<img src="chart.png" alt="Sales increased 25% from Q1 to Q2">

<!-- ✅ Functional image (e.g., button/link) - describe function -->
<a href="/search">
  <img src="search-icon.png" alt="Search">
</a>

<!-- ✅ Decorative image - empty alt -->
<img src="decorative-border.png" alt="">

<!-- ❌ Missing alt -->
<img src="important-chart.png">

<!-- ❌ Redundant alt -->
<img src="photo.jpg" alt="Image of a photo showing...">
<!-- Better: -->
<img src="photo.jpg" alt="Team celebrating product launch in office">
```

**Alt text guidelines:**
- **Be concise** - Aim for under 150 characters
- **Don't start with "Image of" or "Picture of"** - screen readers already announce it's an image
- **Describe the content and function** - What information does the image convey?
- **Context matters** - Alt text should fit the surrounding content
- **Decorative images** - Use `alt=""` (not missing alt attribute)
- **Complex images** - Consider using `longdesc` or nearby text description

#### ✅ SVG Accessibility
```html
<!-- ✅ Accessible SVG icon -->
<svg role="img" aria-labelledby="icon-title">
  <title id="icon-title">Settings</title>
  <path d="..."/>
</svg>

<!-- ✅ Decorative SVG -->
<svg aria-hidden="true" focusable="false">
  <path d="..."/>
</svg>
```

### Forms & Input

#### ✅ Form Labels (1.3.1, 3.3.2)
Every input must have a visible, associated label:

```html
<!-- ✅ Proper label association -->
<label for="email">Email Address</label>
<input type="email" id="email" name="email" required>

<!-- ✅ Alternative: wrap input in label -->
<label>
  Email Address
  <input type="email" name="email" required>
</label>

<!-- ❌ Missing label -->
<input type="email" placeholder="Email"> <!-- Placeholder is not a label! -->

<!-- ✅ If you must hide label visually (rare!) -->
<label for="search" class="sr-only">Search</label>
<input type="search" id="search" placeholder="Search...">
```

**Screen reader only class:**
```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
```

#### ✅ Required Field Indication (3.3.2)
Clearly indicate required fields:

```html
<!-- ✅ Multiple indicators -->
<label for="name">
  Full Name <span class="required" aria-label="required">*</span>
</label>
<input type="text" id="name" required aria-required="true">

<!-- ✅ Text indicator -->
<label for="phone">Phone Number (required)</label>
<input type="tel" id="phone" required aria-required="true">
```

#### ✅ Error Messages (3.3.1, 3.3.3)
Provide clear, specific error messages:

```html
<!-- ✅ Accessible error message -->
<div class="form-field">
  <label for="email">Email Address</label>
  <input
    type="email"
    id="email"
    aria-invalid="true"
    aria-describedby="email-error"
  >
  <p id="email-error" class="error-message" role="alert">
    Please enter a valid email address (e.g., name@example.com)
  </p>
</div>

<!-- ❌ Vague error -->
<p>Invalid input</p> <!-- Which field? What's wrong? How to fix? -->

<!-- ✅ Good error -->
<p>Email address must include @ symbol and domain (e.g., name@example.com)</p>
```

**Error summary for forms with multiple errors:**
```html
<div role="alert" class="error-summary">
  <h2>There are 3 errors in this form</h2>
  <ul>
    <li><a href="#email">Email address is required</a></li>
    <li><a href="#password">Password must be at least 8 characters</a></li>
    <li><a href="#terms">You must accept the terms and conditions</a></li>
  </ul>
</div>
```

#### ✅ Input Purpose (1.3.5)
Use autocomplete attributes to identify input purpose:

```html
<form>
  <label for="name">Full Name</label>
  <input type="text" id="name" autocomplete="name">

  <label for="email">Email</label>
  <input type="email" id="email" autocomplete="email">

  <label for="tel">Phone</label>
  <input type="tel" id="tel" autocomplete="tel">

  <label for="street">Street Address</label>
  <input type="text" id="street" autocomplete="street-address">

  <label for="city">City</label>
  <input type="text" id="city" autocomplete="address-level2">

  <label for="zip">ZIP Code</label>
  <input type="text" id="zip" autocomplete="postal-code">
</form>
```

### ARIA (Accessible Rich Internet Applications)

ARIA fills gaps where HTML semantics aren't sufficient. **Rule #1: Don't use ARIA if HTML semantics work.**

#### Common ARIA Attributes

**aria-label** - Provides an accessible name:
```html
<button aria-label="Close dialog">×</button>
<nav aria-label="Main navigation">...</nav>
```

**aria-labelledby** - References another element for the accessible name:
```html
<section aria-labelledby="section-title">
  <h2 id="section-title">About Us</h2>
  ...
</section>
```

**aria-describedby** - Provides additional description:
```html
<input
  type="password"
  aria-describedby="password-requirements"
>
<p id="password-requirements">
  Must be at least 8 characters with 1 number and 1 special character
</p>
```

**aria-hidden** - Hides content from screen readers:
```html
<!-- Decorative icon, don't announce -->
<span class="icon" aria-hidden="true">★</span>
<span>Featured</span>
```

**aria-live** - Announces dynamic content changes:
```html
<!-- Polite: wait for user to pause -->
<div aria-live="polite" aria-atomic="true" class="status-message">
  <!-- Status messages appear here -->
</div>

<!-- Assertive: interrupt immediately -->
<div aria-live="assertive" role="alert">
  <!-- Critical errors appear here -->
</div>
```

**aria-expanded** - Indicates if element is expanded:
```html
<button
  aria-expanded="false"
  aria-controls="dropdown-menu"
  onclick="toggleDropdown()"
>
  Menu
</button>
<ul id="dropdown-menu" hidden>
  <li><a href="/home">Home</a></li>
  <li><a href="/about">About</a></li>
</ul>
```

**aria-current** - Indicates current item:
```html
<nav>
  <a href="/home" aria-current="page">Home</a>
  <a href="/about">About</a>
  <a href="/contact">Contact</a>
</nav>
```

#### ✅ ARIA Live Regions
For dynamic content updates:

```html
<!-- Status messages (polite) -->
<div role="status" aria-live="polite" aria-atomic="true">
  <!-- "5 items added to cart" -->
</div>

<!-- Urgent alerts (assertive) -->
<div role="alert" aria-live="assertive">
  <!-- "Error: Payment failed" -->
</div>

<!-- Loading indicators -->
<div aria-live="polite" aria-busy="true">
  Loading...
</div>
```

### Interactive Components

#### ✅ Modal Dialogs (2.4.3)
```html
<div
  role="dialog"
  aria-modal="true"
  aria-labelledby="dialog-title"
  class="modal"
>
  <h2 id="dialog-title">Confirm Action</h2>
  <p>Are you sure you want to delete this item?</p>
  <button onclick="confirmDelete()">Delete</button>
  <button onclick="closeDialog()">Cancel</button>
</div>

<script>
// Accessibility requirements for modals:
// 1. Focus trap - Tab cycles within modal
// 2. Close on Escape key
// 3. Focus management - focus first focusable element on open
// 4. Return focus to trigger element on close
// 5. Prevent background scrolling
// 6. aria-modal="true" to hide background from screen readers
</script>
```

#### ✅ Dropdown Menus
```html
<div class="dropdown">
  <button
    aria-expanded="false"
    aria-haspopup="true"
    aria-controls="menu-list"
    id="menu-button"
  >
    Options
  </button>

  <ul id="menu-list" role="menu" hidden>
    <li role="none">
      <a href="/profile" role="menuitem">Profile</a>
    </li>
    <li role="none">
      <a href="/settings" role="menuitem">Settings</a>
    </li>
    <li role="none">
      <a href="/logout" role="menuitem">Logout</a>
    </li>
  </ul>
</div>

<script>
// Keyboard requirements:
// - Arrow keys navigate menu items
// - Enter activates item
// - Escape closes menu
// - Tab closes menu and moves to next element
</script>
```

#### ✅ Accordions
```html
<div class="accordion">
  <h3>
    <button
      aria-expanded="false"
      aria-controls="panel1"
      id="accordion1"
    >
      Section 1
    </button>
  </h3>
  <div id="panel1" role="region" aria-labelledby="accordion1" hidden>
    <p>Content for section 1...</p>
  </div>

  <h3>
    <button
      aria-expanded="false"
      aria-controls="panel2"
      id="accordion2"
    >
      Section 2
    </button>
  </h3>
  <div id="panel2" role="region" aria-labelledby="accordion2" hidden>
    <p>Content for section 2...</p>
  </div>
</div>
```

#### ✅ Tabs
```html
<div class="tabs">
  <div role="tablist" aria-label="Content sections">
    <button role="tab" aria-selected="true" aria-controls="panel1" id="tab1">
      Tab 1
    </button>
    <button role="tab" aria-selected="false" aria-controls="panel2" id="tab2">
      Tab 2
    </button>
    <button role="tab" aria-selected="false" aria-controls="panel3" id="tab3">
      Tab 3
    </button>
  </div>

  <div role="tabpanel" id="panel1" aria-labelledby="tab1">
    Content for tab 1
  </div>
  <div role="tabpanel" id="panel2" aria-labelledby="tab2" hidden>
    Content for tab 2
  </div>
  <div role="tabpanel" id="panel3" aria-labelledby="tab3" hidden>
    Content for tab 3
  </div>
</div>

<script>
// Keyboard requirements:
// - Arrow keys move between tabs
// - Tab key moves into panel content
// - Home/End jump to first/last tab
</script>
```

## Astro-Specific Accessibility Patterns

### Accessible Astro Components

```astro
---
// src/components/AccessibleButton.astro
interface Props {
  variant?: 'primary' | 'secondary';
  type?: 'button' | 'submit' | 'reset';
  ariaLabel?: string;
  disabled?: boolean;
}

const { variant = 'primary', type = 'button', ariaLabel, disabled = false } = Astro.props;
---

<button
  type={type}
  class={`btn btn-${variant}`}
  aria-label={ariaLabel}
  disabled={disabled}
>
  <slot />
</button>

<style>
  .btn {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
  }

  .btn:focus {
    outline: 3px solid #0066cc;
    outline-offset: 2px;
  }

  .btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  .btn-primary {
    background: #0066cc;
    color: white;
  }

  .btn-secondary {
    background: #6c757d;
    color: white;
  }
</style>
```

### Accessible Navigation Component

```astro
---
// src/components/Navigation.astro
const currentPath = Astro.url.pathname;
const navItems = [
  { href: '/', label: 'Home' },
  { href: '/about', label: 'About' },
  { href: '/services', label: 'Services' },
  { href: '/contact', label: 'Contact' },
];
---

<nav aria-label="Main navigation">
  <ul>
    {navItems.map(item => (
      <li>
        <a
          href={item.href}
          aria-current={currentPath === item.href ? 'page' : undefined}
        >
          {item.label}
        </a>
      </li>
    ))}
  </ul>
</nav>

<style>
  nav ul {
    list-style: none;
    display: flex;
    gap: 1rem;
    margin: 0;
    padding: 0;
  }

  nav a {
    color: #333;
    text-decoration: none;
    padding: 0.5rem 1rem;
  }

  nav a:focus {
    outline: 3px solid #0066cc;
    outline-offset: 2px;
  }

  nav a[aria-current="page"] {
    font-weight: bold;
    border-bottom: 2px solid #0066cc;
  }
</style>
```

### Accessible Modal Component

```astro
---
// src/components/Modal.astro
interface Props {
  id: string;
  title: string;
}

const { id, title } = Astro.props;
---

<div id={id} class="modal-backdrop" aria-hidden="true">
  <div
    role="dialog"
    aria-modal="true"
    aria-labelledby={`${id}-title`}
    class="modal"
  >
    <div class="modal-header">
      <h2 id={`${id}-title`}>{title}</h2>
      <button
        class="close-button"
        aria-label="Close dialog"
        data-close-modal={id}
      >
        ×
      </button>
    </div>
    <div class="modal-body">
      <slot />
    </div>
  </div>
</div>

<script>
  // Focus trap and keyboard handling
  document.addEventListener('DOMContentLoaded', () => {
    const modals = document.querySelectorAll('[role="dialog"]');

    modals.forEach(modal => {
      const backdrop = modal.closest('.modal-backdrop');
      const closeButton = modal.querySelector('[data-close-modal]');

      // Close on Escape
      document.addEventListener('keydown', (e) => {
        if (e.key === 'Escape' && backdrop?.getAttribute('aria-hidden') === 'false') {
          closeModal(backdrop);
        }
      });

      // Close button
      closeButton?.addEventListener('click', () => {
        if (backdrop) closeModal(backdrop);
      });
    });
  });

  function closeModal(backdrop: Element) {
    backdrop.setAttribute('aria-hidden', 'true');
    // Return focus to trigger element
    const triggerId = backdrop.getAttribute('data-trigger');
    if (triggerId) {
      document.getElementById(triggerId)?.focus();
    }
  }
</script>

<style>
  .modal-backdrop {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
  }

  .modal-backdrop[aria-hidden="true"] {
    display: none;
  }

  .modal {
    background: white;
    border-radius: 8px;
    max-width: 500px;
    width: 90%;
    max-height: 90vh;
    overflow-y: auto;
  }

  .close-button {
    font-size: 2rem;
    border: none;
    background: none;
    cursor: pointer;
    padding: 0.5rem;
  }

  .close-button:focus {
    outline: 3px solid #0066cc;
    outline-offset: 2px;
  }
</style>
```

### Accessible Form Component

```astro
---
// src/components/ContactForm.astro
---

<form class="contact-form" method="POST">
  <div class="form-field">
    <label for="name">
      Full Name <span class="required" aria-label="required">*</span>
    </label>
    <input
      type="text"
      id="name"
      name="name"
      required
      aria-required="true"
      autocomplete="name"
    >
  </div>

  <div class="form-field">
    <label for="email">
      Email Address <span class="required" aria-label="required">*</span>
    </label>
    <input
      type="email"
      id="email"
      name="email"
      required
      aria-required="true"
      autocomplete="email"
    >
  </div>

  <div class="form-field">
    <label for="phone">Phone Number</label>
    <input
      type="tel"
      id="phone"
      name="phone"
      autocomplete="tel"
    >
  </div>

  <div class="form-field">
    <label for="message">
      Message <span class="required" aria-label="required">*</span>
    </label>
    <textarea
      id="message"
      name="message"
      rows="5"
      required
      aria-required="true"
    ></textarea>
  </div>

  <button type="submit">Send Message</button>
</form>

<div role="status" aria-live="polite" class="form-status"></div>

<style>
  .form-field {
    margin-bottom: 1rem;
  }

  label {
    display: block;
    margin-bottom: 0.25rem;
    font-weight: 500;
  }

  .required {
    color: #dc3545;
  }

  input, textarea {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 1rem;
  }

  input:focus, textarea:focus {
    outline: 3px solid #0066cc;
    outline-offset: 2px;
    border-color: #0066cc;
  }

  input[aria-invalid="true"], textarea[aria-invalid="true"] {
    border-color: #dc3545;
  }

  button {
    background: #0066cc;
    color: white;
    padding: 0.75rem 1.5rem;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
  }

  button:focus {
    outline: 3px solid #0066cc;
    outline-offset: 2px;
  }
</style>
```

## AI-Assisted Accessibility

### Prompts for Generating Accessible Code

#### Initial Component Creation
```
Create an accessible [component type] component for Astro that:
- Follows WCAG 2.1 Level AA standards
- Includes proper ARIA attributes
- Has full keyboard navigation support
- Includes visible focus indicators
- Works with screen readers
- Has semantic HTML structure

Requirements:
[List specific requirements]

Please include comments explaining the accessibility features.
```

#### Accessibility Review Prompt
```
Review this code for WCAG 2.1 Level AA accessibility compliance:

[Paste code]

Check for:
1. Semantic HTML usage
2. Keyboard navigation
3. ARIA attributes (proper usage, not over-use)
4. Focus management
5. Color contrast (if styles present)
6. Alternative text for images
7. Form labels and error messages
8. Heading hierarchy

Provide specific fixes for any issues found.
```

#### Form Accessibility Prompt
```
Create an accessible form for [purpose] that includes:
- Proper label associations for all inputs
- Clear required field indicators
- Input purpose (autocomplete attributes)
- Client-side validation with accessible error messages
- Error summary at top of form
- ARIA live regions for dynamic messages
- Keyboard accessible submit button

Follow WCAG 2.1 Level AA standards.
```

#### Interactive Component Prompt
```
Create an accessible [modal/dropdown/accordion/tabs] component that:
- Has proper ARIA roles and attributes
- Implements keyboard navigation (specify keys)
- Manages focus appropriately
- Announces state changes to screen readers
- Works without JavaScript as fallback
- Includes visible focus indicators

Use vanilla JavaScript or specify if you want a framework.
```

### AI Accessibility Review Workflow

**Step 1: Initial Generation**
- Use AI to generate component with accessibility requirements in prompt
- Request comments explaining accessibility features

**Step 2: Automated Testing**
- Run Lighthouse accessibility audit
- Run axe DevTools scan
- Check with WAVE extension

**Step 3: AI Review**
- Ask AI to review code for accessibility issues
- Provide context about any automated tool warnings
- Request specific fixes

**Step 4: Manual Testing**
- Test keyboard navigation yourself
- Test with actual screen reader (NVDA/VoiceOver)
- Verify color contrast with tools
- Test form validation

**Step 5: Iterative Improvement**
- Document any issues found
- Use AI to fix specific problems
- Retest after fixes

### Context for AI Accessibility Work

Include this in your .cursorrules or project context:

```
# Accessibility Standards

All code must meet WCAG 2.1 Level AA standards:

## Always include:
- Semantic HTML (header, nav, main, article, section, aside, footer)
- Proper heading hierarchy (h1-h6, no skipped levels)
- Alt text for all images (empty alt="" for decorative)
- Form labels for all inputs (using <label for="id">)
- Keyboard accessibility (all interactive elements focusable)
- Visible focus indicators (outline or custom focus styles)
- ARIA attributes only when HTML semantics insufficient
- Color contrast: 4.5:1 for text, 3:1 for large text and UI components

## Never do:
- Remove focus outlines without replacement
- Use divs/spans for buttons (use <button>)
- Skip heading levels
- Rely on color alone to convey information
- Use placeholder as label replacement
- Create keyboard traps
- Use positive tabindex values (tabindex="1", "2", etc.)

## Test with:
- Keyboard only (Tab, Enter, Space, Escape, Arrow keys)
- Screen reader (NVDA on Windows, VoiceOver on Mac)
- Lighthouse accessibility audit (target: 100 score)
- axe DevTools
```

## Testing Tools & Workflow

### Browser DevTools - Chrome Lighthouse

**How to run:**
1. Open Chrome DevTools (F12)
2. Click "Lighthouse" tab
3. Select "Accessibility" category
4. Choose "Desktop" or "Mobile"
5. Click "Analyze page load"

**Target score:** 95-100 (100 is ideal)

**Common issues found:**
- Missing alt text
- Low color contrast
- Missing form labels
- Missing ARIA attributes
- Incorrect heading order

### axe DevTools

**Installation:** Chrome/Firefox/Edge extension (free)

**How to use:**
1. Install extension
2. Open DevTools
3. Click "axe DevTools" tab
4. Click "Scan ALL of my page"
5. Review issues by severity (Critical, Serious, Moderate, Minor)

**Benefits:**
- Catches ~57% of WCAG issues automatically
- Provides specific fixes for each issue
- Highlights affected elements in page
- Export reports for clients

### WAVE Browser Extension

**Installation:** Chrome/Firefox/Edge extension (free)

**How to use:**
1. Install extension
2. Click WAVE icon in toolbar
3. Review color-coded annotations on page
4. Check sidebar for summary

**What it shows:**
- Errors (red) - must fix
- Alerts (yellow) - review needed
- Features (green) - accessibility features present
- Structural elements
- ARIA usage

### Screen Reader Testing

#### Windows: NVDA (Free)

**Download:** https://www.nvaccess.org/download/

**Basic commands:**
- **Ctrl** - Stop reading
- **Insert + Down Arrow** - Read all
- **H** - Next heading
- **Shift + H** - Previous heading
- **K** - Next link
- **B** - Next button
- **F** - Next form field
- **Tab** - Next interactive element

#### Mac: VoiceOver (Built-in)

**Activate:** Cmd + F5

**Basic commands:**
- **VO keys** - Control + Option (held together)
- **VO + A** - Start reading
- **VO + Right Arrow** - Next item
- **VO + Left Arrow** - Previous item
- **VO + Space** - Activate element
- **VO + U** - Open rotor (headings, links, etc.)

#### Testing checklist:
1. Can you navigate the entire page with screen reader?
2. Are all images described appropriately?
3. Are form fields labeled clearly?
4. Do error messages announce?
5. Can you understand page structure from headings?
6. Are button/link purposes clear?
7. Do dynamic updates announce (ARIA live regions)?

### Manual Keyboard Testing

**Test with keyboard only (no mouse):**

1. **Tab through page**
   - All interactive elements reachable?
   - Focus order logical?
   - Focus visible on all elements?

2. **Test interactive elements**
   - Buttons activate with Enter/Space?
   - Links activate with Enter?
   - Dropdowns open with Enter/Space?
   - Dropdowns navigate with Arrow keys?

3. **Test modals**
   - Open with keyboard?
   - Close with Escape?
   - Focus trapped inside modal?
   - Focus returns to trigger on close?

4. **Test forms**
   - All fields reachable with Tab?
   - Can submit with Enter?
   - Error messages appear and are reachable?
   - Can correct errors with keyboard?

5. **Test custom components**
   - Accordions open/close with Enter?
   - Tabs switch with Arrow keys?
   - Carousels navigate with Arrow keys?
   - All functionality available via keyboard?

### Color Contrast Testing

**Tools:**
- **Chrome DevTools** - Inspect element → Color picker shows contrast ratio
- **WebAIM Contrast Checker** - https://webaim.org/resources/contrastchecker/
- **Colour Contrast Analyzer** - Desktop app (Windows/Mac)

**Requirements:**
- Regular text: 4.5:1 minimum
- Large text (18pt+ or 14pt+ bold): 3:1 minimum
- UI components and graphics: 3:1 minimum

**Common issues:**
- Light gray text on white background
- Colored text on colored backgrounds
- Button borders and focus indicators
- Link colors

### Automated Testing in CI/CD

**Lighthouse CI:**
```bash
# Install
npm install -g @lhci/cli

# Run
lhci autorun --collect.url=http://localhost:3000

# In GitHub Actions
- name: Lighthouse CI
  run: |
    npm install -g @lhci/cli
    lhci autorun
```

**axe-core (Playwright/Cypress):**
```javascript
// Playwright
import { test, expect } from '@playwright/test';
import AxeBuilder from '@axe-core/playwright';

test('should not have accessibility violations', async ({ page }) => {
  await page.goto('http://localhost:3000');

  const accessibilityScanResults = await new AxeBuilder({ page }).analyze();

  expect(accessibilityScanResults.violations).toEqual([]);
});
```

**Pa11y:**
```bash
# Install
npm install -g pa11y

# Run
pa11y http://localhost:3000

# With specific standards
pa11y --standard WCAG2AA http://localhost:3000
```

## Common Accessibility Pitfalls in AI-Generated Code

### Pitfall #1: Div Buttons
```html
<!-- ❌ AI often generates this -->
<div class="button" onclick="submit()">Submit</div>

<!-- ✅ Fix -->
<button onclick="submit()">Submit</button>
```

**Why it's wrong:** Divs aren't keyboard accessible, aren't announced as buttons, don't support Enter/Space keys.

### Pitfall #2: Missing Form Labels
```html
<!-- ❌ AI generates placeholder as "label" -->
<input type="email" placeholder="Email Address">

<!-- ✅ Fix -->
<label for="email">Email Address</label>
<input type="email" id="email" placeholder="you@example.com">
```

**Why it's wrong:** Placeholders disappear on input, aren't accessible labels, cause usability issues.

### Pitfall #3: Poor Color Contrast
```css
/* ❌ AI often suggests trendy but inaccessible colors */
.text {
  color: #999; /* Light gray */
  background: #fff; /* White */
}
/* Contrast: 2.8:1 - FAILS WCAG */

/* ✅ Fix */
.text {
  color: #666; /* Darker gray */
  background: #fff;
}
/* Contrast: 5.7:1 - PASSES WCAG */
```

### Pitfall #4: Over-using ARIA
```html
<!-- ❌ AI adds unnecessary ARIA -->
<button role="button" aria-label="Submit">Submit</button>

<!-- ✅ Fix - HTML semantics sufficient -->
<button>Submit</button>
```

**Why it's wrong:** Redundant ARIA adds complexity. First rule of ARIA: Don't use ARIA if HTML works.

### Pitfall #5: Missing Alt Text
```html
<!-- ❌ AI generates images without alt -->
<img src="product.jpg">

<!-- ✅ Fix -->
<img src="product.jpg" alt="Premium leather wallet in brown">
```

### Pitfall #6: No Focus Indicators
```css
/* ❌ AI generates "clean" designs */
* {
  outline: none;
}

/* ✅ Fix - always have visible focus */
*:focus {
  outline: 3px solid #0066cc;
  outline-offset: 2px;
}
```

### Pitfall #7: Skipped Heading Levels
```html
<!-- ❌ AI jumps heading levels -->
<h1>Page Title</h1>
<h3>Section</h3> <!-- Skipped h2 -->

<!-- ✅ Fix -->
<h1>Page Title</h1>
<h2>Section</h2>
```

### Pitfall #8: Click Events on Non-Interactive Elements
```html
<!-- ❌ AI adds click handlers to spans/divs -->
<span onclick="openModal()">Click here</span>

<!-- ✅ Fix -->
<button onclick="openModal()">Click here</button>
```

### Pitfall #9: Missing Error Announcements
```javascript
// ❌ AI shows error visually only
function showError(message) {
  document.getElementById('error').textContent = message;
}

// ✅ Fix - announce to screen readers
function showError(message) {
  const errorEl = document.getElementById('error');
  errorEl.textContent = message;
  errorEl.setAttribute('role', 'alert'); // Announces immediately
}
```

### Pitfall #10: Inaccessible Modals
```html
<!-- ❌ AI creates modal without accessibility -->
<div class="modal">
  <h2>Modal Title</h2>
  <button onclick="close()">×</button>
</div>

<!-- ✅ Fix -->
<div
  role="dialog"
  aria-modal="true"
  aria-labelledby="modal-title"
>
  <h2 id="modal-title">Modal Title</h2>
  <button onclick="close()" aria-label="Close dialog">×</button>
</div>
<!-- Plus: focus management, escape key, focus trap -->
```

## Communicating Accessibility Benefits to Clients

### The Business Case

**Legal risk:**
> "Web accessibility lawsuits have increased 300% since 2018. In the US, settlements typically cost $5,000-$30,000 plus attorney fees. The Americans with Disabilities Act (ADA) requires accessible websites for businesses. Building accessibility in from the start costs far less than retrofitting later or defending a lawsuit."

**Market reach:**
> "15% of the world's population (1 billion people) has some form of disability. That's 15% of your potential customers who may struggle to use your site if it's not accessible. Additionally, many accessibility features benefit all users - like clear headings, good color contrast, and keyboard navigation."

**SEO benefits:**
> "Google prioritizes accessible websites in search results. Many accessibility best practices - like semantic HTML, descriptive headings, alt text for images, and fast loading times - directly improve your search rankings. An accessible site is often a better-optimized site."

**Better UX for everyone:**
> "Accessibility features benefit all users, not just people with disabilities:
> - Clear contrast helps people in bright sunlight
> - Keyboard navigation helps power users
> - Clear error messages help everyone fix mistakes
> - Captions help people in noisy or quiet environments
> - Simple language helps non-native speakers"

**Competitive advantage:**
> "Most small business websites have poor accessibility. By meeting these standards, you'll provide a better experience than your competitors. This is especially important for local businesses where customer experience is a key differentiator."

### Explaining the Cost

**Initial development:**
> "Building accessibility in from the start adds approximately 10-15% to development time, but costs significantly less than retrofitting later (which can add 30-50% or more). I include basic accessibility in all projects at no extra cost, as it's part of modern web development standards."

**Ongoing value:**
> "An accessible site requires less rework over time. You won't need to rebuild components to meet accessibility requirements later. It also reduces support requests from users who can't complete actions on your site."

### What to Include vs. Upsell

**Base package (included):**
- Semantic HTML structure
- Proper heading hierarchy
- Form labels and error messages
- Keyboard navigation for all interactive elements
- Color contrast meeting WCAG standards
- Alt text for images (client provides descriptions)
- Basic ARIA where needed
- Lighthouse accessibility score 90+

**Premium accessibility package (upsell):**
- WCAG 2.1 Level AA compliance audit and certification
- Advanced screen reader optimization
- Accessibility statement page
- Comprehensive testing with multiple screen readers
- Accessibility training for client's content team
- Ongoing accessibility monitoring
- VPAT (Voluntary Product Accessibility Template) documentation for B2B/government clients

### Sample Client Conversation

**Client:** "Do I really need to pay extra for accessibility?"

**You:** "Actually, I include basic accessibility in all my projects - it's part of professional web development standards. This includes semantic HTML, keyboard navigation, proper contrast, and form labels. Your site will score 90+ on accessibility audits at no extra cost.

The premium accessibility package is optional and mainly relevant if you need:
- Legal documentation for compliance (government contracts, etc.)
- Certification for WCAG 2.1 AA compliance
- Advanced optimization for screen readers

For most small businesses, the included accessibility features are sufficient and provide great value:
- You avoid legal risk
- Your site works for all customers
- Your SEO improves
- The user experience is better for everyone

It's a win-win situation."

## Resources & Further Learning

### Official Documentation
- **WCAG 2.1 Guidelines** - https://www.w3.org/WAI/WCAG21/quickref/
- **MDN Accessibility** - https://developer.mozilla.org/en-US/docs/Web/Accessibility
- **WebAIM Resources** - https://webaim.org/resources/

### Testing Tools
- **Lighthouse** - Built into Chrome DevTools
- **axe DevTools** - https://www.deque.com/axe/devtools/
- **WAVE** - https://wave.webaim.org/
- **NVDA Screen Reader** - https://www.nvaccess.org/download/
- **Colour Contrast Analyzer** - https://www.tpgi.com/color-contrast-checker/

### Checklists
- **WebAIM WCAG 2 Checklist** - https://webaim.org/standards/wcag/checklist
- **A11y Project Checklist** - https://www.a11yproject.com/checklist/

### ARIA Patterns
- **WAI-ARIA Authoring Practices** - https://www.w3.org/WAI/ARIA/apg/patterns/

## Cross-References

**Related documentation:**
- [Testing & Debugging Workflow](../workflow/phase-3-testing-debugging.md) - Accessibility testing workflows
- [Client Management](../business-model/client-management.md) - Communicating accessibility value to clients
- [Quality Standards Overview](./README.md) - Back to quality standards home
- [SEO Standards](./seo.md) - Accessibility's impact on SEO
- [Performance Standards](./performance.md) - Performance and accessibility overlap

---

**Remember:** Accessibility is not optional. It's a legal requirement, a best practice, and the right thing to do. Build it in from the start - it's easier and cheaper than fixing it later.
