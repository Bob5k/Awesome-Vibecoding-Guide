# Cloudflare Pages

## Overview

Cloudflare Pages is a JAMstack platform for deploying static sites and frontend applications. It's particularly well-suited for modern frameworks like Astro, Next.js, React, Vue, and more.

## Key Benefits

### Completely Free for Static Sites
- **Zero cost** for hosting static pages
- **No bandwidth limits** on the free tier
- **Unlimited requests** - perfect for production websites
- No hidden costs or surprise bills

### Security & Performance
- **DDoS protection** built-in
- **Hacker-proof hosting** - static sites have minimal attack surface
- **Global CDN** - content served from 300+ locations worldwide
- **Automatic HTTPS** with SSL certificates
- **Always online** with 100% uptime SLA

### Perfect Use Cases
- Business websites for clients
- Portfolio sites
- Documentation sites
- Marketing landing pages
- Astro + Tailwind CSS stack (recommended baseline)
- Static blogs with CMS integration

## CMS Integration

### Keystatic CMS via GitHub
Cloudflare Pages integrates seamlessly with Keystatic CMS through GitHub:

1. **Content Management**: Non-technical users can edit content
2. **Git-based workflow**: All changes tracked in version control
3. **Automatic deployments**: Push to GitHub = instant deployment
4. **Free hosting**: No CMS hosting fees
5. **Collaborative editing**: Multiple team members can manage content

## Getting Started

### Prerequisites
- GitHub account (or GitLab/Bitbucket)
- Cloudflare account (free)
- Your static site or framework project

### Setup Process

1. **Prepare Your Project**
   ```bash
   # Example with Astro
   npm create astro@latest my-site
   cd my-site
   npm install
   npm run build
   ```

2. **Connect to Git**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

3. **Deploy to Cloudflare Pages**
   - Log in to [Cloudflare Dashboard](https://dash.cloudflare.com)
   - Navigate to **Pages** in the sidebar
   - Click **Create a project**
   - Click **Connect to Git**
   - Authorize Cloudflare to access your repository
   - Select your repository

4. **Configure Build Settings**

   For **Astro** projects:
   ```
   Framework preset: Astro
   Build command: npm run build
   Build output directory: dist
   ```

   For **Next.js** (static export):
   ```
   Framework preset: Next.js (Static HTML Export)
   Build command: npm run build
   Build output directory: out
   ```

   For **React/Vite**:
   ```
   Framework preset: Create React App / Vite
   Build command: npm run build
   Build output directory: dist
   ```

5. **Deploy**
   - Click **Save and Deploy**
   - Watch the build process in real-time
   - Your site will be live in ~1-2 minutes

## Custom Domains

### Adding a Custom Domain

1. Go to your Pages project
2. Click **Custom domains** tab
3. Click **Set up a custom domain**
4. Enter your domain (e.g., `example.com`)
5. Follow DNS configuration instructions

### DNS Configuration
If your domain is on Cloudflare:
- Automatic CNAME setup
- Instant SSL certificate

If your domain is elsewhere:
- Add CNAME record pointing to your Pages URL
- SSL certificate issued within minutes

## Environment Variables

### Adding Secrets/Config

1. Go to project **Settings**
2. Navigate to **Environment variables**
3. Add variables for different environments:
   - Production
   - Preview (for PR deployments)

Example variables:
```
API_KEY=your-api-key
SITE_URL=https://example.com
```

Access in your code:
```javascript
// Astro
const apiKey = import.meta.env.API_KEY;

// Next.js
const apiKey = process.env.NEXT_PUBLIC_API_KEY;
```

## Preview Deployments

Every pull request gets its own preview deployment:
- Unique URL for testing
- Production-identical environment
- Perfect for client previews
- Automatic comments on PRs with preview links

## Ensuring It Works

### Build Verification Checklist

1. **Local build test**:
   ```bash
   npm run build
   npm run preview  # Test the built output
   ```

2. **Check deployment logs**:
   - View build logs in Cloudflare dashboard
   - Look for any warnings or errors
   - Verify build completed successfully

3. **Test the live site**:
   - Open the provided `.pages.dev` URL
   - Check all pages load correctly
   - Verify images and assets load
   - Test navigation and links

4. **Performance check**:
   - Use [PageSpeed Insights](https://pagespeed.web.dev/)
   - Should score 90+ on all metrics
   - Check mobile and desktop versions

### Common Issues & Solutions

**Build fails:**
- Check Node.js version in build settings
- Verify all dependencies in `package.json`
- Ensure build command is correct

**404 errors:**
- Check output directory matches build output
- Verify routing configuration for SPAs

**Assets not loading:**
- Use relative paths or proper base URLs
- Check asset paths in built output

## Efficient Usage Tips

### 1. Optimize Build Times
```javascript
// Use caching for dependencies
// Cloudflare automatically caches node_modules
```

### 2. Leverage Astro for Performance
```bash
npm create astro@latest
# Choose "Empty" template
# Add only what you need
```

### 3. Use Tailwind for Styling
```bash
npm install -D tailwindcss
npx tailwindcss init
```

### 4. Implement Keystatic CMS
```bash
npm install @keystatic/core @keystatic/astro
```

Configuration example:
```javascript
// keystatic.config.js
import { config, collection, fields } from '@keystatic/core';

export default config({
  storage: {
    kind: 'github',
    repo: 'your-username/your-repo',
  },
  collections: {
    posts: collection({
      label: 'Posts',
      path: 'src/content/posts/*',
      schema: {
        title: fields.text({ label: 'Title' }),
        content: fields.document({ label: 'Content' }),
      },
    }),
  },
});
```

### 5. Monitoring & Analytics
- Enable **Web Analytics** in Cloudflare (free, privacy-first)
- Track page views without cookies
- No impact on performance

## Pricing

### Free Tier (Generous)
- ✅ Unlimited sites
- ✅ Unlimited requests
- ✅ Unlimited bandwidth
- ✅ 500 builds per month
- ✅ 1 concurrent build
- ✅ 20,000 files per deployment

### Paid Plan ($20/month - if needed)
- 5,000 builds per month
- 5 concurrent builds
- Advanced build configurations
- Larger file limits

**Reality**: Most projects never need paid plan for static sites.

## Integration with Other Cloudflare Services

- **Pages Functions**: Add serverless functions (similar to Workers)
- **D1 Database**: Connect database for dynamic features
- **R2 Storage**: Store and serve media files
- **KV**: Store configuration and cache data

## Official Resources

- **Documentation**: https://developers.cloudflare.com/pages/
- **Framework Guides**: https://developers.cloudflare.com/pages/framework-guides/
- **Discord Community**: https://discord.cloudflare.com
- **Status Page**: https://www.cloudflarestatus.com/

## Real-World Example

Deploying an Astro + Tailwind business site with Keystatic CMS:

```bash
# 1. Create project
npm create astro@latest client-business-site
cd client-business-site

# 2. Add Tailwind
npx astro add tailwind

# 3. Add Keystatic
npm install @keystatic/core @keystatic/astro
npx @keystatic/cli init

# 4. Build and test
npm run build
npm run preview

# 5. Push to GitHub
git init
git add .
git commit -m "Initial business site"
git push

# 6. Deploy to Cloudflare Pages via dashboard
# Total time: ~10 minutes
# Total cost: $0
# Result: Professional, fast, secure website
```

## Why It's Perfect for Client Work

1. **Zero hosting costs** - better margins for you
2. **Set it and forget it** - no server maintenance
3. **Impossible to hack** - static files only
4. **Fast globally** - Cloudflare's CDN
5. **Client can edit content** - via Keystatic
6. **Professional results** - enterprise-grade infrastructure
7. **Scalable** - handles traffic spikes automatically

This makes Cloudflare Pages ideal for building websites for clients where you can deliver professional results without ongoing hosting costs or security concerns.
