# Internationalization (i18n) Guide

## Overview

Internationalization (i18n) enables your site to support multiple languages and locales. This guide covers implementation strategies for Astro-based projects serving international audiences.

**When you need i18n:**
- Targeting multiple countries/languages
- Legal requirements (EU, Canada require multilingual)
- Market expansion
- Diverse user base

**When you might not:**
- Single market/language
- MVP/early stage
- Budget constraints
- Small team

## Key Concepts

### Internationalization (i18n) vs. Localization (l10n)

**Internationalization (i18n):**
- Technical implementation
- Code structure to support multiple languages
- Done once by developers

**Localization (l10n):**
- Content translation
- Cultural adaptation
- Done per language/locale

### Locale Format

**Standard format:** `language-COUNTRY`

Examples:
- `en-US` - English (United States)
- `en-GB` - English (United Kingdom)
- `es-ES` - Spanish (Spain)
- `es-MX` - Spanish (Mexico)
- `fr-FR` - French (France)
- `fr-CA` - French (Canada)
- `zh-CN` - Chinese (Simplified, China)
- `zh-TW` - Chinese (Traditional, Taiwan)
- `pt-BR` - Portuguese (Brazil)
- `pt-PT` - Portuguese (Portugal)

**Language-only:** `en`, `es`, `fr` (when country doesn't matter)

### What Needs Localization

**Content:**
- UI text (buttons, labels, menus)
- Page content (headings, paragraphs)
- Error messages
- Success messages
- Form labels and placeholders
- SEO meta tags (title, description)

**Formatting:**
- Dates and times
- Numbers
- Currency
- Phone numbers
- Addresses

**Cultural:**
- Images (people, flags, symbols)
- Colors (meanings vary by culture)
- Icons (gestures, symbols)
- Examples and references

## Astro i18n Setup
[→ See also: Core Technologies - Astro Framework](../core-technologies.md)

### Project Structure

**Approach 1: Separate Pages per Locale**

```
src/
├── pages/
│   ├── en/
│   │   ├── index.astro
│   │   ├── about.astro
│   │   └── contact.astro
│   ├── es/
│   │   ├── index.astro
│   │   ├── about.astro (sobre-nosotros.astro)
│   │   └── contact.astro (contacto.astro)
│   └── fr/
│       ├── index.astro
│       ├── about.astro (a-propos.astro)
│       └── contact.astro
```

**URLs:**
- `/en/` - English homepage
- `/es/` - Spanish homepage
- `/fr/` - French homepage

**Pros:**
- Clear separation
- Easy to manage
- Different layouts per locale

**Cons:**
- Duplicate code
- More files to maintain

**Approach 2: Dynamic Routes (Recommended)**

```
src/
├── pages/
│   └── [lang]/
│       ├── index.astro
│       ├── about.astro
│       └── contact.astro
├── i18n/
│   ├── en.json
│   ├── es.json
│   └── fr.json
└── utils/
    └── i18n.ts
```

**Pros:**
- Single code path
- Easy to add languages
- Cleaner codebase

**Cons:**
- More complex setup initially

### Configuration

**astro.config.mjs:**

```javascript
import { defineConfig } from 'astro/config';

export default defineConfig({
  i18n: {
    defaultLocale: 'en',
    locales: ['en', 'es', 'fr', 'de'],
    routing: {
      prefixDefaultLocale: false, // /en/about or /about
      redirectToDefaultLocale: true
    }
  }
});
```

**Routing options:**

```javascript
// Option 1: Prefix all locales (including default)
// URLs: /en/about, /es/about, /fr/about
{
  prefixDefaultLocale: true
}

// Option 2: No prefix for default locale (recommended)
// URLs: /about (English), /es/about, /fr/about
{
  prefixDefaultLocale: false
}
```

### Translation Files

**src/i18n/en.json:**
```json
{
  "nav": {
    "home": "Home",
    "about": "About",
    "services": "Services",
    "contact": "Contact"
  },
  "home": {
    "hero": {
      "title": "Professional Plumbing Services",
      "subtitle": "24/7 Emergency Service in Austin, TX",
      "cta": "Get Free Quote"
    },
    "features": {
      "title": "Why Choose Us",
      "licensed": "Licensed & Insured",
      "licensed_desc": "Fully licensed master plumbers",
      "fast": "Same-Day Service",
      "fast_desc": "Available 24/7 for emergencies",
      "quality": "Quality Guaranteed",
      "quality_desc": "100% satisfaction guarantee"
    }
  },
  "contact": {
    "title": "Contact Us",
    "name": "Full Name",
    "email": "Email Address",
    "phone": "Phone Number",
    "message": "Message",
    "submit": "Send Message",
    "success": "Message sent successfully!",
    "error": "Error sending message. Please try again."
  },
  "common": {
    "loading": "Loading...",
    "error": "An error occurred",
    "retry": "Try Again",
    "cancel": "Cancel",
    "save": "Save",
    "delete": "Delete",
    "edit": "Edit",
    "close": "Close"
  }
}
```

**src/i18n/es.json:**
```json
{
  "nav": {
    "home": "Inicio",
    "about": "Nosotros",
    "services": "Servicios",
    "contact": "Contacto"
  },
  "home": {
    "hero": {
      "title": "Servicios Profesionales de Plomería",
      "subtitle": "Servicio de Emergencia 24/7 en Austin, TX",
      "cta": "Cotización Gratis"
    },
    "features": {
      "title": "Por Qué Elegirnos",
      "licensed": "Licenciado y Asegurado",
      "licensed_desc": "Plomeros maestros totalmente licenciados",
      "fast": "Servicio el Mismo Día",
      "fast_desc": "Disponible 24/7 para emergencias",
      "quality": "Calidad Garantizada",
      "quality_desc": "Garantía de satisfacción 100%"
    }
  },
  "contact": {
    "title": "Contáctenos",
    "name": "Nombre Completo",
    "email": "Correo Electrónico",
    "phone": "Número de Teléfono",
    "message": "Mensaje",
    "submit": "Enviar Mensaje",
    "success": "¡Mensaje enviado exitosamente!",
    "error": "Error al enviar mensaje. Por favor intente de nuevo."
  },
  "common": {
    "loading": "Cargando...",
    "error": "Ocurrió un error",
    "retry": "Intentar de Nuevo",
    "cancel": "Cancelar",
    "save": "Guardar",
    "delete": "Eliminar",
    "edit": "Editar",
    "close": "Cerrar"
  }
}
```

### Translation Utility

**src/utils/i18n.ts:**

```typescript
import en from '../i18n/en.json';
import es from '../i18n/es.json';
import fr from '../i18n/fr.json';

export const languages = {
  en: 'English',
  es: 'Español',
  fr: 'Français'
};

export const defaultLang = 'en';

const translations = {
  en,
  es,
  fr
};

export type Language = keyof typeof translations;

export function getLangFromUrl(url: URL): Language {
  const [, lang] = url.pathname.split('/');
  if (lang in translations) return lang as Language;
  return defaultLang;
}

export function useTranslations(lang: Language) {
  return function t(key: string): string {
    const keys = key.split('.');
    let value: any = translations[lang];

    for (const k of keys) {
      value = value?.[k];
    }

    if (!value) {
      console.warn(`Translation missing: ${key} for lang: ${lang}`);
      return key;
    }

    return value;
  };
}

// Get translation with fallback
export function getTranslation(lang: Language, key: string, fallback?: string): string {
  const t = useTranslations(lang);
  const value = t(key);

  if (value === key && fallback) {
    return fallback;
  }

  return value;
}
```

### Using Translations in Components

**src/pages/[lang]/index.astro:**

```astro
---
import { getLangFromUrl, useTranslations } from '../../utils/i18n';
import Layout from '../../layouts/Layout.astro';

const lang = getLangFromUrl(Astro.url);
const t = useTranslations(lang);
---

<Layout title={t('home.hero.title')} lang={lang}>
  <main>
    <section class="hero">
      <h1>{t('home.hero.title')}</h1>
      <p>{t('home.hero.subtitle')}</p>
      <a href={`/${lang}/contact`} class="cta-button">
        {t('home.hero.cta')}
      </a>
    </section>

    <section class="features">
      <h2>{t('home.features.title')}</h2>

      <div class="feature">
        <h3>{t('home.features.licensed')}</h3>
        <p>{t('home.features.licensed_desc')}</p>
      </div>

      <div class="feature">
        <h3>{t('home.features.fast')}</h3>
        <p>{t('home.features.fast_desc')}</p>
      </div>

      <div class="feature">
        <h3>{t('home.features.quality')}</h3>
        <p>{t('home.features.quality_desc')}</p>
      </div>
    </section>
  </main>
</Layout>
```

### Language Switcher Component

**src/components/LanguageSwitcher.astro:**

```astro
---
import { languages, getLangFromUrl } from '../utils/i18n';

const currentLang = getLangFromUrl(Astro.url);
const currentPath = Astro.url.pathname.replace(`/${currentLang}`, '');
---

<div class="language-switcher">
  {Object.entries(languages).map(([lang, label]) => (
    <a
      href={`/${lang}${currentPath}`}
      class:list={['lang-link', { active: lang === currentLang }]}
      aria-current={lang === currentLang ? 'true' : undefined}
    >
      {label}
    </a>
  ))}
</div>

<style>
  .language-switcher {
    display: flex;
    gap: 0.5rem;
  }

  .lang-link {
    padding: 0.5rem 1rem;
    text-decoration: none;
    color: #333;
    border-radius: 4px;
  }

  .lang-link.active {
    background: #0066cc;
    color: white;
    font-weight: bold;
  }

  .lang-link:hover {
    background: #e0e0e0;
  }

  .lang-link.active:hover {
    background: #0052a3;
  }
</style>
```

## AI-Assisted Translation Workflows
[→ See also: Prompting Guides](../prompting/README.md)

### Initial Translation

**Prompt for AI:**

```
Translate this JSON file to Spanish (es-MX dialect):

[Paste en.json]

Requirements:
- Maintain JSON structure exactly
- Use natural, conversational Spanish
- Mexican Spanish dialect
- Professional tone for business site
- Keep placeholders intact (e.g., {name})
- Keep HTML tags intact

Provide complete translated JSON file.
```

**For multiple languages:**

```
Translate en.json to these languages:
1. Spanish (es-MX) - Mexican Spanish
2. French (fr-FR) - French from France
3. German (de-DE) - German from Germany

For each language:
- Use appropriate dialect
- Professional business tone
- Natural conversational style
- Maintain JSON structure

Provide separate JSON file for each language.
```

### Context-Aware Translation

**For better translations, provide context:**

```
Translate this contact form to Spanish:

Context:
- Plumbing business website
- Targeting homeowners in Austin, Texas
- Many customers are Spanish-speaking
- Tone: Professional but friendly, not overly formal

Content:
{
  "contact": {
    "title": "Contact Us",
    "subtitle": "Get a free quote today",
    ...
  }
}

Please translate to Mexican Spanish (es-MX).
```

### Native Speaker Review

**AI translations should be reviewed by native speakers:**

```markdown
# Translation Review Checklist

For each language:
- [ ] Grammar is correct
- [ ] Spelling is correct
- [ ] Tone matches brand (professional/casual/friendly)
- [ ] Idioms make sense in target culture
- [ ] No awkward phrasings
- [ ] No offensive terms or implications
- [ ] Technical terms translated correctly
- [ ] Call-to-actions are compelling
- [ ] Formatting is appropriate (dates, numbers, etc.)
```

**Hire native speakers for:**
- Final review of AI translations
- Cultural appropriateness check
- Tone and brand voice matching
- Technical term validation

**Budget:**
- $0.10-0.30 per word for professional translation
- Or hire reviewer on Upwork: $20-50/hour
- Or use Fiverr: $20-100 per 500 words

## RTL (Right-to-Left) Language Support

### RTL Languages

**Common RTL languages:**
- Arabic (ar)
- Hebrew (he)
- Persian/Farsi (fa)
- Urdu (ur)

### CSS Considerations

**Use logical properties:**

```css
/* ❌ Don't use directional properties */
.element {
  margin-left: 1rem;
  padding-right: 2rem;
  text-align: left;
}

/* ✅ Use logical properties */
.element {
  margin-inline-start: 1rem;
  padding-inline-end: 2rem;
  text-align: start;
}
```

**Automatic RTL:**

```css
/* Set direction on html element */
html[dir="rtl"] {
  direction: rtl;
}

html[dir="ltr"] {
  direction: ltr;
}

/* Or per-language */
html[lang="ar"],
html[lang="he"] {
  direction: rtl;
}
```

**Layout mirroring:**

```css
/* Use CSS transforms for icons */
html[dir="rtl"] .icon-arrow-right {
  transform: scaleX(-1);
}

/* Or provide RTL-specific icons */
html[dir="rtl"] .icon-arrow {
  background-image: url('/icons/arrow-left.svg');
}

html[dir="ltr"] .icon-arrow {
  background-image: url('/icons/arrow-right.svg');
}
```

### Icon Placement

**Directional icons need flipping:**

```html
<!-- Arrow icons, chevrons, etc. -->
<span class="icon" data-icon="arrow-right">→</span>

<style>
  html[dir="rtl"] [data-icon="arrow-right"]::before {
    content: "←"; /* Flip arrow */
  }
</style>
```

**Non-directional icons don't flip:**
- Search icon (🔍)
- Settings icon (⚙️)
- User icon (👤)
- Close icon (✕)

### Text Direction

```html
<!-- Set dir attribute -->
<html lang="ar" dir="rtl">

<!-- Or dynamically -->
<html lang={lang} dir={isRTL(lang) ? 'rtl' : 'ltr'}>
```

```typescript
// utils/i18n.ts
export const RTL_LANGUAGES = ['ar', 'he', 'fa', 'ur'];

export function isRTL(lang: string): boolean {
  return RTL_LANGUAGES.includes(lang);
}
```

## Formatting

### Dates and Times

**Use Intl.DateTimeFormat:**

```typescript
// utils/format.ts

export function formatDate(date: Date, lang: string): string {
  return new Intl.DateTimeFormat(lang, {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  }).format(date);
}

export function formatTime(date: Date, lang: string): string {
  return new Intl.DateTimeFormat(lang, {
    hour: 'numeric',
    minute: '2-digit',
    hour12: lang === 'en-US' // 12-hour for US, 24-hour for others
  }).format(date);
}

export function formatDateTime(date: Date, lang: string): string {
  return new Intl.DateTimeFormat(lang, {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: 'numeric',
    minute: '2-digit'
  }).format(date);
}
```

**Usage:**

```astro
---
import { formatDate } from '../utils/format';

const lang = getLangFromUrl(Astro.url);
const date = new Date();
---

<p>{formatDate(date, lang)}</p>
<!-- en: January 15, 2025 -->
<!-- es: 15 de enero de 2025 -->
<!-- fr: 15 janvier 2025 -->
```

### Numbers

```typescript
export function formatNumber(num: number, lang: string): string {
  return new Intl.NumberFormat(lang).format(num);
}

// Examples:
formatNumber(1234.56, 'en-US') // "1,234.56"
formatNumber(1234.56, 'de-DE') // "1.234,56"
formatNumber(1234.56, 'fr-FR') // "1 234,56"
```

### Currency

```typescript
export function formatCurrency(
  amount: number,
  currency: string,
  lang: string
): string {
  return new Intl.NumberFormat(lang, {
    style: 'currency',
    currency: currency
  }).format(amount);
}

// Examples:
formatCurrency(99.99, 'USD', 'en-US') // "$99.99"
formatCurrency(99.99, 'EUR', 'de-DE') // "99,99 €"
formatCurrency(99.99, 'GBP', 'en-GB') // "£99.99"
formatCurrency(99.99, 'MXN', 'es-MX') // "MX$99.99"
```

## URL Structure

### Strategies

**Option 1: Subdirectories (Recommended)**

```
example.com/          (English - default)
example.com/es/       (Spanish)
example.com/fr/       (French)
```

**Pros:**
- Easy to implement
- Good for SEO
- User-friendly URLs
- Single domain

**Cons:**
- Default language not explicit

**Option 2: Subdomain**

```
example.com           (English)
es.example.com        (Spanish)
fr.example.com        (French)
```

**Pros:**
- Clear language separation
- Can host on different servers

**Cons:**
- Multiple SSL certificates
- More DNS configuration
- Harder to manage
- Cookie sharing issues

**Option 3: Query Parameter**

```
example.com/?lang=en
example.com/?lang=es
```

**Pros:**
- Simple to implement

**Cons:**
- Poor SEO
- Not user-friendly
- Not recommended

**Option 4: TLD (Top-Level Domain)**

```
example.com    (English)
example.es     (Spanish)
example.fr     (French)
```

**Pros:**
- Strongest local SEO signal
- User trust in local domains

**Cons:**
- Expensive (multiple domains)
- Complex management
- Separate sites

## SEO for Multi-Language Sites

### Hreflang Tags

**Tell search engines about language versions:**

```astro
---
const lang = getLangFromUrl(Astro.url);
const alternates = ['en', 'es', 'fr'];
const currentPath = Astro.url.pathname.replace(`/${lang}`, '');
---

<head>
  <!-- Self-reference -->
  <link rel="alternate" hreflang={lang} href={`https://example.com/${lang}${currentPath}`} />

  <!-- Other language versions -->
  {alternates.filter(l => l !== lang).map(l => (
    <link rel="alternate" hreflang={l} href={`https://example.com/${l}${currentPath}`} />
  ))}

  <!-- Default/fallback -->
  <link rel="alternate" hreflang="x-default" href={`https://example.com/en${currentPath}`} />
</head>
```

**Results:**
```html
<link rel="alternate" hreflang="en" href="https://example.com/en/about" />
<link rel="alternate" hreflang="es" href="https://example.com/es/about" />
<link rel="alternate" hreflang="fr" href="https://example.com/fr/about" />
<link rel="alternate" hreflang="x-default" href="https://example.com/en/about" />
```

### Language-Specific Sitemaps

**Generate sitemap per language:**

```xml
<!-- sitemap-en.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/en/</loc>
    <xhtml:link rel="alternate" hreflang="es" href="https://example.com/es/" />
    <xhtml:link rel="alternate" hreflang="fr" href="https://example.com/fr/" />
  </url>
</urlset>
```

**Submit all sitemaps:**
```
https://example.com/sitemap-en.xml
https://example.com/sitemap-es.xml
https://example.com/sitemap-fr.xml
```

### Duplicate Content Handling

**Hreflang prevents duplicate content issues:**
- Google understands pages are translations
- Each language version can rank in appropriate locale
- No penalty for "duplicate" content in different languages

## Common Pitfalls

### 1. Hardcoded Strings

```astro
<!-- ❌ Hardcoded -->
<button>Submit</button>

<!-- ✅ Translated -->
<button>{t('common.submit')}</button>
```

### 2. Date Format Assumptions

```typescript
// ❌ US date format assumed
const dateString = `${month}/${day}/${year}`;

// ✅ Use Intl
const dateString = new Intl.DateTimeFormat(lang).format(date);
```

### 3. Text Expansion

**Text length varies by language:**

English: "Submit"
Spanish: "Enviar"
German: "Einreichen"
French: "Soumettre"

**Design for expansion:**
```css
/* Allow buttons to grow */
.button {
  min-width: 120px; /* Not fixed width */
  padding: 0.5rem 1rem;
  white-space: nowrap;
}
```

### 4. Cultural Insensitivity

**Images:**
- Hand gestures mean different things
- Colors have different meanings (white = death in some cultures)
- Symbols may be offensive

**Examples:**
- Thumbs up: Offensive in some Middle Eastern countries
- OK sign (👌): Offensive in some countries
- Red: Good luck (China), danger (Western countries)

**Solution:** Use culturally neutral images or localize imagery.

### 5. Concatenation

```typescript
// ❌ String concatenation
const message = `Hello ${name}, you have ${count} messages`;

// ✅ Placeholders in translations
// en.json: "greeting": "Hello {name}, you have {count} messages"
// fr.json: "greeting": "Bonjour {name}, vous avez {count} messages"

const t = useTranslations(lang);
const message = t('greeting')
  .replace('{name}', name)
  .replace('{count}', count.toString());
```

---

## Related Documentation

**Core Technologies:**
- [Core Technologies](../core-technologies.md) - Astro framework basics and setup
- [Development Tools](../development-tools/README.md) - Tools for international projects

**Quality Standards:**
- [SEO Standards](../quality-standards/seo.md) - Hreflang tags and i18n SEO optimization
- [Accessibility Standards](../quality-standards/accessibility.md) - WCAG for multiple languages
- [Performance Standards](../quality-standards/performance.md) - Optimizing multi-language sites

**Development Workflow:**
- [Prompting Guides](../prompting/README.md) - AI-assisted translation techniques
- [Workflow Phases](../workflow/README.md) - Integrating i18n into development process
- [Phase 2: Development](../workflow/phase-2-development.md) - Building multilingual features

**Business Considerations:**
- [Client Management](../business-model/client-management.md) - Pricing i18n projects
- [Business Model](../business-model/README.md) - Monetizing international services

**Troubleshooting:**
- [Troubleshooting Guide](../troubleshooting/README.md) - Common i18n issues

---

**Remember:** Start with your primary market language, add others as you expand. Don't over-engineer i18n before you need it.
