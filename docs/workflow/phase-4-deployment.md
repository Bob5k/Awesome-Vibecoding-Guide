# Phase 5: Deployment 🚢

**Tools:** CI/CD platform + Hosting provider

## Recommended Platforms

### Cloudflare Pages/Workers ⭐ **Best for Professional Projects**

**Cloudflare Pages** (Static Sites)
- **Completely free hosting** - no bandwidth limits, no visitor caps
- **Built-in CI/CD** - automatic deployments from Git repositories
- **Global CDN** - instant caching and fast loading worldwide
- **Custom domains** free with SSL certificates
- **Edge functions** for dynamic content without a separate backend

**Cloudflare Workers** (Serverless Backend)
- **100,000 requests/day free** - enough for most business websites
- **Pay-as-you-go beyond that** - $0.15 per million additional requests
- **Global edge network** - low latency worldwide
- **Durable objects** for real-time applications
- **KV storage** for key-value data

**Why it's perfect for client projects:**
- **Predictable costs** - you know exactly what you'll pay
- **Enterprise-grade infrastructure** - used by major companies
- **No surprise bills** - usage is predictable and billing is transparent
- **Professional reliability** - 99.9%+ uptime guarantee
- **Scalability** - handles traffic spikes without additional cost

### GitHub Pages 🆓 **Best for Personal/Portfolio Projects**

**Completely free for:**
- Static websites (HTML, CSS, JavaScript)
- Personal portfolios
- Open source project documentation
- Experimental side projects

**Limitations:**
- **Static only** - no server-side processing
- **GitHub branding** on free plans
- **Build time limits** (10 minutes)
- **Not suitable for client work** - lacks professional SLA and support
- **Custom domain setup** requires manual DNS configuration

**Perfect for:**
- Learning developers building their first projects
- Personal portfolios and blogs
- Open source documentation
- Hobby projects where cost is the primary concern

### Vercel/Netlify 🚀 **Best (performance wise) for Interactive Next.js Applications**

**Vercel**
- **Optimized for Next.js** - best performance and features
- **Server-side rendering** and API routes supported
- **Edge functions** for compute-heavy operations
- **Free tier limitations:**
  - 100GB bandwidth/month
  - Limited serverless function execution time
  - Usage-based pricing can add up quickly

**Netlify**
- **Great for Jamstack sites**
- **Forms handling** and serverless functions
- **Build plugins** ecosystem
- **Similar free tier limitations** to Vercel

**⚠️ Cost Warning for Client Projects:**
- **Usage-based billing** can become expensive with traffic
- **Serverless functions** charge per invocation and execution time
- **Bandwidth overages** can lead to surprise bills
- **Not predictable** - costs scale with user engagement

**When to use:**
- **Client projects** with **defined budgets** and **traffic expectations**
- **Next.js applications** that require server-side features
- **Projects where performance justifies the cost**
- **Applications with clear monetization strategies**


## CI/CD Implementation

### Automated Deployment Pipeline

**Standard Workflow:**
```bash
# Development
git add .
git commit -m "feat: Add user authentication"
git push origin main

# Automatic deployment
# Cloudflare/GitHub Pages/GitLab Pages picks up changes
# Builds and deploys automatically
```

### Platform-Specific Deployment

#### Cloudflare Pages (Recommended)
**Setup for automatic deployment:**
1. Connect GitHub repository to Cloudflare Pages
2. Configure build settings:
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
   - **Node version**: 18 or 20
3. Set environment variables if needed
4. Deploy on every push to main branch

**Configuration:**
```toml
# wrangler.toml (for Workers/Functions)
name = "my-project"
compatibility_date = "2023-10-30"
pages_build_output_dir = "./dist"

[env.production]
vars = { ENVIRONMENT = "production" }
```

#### GitHub Pages
**Setup for static sites:**
1. Enable Pages in repository settings
2. Select source branch (usually `main`)
3. Configure build if using Jekyll/Hugo
4. Custom domain setup (optional)

**Workflow:**
```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '20'
    - name: Install dependencies
      run: npm install
    - name: Build
      run: npm run build
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

## Production Deployment Checklist

**Pre-Deployment:**
- [ ] [Testing completed](./phase-3-testing-debugging.md) - All tests passing
- [ ] [Code reviewed](./phase-3-testing-debugging.md#code-review-process) - Quality standards met
- [ ] [Environment variables configured](../core-technologies.md#environment-variables)
- [ ] [Build process tested locally](../core-technologies.md#build-for-production)
- [ ] [Domain name registered and configured](#domain-setup)

**Deployment Configuration:**
- [ ] [Hosting platform configured](./phase-4-deployment.md#recommended-platforms)
- [ ] [Environment variables set in production](#environment-variables)
- [ ] [SSL certificates configured](#ssl-setup)
- [ ] [Custom domain pointed correctly](#domain-setup)
- [ ] [Analytics and monitoring setup](#monitoring-setup)

**Post-Deployment Verification:**
- [ ] [Website loads correctly](#post-deployment-testing)
- [ ] [All features working in production](#functionality-testing)
- [ ] [Performance metrics acceptable](#performance-testing)
- [ ] [SEO elements properly configured](#seo-verification)
- [ ] [Error monitoring active](#error-tracking)

## Environment Variables & Configuration

### Production Environment Setup

**Common Environment Variables:**
```bash
# API Configuration
API_BASE_URL=https://api.yourdomain.com
PUBLIC_API_KEY=your_public_key

# Database
DATABASE_URL=your_production_db_url
DB_ENCRYPTION_KEY=your_encryption_key

# External Services
STRIPE_SECRET_KEY=sk_live_...
SENDGRID_API_KEY=SG....
CLOUDFLARE_ZONE_ID=your_zone_id

# Analytics
GOOGLE_ANALYTICS_ID=G-XXXXXXXXXX
MIXPANEL_TOKEN=your_mixpanel_token
```

**Setting Variables by Platform:**

**Cloudflare Pages:**
1. Go to Pages dashboard
2. Select your project
3. Navigate to Settings > Environment Variables
4. Add each variable with its value
5. Redeploy to apply changes

**Vercel:**
1. Go to project dashboard
2. Navigate to Settings > Environment Variables
3. Add variables for Production, Preview, and Development
4. Deploy automatically updates

**GitHub Actions:**
```yaml
env:
  PRODUCTION_URL: ${{ secrets.PRODUCTION_URL }}
  DATABASE_URL: ${{ secrets.DATABASE_URL }}
```

## Domain Setup & SSL

### Custom Domain Configuration

**DNS Setup:**
```dns
# A records for root domain
A @ 192.0.2.1
A www 192.0.2.1

# CNAME for subdomain
CNAME app your-app.pages.dev

# For Cloudflare (recommended)
CNAME @ your-site.pages.dev
CNAME www your-site.pages.dev
```

**Cloudflare Specific:**
1. Add domain to Cloudflare DNS
2. Update nameservers at domain registrar
3. Enable "Always Use HTTPS"
4. Configure caching rules

**SSL Certificate Management:**
- **Automatic**: Most platforms (Cloudflare, Vercel) provide free SSL
- **Let's Encrypt**: Free SSL certificates for custom setup
- **Manual**: Purchase SSL certificates for enterprise needs

## Monitoring & Error Tracking

### Production Monitoring Setup

**Essential Monitoring Tools:**

**1. Uptime Monitoring**
- [Cloudflare Analytics](https://dash.cloudflare.com) - Built-in analytics
- [Pingdom](https://www.pingdom.com) - External uptime monitoring
- [UptimeRobot](https://uptimerobot.com) - Free tier available

**2. Performance Monitoring**
- [Google Analytics](https://analytics.google.com) - User behavior tracking
- [Google PageSpeed Insights](https://pagespeed.web.dev) - Performance metrics
- [GTmetrix](https://gtmetrix.com) - Detailed performance analysis

**3. Error Tracking**
- [Sentry](https://sentry.io) - Error monitoring and performance tracking
- [LogRocket](https://logrocket.com) - Session replay and error tracking
- [Bugsnag](https://www.bugsnag.com) - Error monitoring and alerting

### Health Check Endpoints

**API Health Check:**
```typescript
// /api/health.ts
export async function GET() {
  try {
    // Check database connection
    await db.ping();
    
    // Check external services
    await fetch(process.env.API_HEALTH_CHECK);
    
    return new Response(
      JSON.stringify({ status: 'healthy', timestamp: new Date().toISOString() }),
      { headers: { 'Content-Type': 'application/json' } }
    );
  } catch (error) {
    return new Response(
      JSON.stringify({ status: 'unhealthy', error: error.message }),
      { status: 500, headers: { 'Content-Type': 'application/json' } }
    );
  }
}
```

## Backup & Rollback Strategy

### Database Backup

**Automated Backups:**
```sql
-- Daily backup script
pg_dump production_db > backup_$(date +%Y%m%d).sql

-- Upload to cloud storage
aws s3 cp backup_$(date +%Y%m%d).sql s3://backups-bucket/
```

**Manual Backup Process:**
1. Create database dump
2. Upload to cloud storage (S3, R2, etc.)
3. Test restore process
4. Document backup retention policy

### Rollback Procedures

**Application Rollback:**
```bash
# Git-based rollback
git revert HEAD~2..HEAD
git push origin main

# Or revert to specific deployment
cf pages deployment list --project-name=my-project
cf pages deployment rollback --project-name=my-project --deployment=<id>
```

**Database Rollback:**
```bash
# Restore from backup
psql production_db < backup_20231201.sql

# Point application to restored database
# Update environment variables if needed
```

## Client Project Considerations

### Handover Documentation

**Create comprehensive handover package:**
1. **Technical documentation** - Architecture and stack
2. **Admin access** - Hosting, domain, analytics
3. **Content management** - How to update content
4. **Maintenance plan** - Regular updates and monitoring
5. **Contact information** - For ongoing support

**Client Training Materials:**
- How to make basic content updates
- How to access analytics dashboard
- How to request feature additions
- Maintenance schedule and costs

### Maintenance & Updates

**Regular Maintenance Tasks:**
- Security updates (monthly)
- Content updates (as needed)
- Performance monitoring (weekly)
- Backup verification (weekly)
- SSL certificate renewal (annually)

**Update Process:**
```bash
# Development
git checkout -b update/feature-addition
# Make changes
git add .
git commit -m "feat: Add client request feature"
git push origin update/feature-addition

# Review and deploy
# Test in staging environment
# Deploy to production
# Monitor for issues
```

## Performance Optimization Post-Deployment

### Core Web Vitals Monitoring

**Target Metrics:**
- **LCP (Largest Contentful Paint)**: < 2.5s
- **FID (First Input Delay)**: < 100ms
- **CLS (Cumulative Layout Shift)**: < 0.1

**Optimization Checklist:**
- [ ] Images optimized and compressed
- [ ] CSS and JavaScript minified
- [ ] Caching headers configured
- [ ] CDN properly configured
- [ ] Database queries optimized

### CDN Configuration

**Cloudflare CDN:**
```javascript
// Cache static assets for 1 year
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url)
  
  // Cache static assets
  if (url.pathname.match(/\.(js|css|png|jpg|gif|ico|svg)$/)) {
    const cacheKey = new Request(url.toString(), request)
    const cachedResponse = await caches.default.match(cacheKey)
    
    if (cachedResponse) {
      return cachedResponse
    }
    
    const response = await fetch(request)
    const cacheResponse = new Response(response.body, response)
    cacheResponse.headers.set('Cache-Control', 'public, max-age=31536000')
    
    return cacheResponse
  }
  
  return fetch(request)
}
```

## Deployment Troubleshooting

**Common problems during deployment and their solutions**

### Build Failures

**Symptom:** Build process fails with errors not present in development.

**Common causes:**
- Environment variable missing
- Dependency version mismatch
- Build optimization issues
- Memory/resource limits

**Quick fix:**
```
"Build failing in production but works in development:

BUILD ERROR:
[error message from build log]

ENVIRONMENT:
- Development: Node 18.16.0, works fine
- Production: [platform, Node version]

RECENT CHANGES:
[what was changed before failure]

Check:
1. Environment variables (are all set in production?)
2. Dependency versions (package-lock.json committed?)
3. Build configuration (vite.config.ts, next.config.js, etc.)
4. Memory limits (increase if needed)
5. Missing files (.gitignore hiding required files?)"
```

**Prevention:**
- Test build locally: `npm run build`
- Commit package-lock.json/yarn.lock
- Document all required environment variables
- Test in staging environment first

---

### Environment-Specific Issues

**Symptom:** Code works locally but fails in production.

**Quick diagnosis:**
```bash
# Check environment variables
"List all environment variables used in code"

# Check configuration differences
"Compare development vs production configs"

# Check dependencies
"Check if all dependencies available in production"
```

**Quick fix:**
```
"Works in development, fails in production:

ERROR IN PRODUCTION:
[error message]

ENVIRONMENT DIFFERENCES:
Development:
- Database: localhost:5432
- API URL: http://localhost:3000
- Node ENV: development

Production:
- Database: [production DB URL]
- API URL: [production URL]
- Node ENV: production

SUSPECTED ISSUE:
[What might be different]

Debug and fix environment-specific issue."
```

**Common environment issues:**
- Database connection strings
- API endpoints (localhost vs production)
- CORS configuration
- File paths (absolute vs relative)
- SSL/HTTPS requirements

---

### DNS/Domain Problems

**Symptom:** Domain not pointing to deployment, or SSL certificate issues.

**Quick diagnosis:**
```bash
# Check DNS propagation
dig yourdomain.com
nslookup yourdomain.com

# Check DNS records
# Should show:
# A record → Your server IP
# or CNAME → Your hosting platform
```

**Quick fix (Cloudflare Pages):**
```
1. Add custom domain in Cloudflare Pages dashboard
2. Add DNS records:
   - yourdomain.com → CNAME → your-project.pages.dev
   - www.yourdomain.com → CNAME → your-project.pages.dev
3. Enable "Automatic HTTPS Rewrites"
4. Wait for SSL certificate (5-30 minutes)
5. Test: https://yourdomain.com
```

**Prevention:**
- Set up DNS before announcing site
- Wait 24-48h for full DNS propagation
- Test both www and non-www versions
- Enable SSL/HTTPS from start

---

### Deployment Pipeline Failures

**Symptom:** CI/CD pipeline fails during deployment.

**Quick diagnosis:**
```bash
# Check pipeline logs
# Look for:
- Failed tests
- Build errors
- Deployment errors
- Permission issues
```

**Quick fix:**
```
"CI/CD pipeline failing:

PIPELINE LOG:
[relevant error from CI/CD]

STAGE THAT FAILS:
- [ ] Tests
- [ ] Build
- [ ] Deploy
- [ ] Post-deploy checks

SUSPECTED CAUSE:
[hypothesis]

Fix the pipeline configuration."
```

**Common pipeline issues:**
- Tests failing in CI but passing locally
- Missing environment variables in CI
- Different Node/dependency versions
- Insufficient permissions
- Timeout limits exceeded

---

### Performance Degradation After Deployment

**Symptom:** Site is slow in production despite being fast locally.

**Quick diagnosis:**
```
Use Chrome DevTools (on production site):
1. Open Network tab
2. Hard refresh (Cmd+Shift+R / Ctrl+Shift+R)
3. Check:
   - Total load time
   - Largest requests
   - Failed requests
   - Slow API calls

Use Lighthouse:
1. Run Lighthouse audit
2. Check Core Web Vitals:
   - LCP (should be <2.5s)
   - FID (should be <100ms)
   - CLS (should be <0.1)
```

**Quick fixes:**
```
Common performance issues in production:

1. Images not optimized
   - Solution: Use image optimization service
   - Solution: Use modern formats (WebP, AVIF)
   - Solution: Implement lazy loading

2. No caching
   - Solution: Configure cache headers
   - Solution: Enable CDN caching
   - Solution: Use service workers

3. Slow API calls
   - Solution: Add database indexes
   - Solution: Implement caching (Redis)
   - Solution: Use CDN for static data

4. Large bundle sizes
   - Solution: Code splitting
   - Solution: Tree shaking
   - Solution: Remove unused dependencies

5. No compression
   - Solution: Enable gzip/brotli compression
   - Solution: Configure in hosting platform
```

---

### Database Connection Issues

**Symptom:** Can't connect to database from production.

**Quick fix:**
```
"Database connection failing in production:

ERROR:
[connection error message]

CONFIGURATION:
- Database host: [host]
- Port: [port]
- SSL required: [yes/no]
- Firewall rules: [configured?]

CONNECTION STRING:
[connection string with password redacted]

Check:
1. Database server running and accessible
2. Firewall allows connections from production server
3. Database credentials correct in environment variables
4. SSL/TLS configured if required
5. Connection pool settings appropriate
6. Database not at connection limit"
```

**Prevention:**
- Test database connection from production environment before deploying
- Use connection pooling
- Set reasonable connection limits
- Monitor connection count
- Enable database logs for debugging

---

### Rollback Procedures

**When to rollback:**
- Critical bug discovered in production
- Performance severely degraded
- Data corruption risk
- Security vulnerability

**Quick rollback (Cloudflare Pages):**
```bash
# Via Dashboard:
1. Go to Cloudflare Pages dashboard
2. Select your project
3. View deployments
4. Click "Rollback" on previous stable deployment

# Via CLI:
wrangler pages deployment list
wrangler pages deployment rollback [DEPLOYMENT_ID]
```

**Quick rollback (Git-based):**
```bash
# Find last good commit
git log --oneline

# Revert to last good commit
git revert [bad-commit-hash]
git push origin main

# Or hard reset (if safe)
git reset --hard [last-good-commit]
git push --force origin main
```

**After rollback:**
1. Notify users if needed
2. Document what went wrong
3. Fix issue in development
4. Test thoroughly
5. Deploy fix

---

### Deployment Checklist

Before deploying to production:

**Pre-Deployment:**
- [ ] All tests passing locally
- [ ] Build succeeds locally (`npm run build`)
- [ ] Tested in staging environment
- [ ] Environment variables documented
- [ ] Database migrations ready (if any)
- [ ] Rollback plan prepared

**Configuration:**
- [ ] Production environment variables set
- [ ] Database connection configured
- [ ] API endpoints point to production
- [ ] CORS configured correctly
- [ ] SSL/HTTPS enabled
- [ ] Domain DNS configured

**Post-Deployment:**
- [ ] Deployment successful (check logs)
- [ ] Site accessible at domain
- [ ] Core functionality works
- [ ] API calls working
- [ ] Database operations working
- [ ] No console errors
- [ ] Performance acceptable
- [ ] SSL certificate valid

**Monitoring:**
- [ ] Error tracking enabled (Sentry, etc.)
- [ ] Performance monitoring active
- [ ] Uptime monitoring configured
- [ ] Backup system running
- [ ] Logs accessible

---

## Pre-requisites & Next Steps

**Requires completion of:**
- [Phase 3: Testing & Debugging](./phase-3-testing-debugging.md) — Comprehensive QA completed
- [Core Technologies setup](../core-technologies.md) — Production-ready codebase
- [Hosting Tools configuration](../hosting-tools/README.md) — Infrastructure decisions made
- [Business requirements finalized](../introduction/README.md) — Client deliverables defined

**Completed Workflow:**
- ✅ [Phase 0: Preparation](./phase-0-vibecoder-preparation.md) — Tools and mindset ready
- ✅ [Phase 1: Planning](./phase-1-planning.md) — Specifications complete
- ✅ [Phase 2: Development](./phase-2-development.md) — Features implemented
- ✅ [Phase 3: Testing](./phase-3-testing-debugging.md) — Quality assurance passed
- ✅ [Phase 4: Deployment](./phase-4-deployment.md) — Production ready

**Business Implementation:**
- [Client handover documentation](#client-project-considerations) — Project delivery
- [Maintenance plan establishment](#maintenance--updates) — Ongoing support
- [Performance monitoring](#performance-optimization-post-deployment) — Success metrics

**Related Reading:**
- [Hosting Tools](../hosting-tools/README.md) — Complete hosting platform guide
- [Business Strategy](../introduction/README.md) — Freelance and client management
- [Context Management](../context-management/README.md) — Project handover workflows

Back: [Phase 3 → Testing, Debugging & Code Review](./phase-3-testing-debugging.md)

Next: [Introduction → Business Model](../introduction/README.md)
