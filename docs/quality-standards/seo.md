# SEO Standards & Best Practices

## Overview

This guide covers comprehensive SEO (Search Engine Optimization) according to Google's latest standards and best practices. SEO is critical for small business clients who depend on organic search traffic to find customers.

**Why SEO matters for your clients:**
- **Free traffic** - Organic search is the #1 traffic source for most small businesses
- **High intent leads** - People searching have purchase intent
- **Long-term ROI** - SEO compounds over time, unlike paid ads
- **Local discovery** - "Near me" searches drive foot traffic to physical businesses
- **Competitive advantage** - Many local businesses have poor SEO

**SEO fundamentals:**
- **On-page SEO** - Content, HTML, meta tags (this guide)
- **Technical SEO** - Site speed, mobile-friendliness, structure
- **Off-page SEO** - Backlinks, citations, reviews (client's responsibility)
- **Local SEO** - Google Business Profile, local keywords, NAP consistency

## HTML Meta Tags

Meta tags provide information about your page to search engines and social media platforms.

### Essential Meta Tags

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Character encoding (required) -->
  <meta charset="UTF-8">

  <!-- Viewport (required for mobile) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Title (most important meta tag) -->
  <title>Professional Plumbing Services in Austin, TX | Smith Plumbing</title>

  <!-- Meta description (appears in search results) -->
  <meta name="description" content="Smith Plumbing provides 24/7 emergency plumbing services in Austin, TX. Licensed, insured, and highly rated. Call (512) 555-0100 for fast, reliable service.">

  <!-- Keywords (less important now, but doesn't hurt) -->
  <meta name="keywords" content="plumber austin, emergency plumbing, water heater repair, drain cleaning, austin plumber">

  <!-- Canonical URL (prevent duplicate content) -->
  <link rel="canonical" href="https://www.smithplumbing.com/">

  <!-- Robots (control indexing) -->
  <meta name="robots" content="index, follow">

  <!-- Language -->
  <meta http-equiv="content-language" content="en-US">

  <!-- Author -->
  <meta name="author" content="Smith Plumbing">

  <!-- Theme color (mobile browsers) -->
  <meta name="theme-color" content="#0066cc">
</head>
<body>
  ...
</body>
</html>
```

### Title Tag Best Practices

**Format:** `Primary Keyword - Secondary Keyword | Brand Name`

**Rules:**
- **Length:** 50-60 characters (longer gets truncated)
- **Keywords:** Include primary keyword near the beginning
- **Unique:** Every page should have a unique title
- **Brand:** Include brand name at end (or beginning for homepage)
- **Compelling:** Write for users, not just search engines

**Examples:**
```html
<!-- Homepage -->
<title>Smith Plumbing - 24/7 Emergency Plumber in Austin, TX</title>

<!-- Service page -->
<title>Water Heater Repair & Installation Austin | Smith Plumbing</title>

<!-- Location page -->
<title>Plumber in South Austin, TX - Fast & Reliable | Smith Plumbing</title>

<!-- Blog post -->
<title>How to Fix a Leaky Faucet: Step-by-Step Guide | Smith Plumbing</title>

<!-- Contact page -->
<title>Contact Smith Plumbing - Get a Free Quote Today</title>
```

**Bad examples:**
```html
<!-- ❌ Too long (90+ characters) -->
<title>Professional Plumbing Services Including Water Heater Repair, Drain Cleaning, and Emergency Plumbing in Austin, TX | Smith Plumbing</title>

<!-- ❌ Keyword stuffing -->
<title>Plumber Austin, Austin Plumber, Plumbing Austin, Best Plumber Austin</title>

<!-- ❌ Not descriptive -->
<title>Home</title>

<!-- ❌ Missing brand -->
<title>Plumbing Services in Austin</title>
```

### Meta Description Best Practices

**Rules:**
- **Length:** 150-160 characters (longer gets truncated)
- **Compelling:** Include a call-to-action
- **Keywords:** Include primary keyword naturally
- **Unique:** Every page should have unique description
- **Accurate:** Must accurately describe page content

**Examples:**
```html
<!-- Homepage -->
<meta name="description" content="Smith Plumbing provides 24/7 emergency plumbing services in Austin, TX. Licensed, insured, and highly rated. Call (512) 555-0100 for fast, reliable service.">

<!-- Service page -->
<meta name="description" content="Expert water heater repair and installation in Austin. Same-day service available. We work on all brands and models. Free estimates. Call (512) 555-0100 today.">

<!-- Blog post -->
<meta name="description" content="Learn how to fix a leaky faucet in 5 simple steps. This DIY guide includes photos and tools you'll need. Save money and stop that annoying drip today.">

<!-- Contact page -->
<meta name="description" content="Contact Smith Plumbing for a free quote on plumbing services in Austin, TX. Available 24/7 for emergencies. Call (512) 555-0100 or fill out our online form.">
```

**Bad examples:**
```html
<!-- ❌ Too short -->
<meta name="description" content="Plumbing services.">

<!-- ❌ Too long (250+ characters) -->
<meta name="description" content="Smith Plumbing is the leading provider of comprehensive plumbing services in Austin, TX and surrounding areas. We offer emergency plumbing, water heater repair and installation, drain cleaning, sewer line repair, fixture installation, leak detection, and much more. Our licensed and insured plumbers are available 24/7.">

<!-- ❌ Not compelling -->
<meta name="description" content="This is the homepage for Smith Plumbing.">

<!-- ❌ Keyword stuffing -->
<meta name="description" content="Plumber Austin plumbing Austin plumber emergency plumber 24/7 plumber best plumber Austin TX.">
```

### Open Graph Tags (Facebook, LinkedIn)

Open Graph tags control how your page appears when shared on social media.

```html
<!-- Basic Open Graph tags -->
<meta property="og:title" content="Professional Plumbing Services in Austin, TX | Smith Plumbing">
<meta property="og:description" content="24/7 emergency plumbing services. Licensed, insured, highly rated. Call (512) 555-0100 for fast, reliable service.">
<meta property="og:image" content="https://www.smithplumbing.com/images/og-image.jpg">
<meta property="og:url" content="https://www.smithplumbing.com/">
<meta property="og:type" content="website">
<meta property="og:site_name" content="Smith Plumbing">
<meta property="og:locale" content="en_US">

<!-- Article-specific (for blog posts) -->
<meta property="og:type" content="article">
<meta property="article:author" content="John Smith">
<meta property="article:published_time" content="2025-01-15T09:00:00Z">
<meta property="article:modified_time" content="2025-01-20T14:30:00Z">
<meta property="article:section" content="DIY Tips">
<meta property="article:tag" content="plumbing">
<meta property="article:tag" content="DIY">

<!-- Business-specific -->
<meta property="og:type" content="business.business">
<meta property="business:contact_data:street_address" content="123 Main St">
<meta property="business:contact_data:locality" content="Austin">
<meta property="business:contact_data:region" content="TX">
<meta property="business:contact_data:postal_code" content="78701">
<meta property="business:contact_data:country_name" content="USA">
```

**OG Image requirements:**
- **Size:** 1200 × 630 pixels (recommended)
- **Format:** JPG or PNG
- **Max size:** Under 8 MB
- **Aspect ratio:** 1.91:1
- **Content:** Include branding, avoid text that's hard to read when small

### Twitter Card Tags

Twitter Cards control how your page appears when shared on Twitter/X.

```html
<!-- Summary card (default) -->
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@smithplumbing">
<meta name="twitter:creator" content="@johnsmith">
<meta name="twitter:title" content="Professional Plumbing Services in Austin, TX">
<meta name="twitter:description" content="24/7 emergency plumbing services. Licensed, insured, highly rated. Call (512) 555-0100.">
<meta name="twitter:image" content="https://www.smithplumbing.com/images/twitter-card.jpg">
<meta name="twitter:image:alt" content="Smith Plumbing logo and phone number">

<!-- Large image card (for hero images) -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@smithplumbing">
<meta name="twitter:title" content="How to Fix a Leaky Faucet: Step-by-Step Guide">
<meta name="twitter:description" content="Learn how to fix a leaky faucet in 5 simple steps. Includes photos and tool list.">
<meta name="twitter:image" content="https://www.smithplumbing.com/blog/leaky-faucet-hero.jpg">
<meta name="twitter:image:alt" content="Plumber fixing a kitchen faucet">
```

**Twitter image requirements:**
- **Summary card:** 1:1 aspect ratio (144 × 144 minimum, 4096 × 4096 max)
- **Large image card:** 2:1 aspect ratio (300 × 157 minimum, 4096 × 4096 max)
- **Format:** JPG, PNG, WEBP, GIF
- **Max size:** 5 MB

### Complete Meta Tags Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Primary SEO -->
  <title>Professional Plumbing Services in Austin, TX | Smith Plumbing</title>
  <meta name="description" content="Smith Plumbing provides 24/7 emergency plumbing services in Austin, TX. Licensed, insured, and highly rated. Call (512) 555-0100 for fast, reliable service.">
  <meta name="keywords" content="plumber austin, emergency plumbing, water heater repair, drain cleaning">
  <link rel="canonical" href="https://www.smithplumbing.com/">
  <meta name="robots" content="index, follow">

  <!-- Open Graph -->
  <meta property="og:title" content="Professional Plumbing Services in Austin, TX | Smith Plumbing">
  <meta property="og:description" content="24/7 emergency plumbing services. Licensed, insured, highly rated. Call (512) 555-0100.">
  <meta property="og:image" content="https://www.smithplumbing.com/images/og-image.jpg">
  <meta property="og:url" content="https://www.smithplumbing.com/">
  <meta property="og:type" content="website">
  <meta property="og:site_name" content="Smith Plumbing">

  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:site" content="@smithplumbing">
  <meta name="twitter:title" content="Professional Plumbing Services in Austin, TX">
  <meta name="twitter:description" content="24/7 emergency plumbing. Licensed, insured, highly rated. Call (512) 555-0100.">
  <meta name="twitter:image" content="https://www.smithplumbing.com/images/twitter-card.jpg">

  <!-- Additional -->
  <meta name="author" content="Smith Plumbing">
  <meta name="theme-color" content="#0066cc">

  <!-- Schema.org structured data -->
  <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "LocalBusiness",
      "name": "Smith Plumbing",
      ...
    }
  </script>
</head>
<body>
  ...
</body>
</html>
```

## Structured Data (Schema.org JSON-LD)

Structured data helps search engines understand your content and can result in rich snippets in search results (star ratings, prices, event dates, etc.).

**Format:** Use JSON-LD (Google's recommended format)
**Placement:** In `<head>` or end of `<body>`
**Testing:** Use Google's Rich Results Test

### LocalBusiness Schema (Critical for Local Businesses)

Perfect for plumbers, electricians, restaurants, salons, etc.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Smith Plumbing",
  "image": "https://www.smithplumbing.com/images/logo.jpg",
  "url": "https://www.smithplumbing.com",
  "telephone": "+15125550100",
  "priceRange": "$$",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main Street",
    "addressLocality": "Austin",
    "addressRegion": "TX",
    "postalCode": "78701",
    "addressCountry": "US"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 30.2672,
    "longitude": -97.7431
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday"
      ],
      "opens": "08:00",
      "closes": "18:00"
    },
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": "Saturday",
      "opens": "09:00",
      "closes": "14:00"
    }
  ],
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "127"
  },
  "review": [
    {
      "@type": "Review",
      "author": {
        "@type": "Person",
        "name": "Jane Doe"
      },
      "reviewRating": {
        "@type": "Rating",
        "ratingValue": "5"
      },
      "datePublished": "2025-01-15",
      "reviewBody": "Excellent service! Fast, professional, and reasonably priced. Highly recommend Smith Plumbing."
    }
  ],
  "areaServed": [
    {
      "@type": "City",
      "name": "Austin"
    },
    {
      "@type": "City",
      "name": "Round Rock"
    },
    {
      "@type": "City",
      "name": "Cedar Park"
    }
  ],
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Plumbing Services",
    "itemListElement": [
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "Emergency Plumbing",
          "description": "24/7 emergency plumbing services"
        }
      },
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "Water Heater Repair",
          "description": "Repair and installation of all water heater brands"
        }
      }
    ]
  }
}
</script>
```

**More specific types:**
- `Plumber` - For plumbing businesses
- `Electrician` - For electrical contractors
- `HomeAndConstructionBusiness` - General contractors
- `Restaurant` - Restaurants and cafes
- `BeautySalon` - Hair salons, nail salons
- `Attorney` - Law firms
- `Dentist` - Dental practices
- `MedicalClinic` - Medical clinics

### Organization Schema

For company information and branding.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Smith Plumbing",
  "alternateName": "Smith Plumbing & Heating",
  "url": "https://www.smithplumbing.com",
  "logo": "https://www.smithplumbing.com/images/logo.jpg",
  "image": "https://www.smithplumbing.com/images/team.jpg",
  "description": "Professional plumbing services in Austin, TX since 2005. Licensed, insured, and highly rated.",
  "email": "info@smithplumbing.com",
  "telephone": "+15125550100",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main Street",
    "addressLocality": "Austin",
    "addressRegion": "TX",
    "postalCode": "78701",
    "addressCountry": "US"
  },
  "contactPoint": [
    {
      "@type": "ContactPoint",
      "telephone": "+15125550100",
      "contactType": "customer service",
      "availableLanguage": ["English", "Spanish"],
      "areaServed": "US"
    },
    {
      "@type": "ContactPoint",
      "telephone": "+15125550101",
      "contactType": "emergency",
      "availableLanguage": "English",
      "hoursAvailable": "24/7"
    }
  ],
  "sameAs": [
    "https://www.facebook.com/smithplumbing",
    "https://www.instagram.com/smithplumbing",
    "https://twitter.com/smithplumbing",
    "https://www.linkedin.com/company/smithplumbing",
    "https://www.yelp.com/biz/smith-plumbing-austin"
  ],
  "founder": {
    "@type": "Person",
    "name": "John Smith"
  },
  "foundingDate": "2005-03-15",
  "numberOfEmployees": {
    "@type": "QuantitativeValue",
    "value": 12
  }
}
</script>
```

### Article Schema (Blog Posts)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "How to Fix a Leaky Faucet: Complete DIY Guide",
  "image": [
    "https://www.smithplumbing.com/blog/leaky-faucet-1x1.jpg",
    "https://www.smithplumbing.com/blog/leaky-faucet-4x3.jpg",
    "https://www.smithplumbing.com/blog/leaky-faucet-16x9.jpg"
  ],
  "datePublished": "2025-01-15T09:00:00-06:00",
  "dateModified": "2025-01-20T14:30:00-06:00",
  "author": {
    "@type": "Person",
    "name": "John Smith",
    "url": "https://www.smithplumbing.com/about/john-smith",
    "jobTitle": "Master Plumber",
    "image": "https://www.smithplumbing.com/images/john-smith.jpg"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Smith Plumbing",
    "logo": {
      "@type": "ImageObject",
      "url": "https://www.smithplumbing.com/images/logo.jpg",
      "width": 600,
      "height": 60
    }
  },
  "description": "Learn how to fix a leaky faucet in 5 simple steps with our complete DIY guide. Includes photos, tools needed, and troubleshooting tips.",
  "articleBody": "Full article text here...",
  "wordCount": 1250,
  "keywords": "leaky faucet, fix faucet, DIY plumbing, faucet repair",
  "articleSection": "DIY Tips",
  "inLanguage": "en-US",
  "isAccessibleForFree": true,
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://www.smithplumbing.com/blog/how-to-fix-leaky-faucet"
  }
}
</script>
```

**Article image requirements:**
- Multiple aspect ratios (1x1, 4x3, 16x9)
- Minimum width: 1200px
- Format: JPG, PNG, WebP

### Product Schema (E-commerce)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Premium Kitchen Faucet - Brushed Nickel",
  "image": [
    "https://www.example.com/faucet-front.jpg",
    "https://www.example.com/faucet-side.jpg",
    "https://www.example.com/faucet-top.jpg"
  ],
  "description": "High-quality kitchen faucet with pull-down sprayer. Brushed nickel finish resists spots and fingerprints.",
  "sku": "FK-8875-BN",
  "mpn": "8875",
  "brand": {
    "@type": "Brand",
    "name": "KitchenPro"
  },
  "offers": {
    "@type": "Offer",
    "url": "https://www.example.com/products/kitchen-faucet-bn",
    "priceCurrency": "USD",
    "price": "249.99",
    "priceValidUntil": "2025-12-31",
    "availability": "https://schema.org/InStock",
    "seller": {
      "@type": "Organization",
      "name": "Smith Plumbing Supply"
    },
    "shippingDetails": {
      "@type": "OfferShippingDetails",
      "shippingRate": {
        "@type": "MonetaryAmount",
        "value": "0",
        "currency": "USD"
      },
      "shippingDestination": {
        "@type": "DefinedRegion",
        "addressCountry": "US"
      },
      "deliveryTime": {
        "@type": "ShippingDeliveryTime",
        "businessDays": {
          "@type": "OpeningHoursSpecification",
          "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
        },
        "cutoffTime": "16:00:00-06:00",
        "handlingTime": {
          "@type": "QuantitativeValue",
          "minValue": 0,
          "maxValue": 1,
          "unitCode": "DAY"
        },
        "transitTime": {
          "@type": "QuantitativeValue",
          "minValue": 3,
          "maxValue": 5,
          "unitCode": "DAY"
        }
      }
    }
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.7",
    "reviewCount": "89",
    "bestRating": "5",
    "worstRating": "1"
  },
  "review": [
    {
      "@type": "Review",
      "author": {
        "@type": "Person",
        "name": "Sarah Johnson"
      },
      "reviewRating": {
        "@type": "Rating",
        "ratingValue": "5",
        "bestRating": "5"
      },
      "datePublished": "2025-01-10",
      "reviewBody": "Beautiful faucet and easy to install. The pull-down sprayer works great."
    }
  ]
}
</script>
```

### Service Schema

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Service",
  "serviceType": "Water Heater Repair",
  "provider": {
    "@type": "LocalBusiness",
    "name": "Smith Plumbing",
    "telephone": "+15125550100",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "123 Main Street",
      "addressLocality": "Austin",
      "addressRegion": "TX",
      "postalCode": "78701"
    }
  },
  "areaServed": {
    "@type": "City",
    "name": "Austin"
  },
  "description": "Professional water heater repair and installation services. We work on all brands and models including tank and tankless water heaters.",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "USD",
    "price": "95",
    "description": "Starting price for diagnostic service call"
  },
  "availableChannel": {
    "@type": "ServiceChannel",
    "serviceUrl": "https://www.smithplumbing.com/services/water-heater-repair",
    "servicePhone": {
      "@type": "ContactPoint",
      "telephone": "+15125550100",
      "availableLanguage": ["English", "Spanish"]
    }
  },
  "hoursAvailable": {
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
    "opens": "00:00",
    "closes": "23:59"
  }
}
</script>
```

### Breadcrumb Schema

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://www.smithplumbing.com/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Services",
      "item": "https://www.smithplumbing.com/services"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "Water Heater Repair",
      "item": "https://www.smithplumbing.com/services/water-heater-repair"
    }
  ]
}
</script>
```

### Person Schema

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "John Smith",
  "url": "https://www.smithplumbing.com/about/john-smith",
  "image": "https://www.smithplumbing.com/images/john-smith.jpg",
  "jobTitle": "Master Plumber & Owner",
  "worksFor": {
    "@type": "Organization",
    "name": "Smith Plumbing"
  },
  "email": "john@smithplumbing.com",
  "telephone": "+15125550100",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Austin",
    "addressRegion": "TX",
    "addressCountry": "US"
  },
  "sameAs": [
    "https://www.linkedin.com/in/johnsmith",
    "https://twitter.com/johnsmith"
  ],
  "knowsAbout": ["Plumbing", "Water Heaters", "Drain Cleaning", "Pipe Repair"],
  "alumniOf": {
    "@type": "CollegeOrUniversity",
    "name": "Austin Community College"
  },
  "hasCredential": [
    {
      "@type": "EducationalOccupationalCredential",
      "credentialCategory": "license",
      "name": "Master Plumber License",
      "recognizedBy": {
        "@type": "Organization",
        "name": "Texas State Board of Plumbing Examiners"
      }
    }
  ]
}
</script>
```

### FAQ Schema

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How much does a plumber cost in Austin?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Most plumbers in Austin charge $95-$150 for a service call, which typically includes the first hour of labor. Additional labor is usually $75-$125 per hour. Emergency and after-hours service may cost 1.5-2x the regular rate."
      }
    },
    {
      "@type": "Question",
      "name": "Do you offer same-day plumbing service?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes, we offer same-day service for most plumbing issues in Austin. Call us before 2 PM on weekdays, and we can typically schedule a visit the same day. Emergency service is available 24/7."
      }
    },
    {
      "@type": "Question",
      "name": "Are you licensed and insured?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes, Smith Plumbing is fully licensed (Texas Master Plumber License #M-12345) and insured. We carry both liability insurance and workers compensation insurance to protect our customers and employees."
      }
    }
  ]
}
</script>
```

### Review Schema (For Review Pages)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Review",
  "itemReviewed": {
    "@type": "LocalBusiness",
    "name": "Smith Plumbing",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "123 Main Street",
      "addressLocality": "Austin",
      "addressRegion": "TX",
      "postalCode": "78701"
    },
    "priceRange": "$$"
  },
  "author": {
    "@type": "Person",
    "name": "Michael Rodriguez"
  },
  "reviewRating": {
    "@type": "Rating",
    "ratingValue": "5",
    "bestRating": "5",
    "worstRating": "1"
  },
  "datePublished": "2025-01-18",
  "reviewBody": "Smith Plumbing saved the day! Had a burst pipe emergency and they came out within an hour. Professional, efficient, and reasonably priced. Highly recommend!"
}
</script>
```

## Technical SEO

### Sitemap.xml

Sitemaps help search engines discover and crawl your pages.

**Astro sitemap generation:**
```bash
# Install
npm install @astrojs/sitemap

# Configure in astro.config.mjs
import { defineConfig } from 'astro/dist/core/config';
import sitemap from '@astrojs/sitemap';

export default defineConfig({
  site: 'https://www.smithplumbing.com',
  integrations: [
    sitemap({
      changefreq: 'weekly',
      priority: 0.7,
      lastmod: new Date(),
      // Customize per-page
      serialize(item) {
        if (item.url === 'https://www.smithplumbing.com/') {
          item.priority = 1.0;
          item.changefreq = 'daily';
        }
        if (item.url.includes('/blog/')) {
          item.changefreq = 'monthly';
          item.priority = 0.6;
        }
        return item;
      },
      // Exclude pages
      filter: (page) => !page.includes('/admin/') && !page.includes('/draft/')
    })
  ]
});
```

**Manual sitemap example:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://www.smithplumbing.com/</loc>
    <lastmod>2025-01-20</lastmod>
    <changefreq>daily</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://www.smithplumbing.com/services</loc>
    <lastmod>2025-01-15</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://www.smithplumbing.com/services/water-heater-repair</loc>
    <lastmod>2025-01-10</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.7</priority>
  </url>
  <url>
    <loc>https://www.smithplumbing.com/blog/how-to-fix-leaky-faucet</loc>
    <lastmod>2025-01-20</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.6</priority>
  </url>
</urlset>
```

**Priority guidelines:**
- Homepage: 1.0
- Main service pages: 0.8-0.9
- Individual service pages: 0.7-0.8
- Blog posts: 0.5-0.6
- Utility pages (privacy, terms): 0.3-0.4

**Submit to Google:**
1. Add to robots.txt: `Sitemap: https://www.smithplumbing.com/sitemap.xml`
2. Submit in Google Search Console
3. Updates automatically crawled

### Robots.txt

Controls which pages search engines can crawl.

```txt
# Allow all crawlers to access all content
User-agent: *
Allow: /

# Block specific directories
Disallow: /admin/
Disallow: /private/
Disallow: /api/
Disallow: /temp/
Disallow: /*.pdf$

# Block query parameters
Disallow: /*?*

# Sitemap location
Sitemap: https://www.smithplumbing.com/sitemap.xml
Sitemap: https://www.smithplumbing.com/sitemap-blog.xml

# Crawl delay (optional, if server can't handle aggressive crawling)
# Crawl-delay: 10

# Specific bot rules
User-agent: Googlebot
Allow: /

User-agent: Bingbot
Allow: /

# Block bad bots (optional)
User-agent: AhrefsBot
Disallow: /

User-agent: SemrushBot
Disallow: /
```

**Common mistakes:**
```txt
# ❌ Don't block CSS/JS (Google needs these)
Disallow: /css/
Disallow: /js/

# ❌ Don't accidentally block everything
User-agent: *
Disallow: /  # This blocks ALL pages!

# ✅ Correct
User-agent: *
Allow: /
```

**Testing:** Use Google Search Console > robots.txt Tester

### Canonical URLs

Prevents duplicate content issues.

```html
<!-- Every page should have a canonical URL -->
<link rel="canonical" href="https://www.smithplumbing.com/services/water-heater-repair">
```

**Use cases:**
- **www vs non-www** - Pick one as canonical
- **HTTP vs HTTPS** - Always use HTTPS as canonical
- **Query parameters** - Point to clean URL
- **Similar content** - Point to primary version
- **Pagination** - Each page is canonical to itself

**Examples:**
```html
<!-- Page accessed via: https://www.smithplumbing.com/services?id=123 -->
<link rel="canonical" href="https://www.smithplumbing.com/services/water-heater-repair">

<!-- Page accessed via: http://smithplumbing.com/services (no www, no https) -->
<link rel="canonical" href="https://www.smithplumbing.com/services">

<!-- Page accessed via: https://www.smithplumbing.com/services/?utm_source=facebook -->
<link rel="canonical" href="https://www.smithplumbing.com/services">
```

**Self-referencing canonical (recommended for all pages):**
```html
<!-- Even if there's no duplicate, specify canonical -->
<link rel="canonical" href="https://www.smithplumbing.com/current-page-url">
```

### URL Structure Best Practices

**Good URL structure:**
- **Descriptive** - URL describes page content
- **Short** - Shorter is better (under 60 characters ideal)
- **Keywords** - Include primary keyword
- **Hyphens** - Use hyphens to separate words (not underscores)
- **Lowercase** - Always use lowercase
- **No special characters** - Avoid &, %, #, etc.
- **Logical hierarchy** - Reflects site structure

**Examples:**
```
✅ Good URLs:
https://www.smithplumbing.com/services/water-heater-repair
https://www.smithplumbing.com/blog/fix-leaky-faucet
https://www.smithplumbing.com/locations/south-austin

❌ Bad URLs:
https://www.smithplumbing.com/page.php?id=123&cat=5
https://www.smithplumbing.com/services/Water_Heater_Repair
https://www.smithplumbing.com/svcs/wtr-htr-rpr
https://www.smithplumbing.com/this-is-a-really-long-url-that-goes-on-and-on
```

**Hierarchy examples:**
```
/ (homepage)
/services/ (services overview)
  /services/emergency-plumbing
  /services/water-heater-repair
  /services/drain-cleaning
/locations/ (locations overview)
  /locations/south-austin
  /locations/round-rock
/blog/ (blog homepage)
  /blog/category/diy-tips
    /blog/category/diy-tips/fix-leaky-faucet
/about/
/contact/
```

### Internal Linking Strategy

Internal links help users navigate and distribute page authority.

**Best practices:**
- **Link to important pages** - More internal links = more important
- **Descriptive anchor text** - Use keywords naturally
- **Link from new content to old** - Revive older content
- **Link from high-traffic pages** - Pass authority to important pages
- **Navigation links** - Every page should be reachable in 3 clicks from homepage
- **Contextual links** - Links within content are more valuable than sidebar/footer

**Examples:**
```html
<!-- ✅ Good anchor text (descriptive keywords) -->
<p>
  Our <a href="/services/water-heater-repair">water heater repair services</a>
  are available 24/7 in Austin.
</p>

<!-- ❌ Bad anchor text (generic) -->
<p>
  We offer water heater repair services. <a href="/services/water-heater-repair">Click here</a>
  to learn more.
</p>

<!-- ✅ Contextual linking -->
<p>
  If you're experiencing low water pressure, it could be due to sediment buildup
  in your water heater. Learn more about
  <a href="/blog/signs-your-water-heater-needs-maintenance">signs your water heater needs maintenance</a>
  and how to prevent problems.
</p>
```

**Internal linking checklist:**
- Every page linked from at least one other page?
- Orphan pages (no internal links) identified and fixed?
- Important pages have many internal links pointing to them?
- Broken internal links fixed (404s)?
- Deep pages (4+ clicks from homepage) reduced?

## Content SEO

### Page Structure & Heading Hierarchy

**H1-H6 hierarchy rules:**
- **One H1 per page** - Primary page topic/keyword
- **Logical order** - H1 → H2 → H3 (don't skip levels)
- **Descriptive** - Headings describe section content
- **Keywords** - Include keywords naturally

**Example structure:**
```html
<h1>Water Heater Repair Services in Austin, TX</h1>

<h2>Professional Water Heater Repair</h2>
<p>Content about repair services...</p>

<h2>Common Water Heater Problems</h2>

<h3>No Hot Water</h3>
<p>Content about this problem...</p>

<h3>Water Not Hot Enough</h3>
<p>Content about this problem...</p>

<h3>Strange Noises</h3>
<p>Content about this problem...</p>

<h2>Water Heater Brands We Service</h2>
<p>Content about brands...</p>

<h2>Why Choose Smith Plumbing?</h2>

<h3>Licensed & Insured</h3>
<p>Content...</p>

<h3>Same-Day Service</h3>
<p>Content...</p>

<h2>Contact Us for Water Heater Repair</h2>
<p>Content with call-to-action...</p>
```

### Keyword Placement

**Where to include your primary keyword:**
1. **Title tag** - Near the beginning
2. **H1** - Exact match or close variation
3. **First paragraph** - Within first 100 words
4. **H2s/H3s** - Variations in some subheadings
5. **URL** - Clean, keyword-rich URL
6. **Meta description** - Naturally included
7. **Alt text** - For relevant images
8. **Body content** - 2-3% keyword density (natural, not stuffed)

**Example (primary keyword: "water heater repair austin"):**
```html
<title>Water Heater Repair Austin | Same-Day Service | Smith Plumbing</title>
<meta name="description" content="Expert water heater repair in Austin, TX. Same-day service, all brands. Licensed & insured. Call (512) 555-0100 for fast, reliable repair.">

<h1>Water Heater Repair Services in Austin, TX</h1>

<p>
  Need <strong>water heater repair in Austin</strong>? Smith Plumbing provides
  fast, professional repair services for all brands and models. We're available
  24/7 for emergency repairs and offer same-day service throughout the Austin area.
</p>

<h2>Professional Austin Water Heater Repair</h2>
<p>Content with natural keyword variations...</p>

<h2>Common Water Heater Problems We Fix</h2>
<p>Content...</p>
```

**Keyword density:**
- **Primary keyword:** 2-3% of total words
- **Related keywords:** 5-10% combined
- **Natural language:** Never force keywords

### Image Optimization for SEO

**File naming:**
```
❌ Bad:
IMG_1234.jpg
DSC00567.jpg
image (1).jpg

✅ Good:
water-heater-repair-austin.jpg
plumber-fixing-water-heater.jpg
tankless-water-heater-installation.jpg
```

**Alt text:**
```html
<!-- ✅ Descriptive alt text with keywords -->
<img
  src="water-heater-repair-austin.jpg"
  alt="Licensed plumber repairing gas water heater in Austin home"
  width="800"
  height="600"
  loading="lazy"
>

<!-- ❌ Missing or poor alt text -->
<img src="IMG_1234.jpg" alt="image">
```

**Image optimization checklist:**
- **Format:** WebP with JPG fallback (or just JPG)
- **Size:** Compressed (under 200 KB for photos)
- **Dimensions:** Correct size (don't scale down with HTML/CSS)
- **Descriptive filename:** Keywords with hyphens
- **Alt text:** Descriptive (not keyword stuffing)
- **Loading:** lazy for below-fold images
- **Width/height attributes:** Prevent layout shift (CLS)

**Responsive images:**
```html
<picture>
  <source
    srcset="water-heater-large.webp"
    type="image/webp"
    media="(min-width: 1024px)"
  >
  <source
    srcset="water-heater-medium.webp"
    type="image/webp"
    media="(min-width: 768px)"
  >
  <source srcset="water-heater-small.webp" type="image/webp">
  <img
    src="water-heater-small.jpg"
    alt="Licensed plumber repairing gas water heater"
    width="800"
    height="600"
    loading="lazy"
  >
</picture>
```

### Content Length Recommendations

**By page type:**
- **Homepage:** 500-800 words minimum
- **Service pages:** 800-1,500 words
- **Location pages:** 600-1,000 words
- **Blog posts:** 1,000-2,500 words (longer for comprehensive guides)
- **About page:** 500-1,000 words
- **Contact page:** 300-500 words

**Quality over quantity:**
- Don't artificially inflate word count
- Every sentence should add value
- Answer user questions comprehensively
- Break up text with headings, lists, images

## Local SEO (Critical for Small Businesses)

### Google Business Profile

**Most important local SEO factor!**

**Setup checklist:**
1. **Claim your business** - Search "Google Business Profile"
2. **Verify ownership** - Postcard, phone, or email
3. **Complete all sections:**
   - Business name (match website)
   - Address (NAP consistency)
   - Phone number (NAP consistency)
   - Website URL
   - Category (primary + secondary)
   - Hours (including special hours)
   - Service areas
   - Business description (750 characters, keyword-rich)
   - Attributes (women-owned, LGBTQ+ friendly, etc.)
   - Products/services
4. **Add photos:**
   - Logo
   - Cover photo
   - Team photos
   - Work photos
   - Interior/exterior
   - Products/services
   - **Goal: 100+ photos**
5. **Get reviews:**
   - Ask satisfied customers
   - Make it easy (send direct link)
   - Respond to ALL reviews
   - **Goal: 50+ reviews, 4.5+ rating**
6. **Post regularly:**
   - Updates
   - Offers
   - Events
   - Blog posts
   - **Goal: 2-4 posts per month**

**Google Business Profile description example:**
```
Smith Plumbing is Austin's trusted plumbing company since 2005. We provide 24/7 emergency plumbing, water heater repair and installation, drain cleaning, leak detection, and all residential and commercial plumbing services. Our licensed, insured master plumbers serve Austin, Round Rock, Cedar Park, and surrounding areas. Same-day service available. Family-owned and operated with over 1,000 five-star reviews. Call (512) 555-0100 for fast, professional plumbing service.
```

### NAP Consistency

NAP = Name, Address, Phone number

**Must be EXACTLY the same everywhere:**
- Website
- Google Business Profile
- Facebook
- Yelp
- BBB
- Industry directories
- Citations
- Schema markup

**Example (pick ONE format and use everywhere):**
```
✅ Consistent NAP:
Smith Plumbing
123 Main Street, Austin, TX 78701
(512) 555-0100

❌ Inconsistent (different formats hurt SEO):
Website: Smith Plumbing, 123 Main St, Austin TX 78701, 512-555-0100
Google: Smith Plumbing & Heating, 123 Main Street, Austin, Texas 78701, (512) 555-0100
Yelp: Smith Plumbing Inc., 123 Main St., Austin, TX, 512.555.0100
```

**Check NAP consistency:**
1. Google your business name + city
2. Audit all listings
3. Update incorrect listings
4. Remove duplicate listings

### Local Citations

Citations are mentions of your business NAP on other websites.

**Top citation sources (free):**
- Google Business Profile (required!)
- Bing Places
- Apple Maps
- Yelp
- Facebook
- Better Business Bureau
- Yellow Pages
- Angie's List / Angi
- HomeAdvisor (if you want leads)
- Thumbtack (if you want leads)
- Nextdoor

**Industry-specific:**
- **Plumbers:** PlumberDirectory, Plumbing-Heating-Cooling Contractors Association
- **Electricians:** Electrical Contractor Directory
- **Restaurants:** TripAdvisor, OpenTable, Zomato
- **Retail:** Merchant Circle, Manta

**Local directories:**
- Austin Chamber of Commerce
- Local business associations
- Community websites
- Local blogs/news sites

**Citation building tips:**
- **Consistency:** Use exact same NAP format
- **Accuracy:** Double-check all information
- **Completeness:** Fill out entire profile
- **Categories:** Choose relevant categories
- **Photos:** Add photos to listings
- **Descriptions:** Use keyword-rich descriptions
- **Links:** Link back to your website

### Local Keywords & "Near Me" Optimization

**Local keyword formats:**
- `[service] + [city]` - "plumber austin"
- `[service] + near me` - "plumber near me"
- `[service] + [neighborhood]` - "plumber south austin"
- `[service] + in [city]` - "plumber in austin"
- `[city] + [service]` - "austin plumber"

**Target local keywords on:**
- Homepage (city focus)
- Service pages (city + service)
- Location pages (neighborhood-specific)
- Blog posts (local angle)

**"Near me" optimization:**
```html
<!-- Google uses your address from Schema.org -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Smith Plumbing",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main Street",
    "addressLocality": "Austin",
    "addressRegion": "TX",
    "postalCode": "78701"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 30.2672,
    "longitude": -97.7431
  }
}
</script>
```

**Location pages for multiple service areas:**
```
/locations/south-austin
/locations/north-austin
/locations/round-rock
/locations/cedar-park
/locations/pflugerville
```

Each location page should have:
- Unique content (not duplicate!)
- Local landmarks/neighborhoods mentioned
- Local phone number (if different)
- Service area description
- Embedded Google Map
- Directions
- Testimonials from that area
- Local structured data

### Review Schema Markup

Helps display star ratings in search results.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Smith Plumbing",
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "127",
    "bestRating": "5",
    "worstRating": "1"
  },
  "review": [
    {
      "@type": "Review",
      "author": {
        "@type": "Person",
        "name": "Jane Doe"
      },
      "reviewRating": {
        "@type": "Rating",
        "ratingValue": "5",
        "bestRating": "5"
      },
      "datePublished": "2025-01-15",
      "reviewBody": "Excellent service! Fast, professional, and reasonably priced."
    }
  ]
}
</script>
```

**Review generation strategy:**
1. **Ask at the right time** - After successful job completion
2. **Make it easy** - Send direct link to Google review form
3. **Provide options** - Google, Facebook, Yelp
4. **Don't incentivize** - No payment for reviews (against Google's TOS)
5. **Respond to all** - Thank positive, address negative professionally
6. **Monitor** - Set up alerts for new reviews

**Get Google review link:**
1. Open your Google Business Profile
2. Home → "Get more reviews" → Copy link
3. Format: `https://g.page/r/[YOUR_CODE]/review`

## Performance Impact on SEO

### Core Web Vitals as Ranking Factor

Google uses Core Web Vitals as a ranking signal (since June 2021).

**The three metrics:**
1. **LCP (Largest Contentful Paint)** - Loading performance
   - **Target:** < 2.5 seconds
   - **SEO impact:** HIGH

2. **FID/INP (First Input Delay / Interaction to Next Paint)** - Interactivity
   - **FID target:** < 100ms (deprecated)
   - **INP target:** < 200ms (replacement)
   - **SEO impact:** MEDIUM

3. **CLS (Cumulative Layout Shift)** - Visual stability
   - **Target:** < 0.1
   - **SEO impact:** MEDIUM

**See full details:** [Performance Standards](./performance.md)

### Mobile-First Indexing

Google primarily uses the mobile version of your site for indexing and ranking.

**Requirements:**
- **Responsive design** - Must work well on mobile
- **Same content** - Mobile version has all important content
- **Fast loading** - Mobile performance critical
- **Touch-friendly** - Buttons/links easy to tap (44×44px minimum)
- **Readable text** - No tiny fonts (16px minimum)
- **No intrusive interstitials** - Avoid full-page popups on mobile

**Test mobile-friendliness:**
- Google Mobile-Friendly Test
- Chrome DevTools mobile emulation
- Lighthouse mobile audit
- Real device testing

### Page Speed as Ranking Factor

**Speed impacts:**
- **Bounce rate** - Slow sites = higher bounce rate
- **User experience** - Slow = frustrated users
- **Crawl budget** - Slow sites crawled less frequently
- **Conversions** - Every 100ms delay = 1% revenue loss (Amazon data)

**Speed targets:**
- **Time to Interactive:** < 3.8 seconds
- **Speed Index:** < 3.4 seconds
- **Total Blocking Time:** < 300ms

**See full optimization guide:** [Performance Standards](./performance.md)

## Astro-Specific SEO

### Static Generation SEO Benefits

Astro's static site generation provides SEO advantages:

**Benefits:**
- **Fast loading** - No server processing time
- **Cached content** - Serves from CDN edge locations
- **Reliable** - No database/server failures
- **Crawlable** - Pure HTML, easily crawled by bots
- **Small JavaScript** - Minimal JS = fast TTI

**Best for:**
- Marketing sites
- Business websites
- Blogs
- Documentation
- Landing pages

### SEO Component Pattern

**Reusable SEO component:**

```astro
---
// src/components/SEO.astro
export interface Props {
  title: string;
  description: string;
  image?: string;
  canonical?: string;
  type?: 'website' | 'article' | 'product';
  publishedTime?: string;
  modifiedTime?: string;
}

const {
  title,
  description,
  image = '/images/og-default.jpg',
  canonical,
  type = 'website',
  publishedTime,
  modifiedTime
} = Astro.props;

const siteUrl = 'https://www.smithplumbing.com';
const canonicalURL = canonical || new URL(Astro.url.pathname, siteUrl).toString();
const imageUrl = new URL(image, siteUrl).toString();
---

<!-- Primary Meta Tags -->
<title>{title}</title>
<meta name="title" content={title} />
<meta name="description" content={description} />
<link rel="canonical" href={canonicalURL} />

<!-- Open Graph / Facebook -->
<meta property="og:type" content={type} />
<meta property="og:url" content={canonicalURL} />
<meta property="og:title" content={title} />
<meta property="og:description" content={description} />
<meta property="og:image" content={imageUrl} />
<meta property="og:site_name" content="Smith Plumbing" />

{publishedTime && <meta property="article:published_time" content={publishedTime} />}
{modifiedTime && <meta property="article:modified_time" content={modifiedTime} />}

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:url" content={canonicalURL} />
<meta name="twitter:title" content={title} />
<meta name="twitter:description" content={description} />
<meta name="twitter:image" content={imageUrl} />
```

**Usage:**
```astro
---
// src/pages/services/water-heater-repair.astro
import SEO from '@components/SEO.astro';
import Layout from '@layouts/Layout.astro';
---

<Layout>
  <SEO
    title="Water Heater Repair Austin | Same-Day Service | Smith Plumbing"
    description="Expert water heater repair in Austin, TX. Same-day service, all brands. Licensed & insured. Call (512) 555-0100."
    image="/images/water-heater-repair-og.jpg"
  />

  <main>
    <h1>Water Heater Repair Services in Austin, TX</h1>
    <!-- Content -->
  </main>
</Layout>
```

### Metadata Management

**Global SEO config:**

```typescript
// src/config/seo.ts
export const siteConfig = {
  name: 'Smith Plumbing',
  url: 'https://www.smithplumbing.com',
  description: 'Professional plumbing services in Austin, TX since 2005.',
  author: 'Smith Plumbing',
  phone: '(512) 555-0100',
  email: 'info@smithplumbing.com',
  address: {
    street: '123 Main Street',
    city: 'Austin',
    state: 'TX',
    zip: '78701'
  },
  social: {
    facebook: 'https://www.facebook.com/smithplumbing',
    instagram: 'https://www.instagram.com/smithplumbing',
    twitter: 'https://twitter.com/smithplumbing'
  },
  defaultOgImage: '/images/og-default.jpg'
};
```

**Dynamic meta tags:**
```astro
---
// src/pages/blog/[slug].astro
import { siteConfig } from '@config/seo';

export async function getStaticPaths() {
  const posts = await getCollection('blog');
  return posts.map(post => ({
    params: { slug: post.slug },
    props: { post }
  }));
}

const { post } = Astro.props;
const { title, description, publishedAt, image } = post.data;
---

<SEO
  title={`${title} | ${siteConfig.name}`}
  description={description}
  image={image || siteConfig.defaultOgImage}
  type="article"
  publishedTime={publishedAt.toISOString()}
/>
```

## SEO Tools

### Google Search Console

**Essential for monitoring SEO performance.**

**Setup:**
1. Go to search.google.com/search-console
2. Add property (domain or URL prefix)
3. Verify ownership (HTML file, DNS, tag, or Google Analytics)
4. Submit sitemap

**What to monitor:**
- **Performance** - Clicks, impressions, CTR, position
- **Coverage** - Indexed pages, errors, warnings
- **Core Web Vitals** - Performance issues
- **Mobile Usability** - Mobile-friendly issues
- **Security Issues** - Manual actions, security problems

**Key reports:**
1. **Search Results** - Which keywords drive traffic
2. **Pages** - Which pages perform best
3. **Countries** - Geographic distribution
4. **Devices** - Desktop vs mobile vs tablet
5. **Search Appearance** - Rich result performance

### Google Analytics 4

**Setup:**
1. Create GA4 property at analytics.google.com
2. Get Measurement ID (G-XXXXXXXXXX)
3. Add to Astro site:

```astro
---
// src/layouts/Layout.astro
const GA_MEASUREMENT_ID = import.meta.env.PUBLIC_GA_ID;
---

<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Google Analytics -->
  <script async src={`https://www.googletagmanager.com/gtag/js?id=${GA_MEASUREMENT_ID}`}></script>
  <script define:vars={{ GA_MEASUREMENT_ID }}>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', GA_MEASUREMENT_ID);
  </script>

  <!-- Rest of head -->
</head>
<body>
  <slot />
</body>
</html>
```

**Key metrics for SEO:**
- **Organic traffic** - Traffic from search engines
- **Bounce rate** - Single-page sessions
- **Average session duration** - Time on site
- **Pages per session** - Page depth
- **Top landing pages** - Entry points from search

### Lighthouse SEO Audit

**How to run:**
1. Open Chrome DevTools (F12)
2. Click "Lighthouse" tab
3. Select "SEO" category
4. Click "Analyze page load"

**What it checks:**
- Meta description present
- Title tag present and length
- Crawlable links
- Valid robots.txt
- Successful HTTP status code
- Image aspect ratios
- Font sizes
- Tap target sizes
- And more...

**Target score:** 95-100

### Schema Markup Validators

**Google Rich Results Test:**
- URL: search.google.com/test/rich-results
- Tests: All structured data types
- Shows: Preview of how rich result appears
- Use: For testing individual pages

**Schema.org Validator:**
- URL: validator.schema.org
- Tests: JSON-LD, Microdata, RDFa
- Shows: Structured data tree
- Use: For validating schema syntax

**Google Search Console (live data):**
- Reports → Enhancements
- Shows: Rich result performance and errors
- Use: For monitoring live site

## AI-Assisted SEO

### Generating Meta Descriptions with AI

**Prompt template:**
```
Write a compelling meta description (150-160 characters) for this page:

Page URL: [URL]
Primary keyword: [keyword]
Page content: [brief summary]

The description should:
- Include the primary keyword naturally
- Have a clear call-to-action
- Be compelling and click-worthy
- Accurately describe the page content
- Stay within 150-160 character limit

Provide 3 variations.
```

**Example:**
```
Write a compelling meta description (150-160 characters) for this page:

Page URL: /services/water-heater-repair
Primary keyword: water heater repair austin
Page content: We provide professional water heater repair services in Austin. Same-day service, licensed plumbers, all brands. Available 24/7 for emergencies.

The description should:
- Include the primary keyword naturally
- Have a clear call-to-action
- Be compelling and click-worthy
- Accurately describe the page content
- Stay within 150-160 character limit

Provide 3 variations.
```

### Schema Markup Creation with AI

**Prompt template:**
```
Create Schema.org JSON-LD structured data for a [business type]:

Business details:
- Name: [name]
- Address: [address]
- Phone: [phone]
- Website: [url]
- Services: [list]
- Hours: [hours]
- Rating: [rating]
- Review count: [count]

Use the LocalBusiness schema type (or more specific like Plumber, Electrician, etc.).
Include all relevant properties.
```

### Content Optimization with AI

**SEO content review prompt:**
```
Review this page content for SEO optimization:

[Paste content]

Primary keyword: [keyword]
Target word count: [count]

Analyze:
1. Keyword usage (frequency, placement, variations)
2. Heading structure (H1-H6 hierarchy)
3. Content quality and completeness
4. Internal linking opportunities
5. Call-to-action effectiveness
6. Readability (sentence length, paragraph length)
7. Missing elements (images, lists, etc.)

Provide specific recommendations for improvement.
```

**Local SEO content prompt:**
```
Write [word count] words of SEO-optimized content for a [business type] in [city]:

Primary keyword: [keyword]
Secondary keywords: [keywords]
Unique selling points: [USPs]
Service area: [areas]

Content should:
- Target local searchers
- Include location naturally throughout
- Mention local landmarks/neighborhoods
- Include primary keyword in first paragraph
- Use H2/H3 subheadings with keyword variations
- Include a clear call-to-action
- Be conversational and helpful (not keyword-stuffed)

Target audience: [description]
```

## Cross-References

**Interdependent Quality Standards:**
- **[Performance Standards](./performance.md)** - Core Web Vitals are direct Google ranking factors
- **[Accessibility Standards](./accessibility.md)** - Accessible markup improves SEO (semantic HTML, alt text, proper structure)
- **[How These Standards Relate](./README.md#how-these-standards-relate)** - Understanding the quality triangle

**Related documentation:**
- [Client Management](../business-model/client-management.md) - Explaining SEO value to clients
- [Testing & Debugging](../workflow/phase-3-testing-debugging.md) - SEO testing in your workflow
- [Cloudflare Pages](../hosting-tools/cloudflare-pages.md) - Hosting configuration for SEO
- [Quality Standards Overview](./README.md) - Back to quality standards home

---

**Remember:** SEO is a long-term investment. Results take 3-6 months to materialize. Focus on creating genuinely helpful content for your target audience, and the rankings will follow.
