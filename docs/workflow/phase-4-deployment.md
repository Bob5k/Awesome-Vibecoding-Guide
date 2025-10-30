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


## Automated deployment
Setup CI/CD

`git push` → automatic deploy

Back: [Phase 3 → Testing, Debugging & Code Review](./phase-3-testing-debugging.md)
