# Cloudflare Workers

## Overview

Cloudflare Workers is a serverless execution environment that runs JavaScript, TypeScript, Python, and WebAssembly at the edge. Unlike traditional serverless platforms, Workers run on Cloudflare's global network in 300+ locations, providing ultra-low latency for users worldwide.

## Key Benefits

### Full Web Application Hosting
Unlike Pages (static only), Workers let you:
- **Build complete web applications** with backend logic
- **Connect to databases** (D1, PostgreSQL, etc.)
- **Handle API requests** and complex business logic
- **Process payments**, send emails, authenticate users
- **Host SaaS applications** end-to-end

### Edge Computing Advantage
- **Sub-50ms response times** globally
- **No cold starts** (instant execution)
- **Runs close to users** on Cloudflare's network
- **Scales automatically** to millions of requests
- **Built-in DDoS protection**

### Generous Free Tier
- **100,000 requests per day** (free)
- **10ms CPU time per request** (free tier)
- Perfect for micro-SaaS applications
- Many apps never exceed free tier
- When you do, scaling is cheap

### Affordable Scaling
**Paid Plan** ($5/month):
- 10 million requests included
- Additional requests: $0.50 per million
- 50ms CPU time per request

**Example Cost Calculation**:
- 500k requests/day = ~15M/month
- Cost: $5 base + $2.50 overage = $7.50/month
- That's incredibly cheap for a production SaaS!

## Perfect Use Cases

### 1. Micro-SaaS Applications
- URL shorteners
- Image optimization services
- API gateways
- Webhook processors
- Data transformation services

### 2. Full-Stack Applications
- E-commerce platforms
- Booking systems
- CRM applications
- Project management tools
- Social platforms

### 3. API Services
- RESTful APIs
- GraphQL servers
- Real-time data processing
- Third-party integrations
- Authentication services

### 4. Middleware & Proxies
- A/B testing
- Feature flags
- Request routing
- Header manipulation
- Security layers

## Getting Started

### Prerequisites
- Node.js 18+ installed
- Cloudflare account (free)
- Basic JavaScript/TypeScript knowledge

### Installation

```bash
# Install Wrangler (Cloudflare Workers CLI)
npm install -g wrangler

# Verify installation
wrangler --version
```

### Authentication

```bash
# Login to Cloudflare
wrangler login

# This opens browser for authentication
# After auth, you're ready to deploy
```

### Create Your First Worker

```bash
# Create new Worker project
npm create cloudflare@latest my-worker

# Follow the prompts:
# - Choose "Hello World" Worker template
# - TypeScript or JavaScript
# - Git initialization (yes)
```

### Project Structure

```
my-worker/
├── src/
│   └── index.ts          # Your Worker code
├── wrangler.toml         # Configuration file
├── package.json
└── tsconfig.json
```

### Basic Worker Example

```typescript
// src/index.ts

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    // Handle different routes
    if (url.pathname === '/') {
      return new Response('Hello from Cloudflare Workers!', {
        headers: { 'Content-Type': 'text/plain' }
      });
    }

    if (url.pathname === '/api/data') {
      const data = { message: 'API working!', timestamp: Date.now() };
      return Response.json(data);
    }

    return new Response('Not found', { status: 404 });
  }
};
```

### Configuration

```toml
# wrangler.toml

name = "my-worker"
main = "src/index.ts"
compatibility_date = "2024-01-01"

# Environment variables
[vars]
ENVIRONMENT = "production"

# Bind D1 Database
[[d1_databases]]
binding = "DB"
database_name = "my-database"
database_id = "your-database-id"

# Bind KV namespace
[[kv_namespaces]]
binding = "KV"
id = "your-kv-id"

# Bind R2 bucket
[[r2_buckets]]
binding = "STORAGE"
bucket_name = "my-bucket"
```

## Deploying Your Worker

### Development

```bash
# Run locally with hot reload
npm run dev

# Or with wrangler directly
wrangler dev

# Access at http://localhost:8787
```

### Production Deployment

```bash
# Deploy to Cloudflare
npm run deploy

# Or
wrangler deploy

# Your Worker is now live!
# URL: https://my-worker.your-subdomain.workers.dev
```

### Custom Domains

```bash
# Add custom domain via Wrangler
wrangler domains add api.yourdomain.com

# Or in Cloudflare Dashboard:
# Workers & Pages > my-worker > Triggers > Custom Domains
```

## Connecting to D1 Database

### Setup D1 with Workers

```bash
# Create D1 database
wrangler d1 create my-database

# This outputs your database_id
# Add it to wrangler.toml

# Create schema
wrangler d1 execute my-database --file=schema.sql
```

### Schema Example

```sql
-- schema.sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  email TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  created_at INTEGER DEFAULT (strftime('%s', 'now'))
);

CREATE TABLE subscriptions (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  plan TEXT NOT NULL,
  status TEXT NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Using D1 in Worker

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const { pathname } = new URL(request.url);

    if (pathname === '/api/users') {
      // Query database
      const { results } = await env.DB.prepare(
        'SELECT * FROM users LIMIT 10'
      ).all();

      return Response.json(results);
    }

    if (pathname === '/api/user/create' && request.method === 'POST') {
      const { email, name } = await request.json();

      // Insert into database
      const result = await env.DB.prepare(
        'INSERT INTO users (email, name) VALUES (?, ?)'
      ).bind(email, name).run();

      return Response.json({
        success: true,
        userId: result.meta.last_row_id
      });
    }

    return new Response('Not found', { status: 404 });
  }
};
```

## Building a Micro-SaaS Example

### URL Shortener with D1

```typescript
interface Env {
  DB: D1Database;
  KV: KVNamespace;
}

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    // Redirect shortened URL
    if (url.pathname.startsWith('/s/')) {
      const code = url.pathname.slice(3);

      // Check cache first
      let targetUrl = await env.KV.get(`short:${code}`);

      if (!targetUrl) {
        // Fallback to database
        const result = await env.DB.prepare(
          'SELECT url FROM links WHERE code = ?'
        ).bind(code).first();

        if (result) {
          targetUrl = result.url as string;
          // Cache for next time
          await env.KV.put(`short:${code}`, targetUrl, {
            expirationTtl: 3600
          });
        }
      }

      if (targetUrl) {
        // Track click
        await env.DB.prepare(
          'UPDATE links SET clicks = clicks + 1 WHERE code = ?'
        ).bind(code).run();

        return Response.redirect(targetUrl, 301);
      }

      return new Response('Short link not found', { status: 404 });
    }

    // Create shortened URL
    if (url.pathname === '/api/shorten' && request.method === 'POST') {
      const { url: targetUrl } = await request.json();

      // Generate random code
      const code = generateCode(6);

      // Store in database
      await env.DB.prepare(
        'INSERT INTO links (code, url, clicks) VALUES (?, ?, 0)'
      ).bind(code, targetUrl).run();

      return Response.json({
        shortUrl: `${url.origin}/s/${code}`,
        code
      });
    }

    return new Response('Not found', { status: 404 });
  }
};

function generateCode(length: number): string {
  const chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
  let result = '';
  for (let i = 0; i < length; i++) {
    result += chars.charAt(Math.floor(Math.random() * chars.length));
  }
  return result;
}
```

## Environment Variables & Secrets

### Adding Secrets

```bash
# Add secret (not visible in wrangler.toml)
wrangler secret put API_KEY
# Enter the value when prompted

# Add another secret
wrangler secret put STRIPE_SECRET_KEY

# List secrets
wrangler secret list
```

### Using Secrets in Code

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    // Access secrets via env
    const apiKey = env.API_KEY;
    const stripeKey = env.STRIPE_SECRET_KEY;

    // Use for API calls
    const response = await fetch('https://api.example.com/data', {
      headers: {
        'Authorization': `Bearer ${apiKey}`
      }
    });

    return response;
  }
};
```

## Ensuring It Works

### Testing Checklist

1. **Local Testing**:
   ```bash
   wrangler dev
   # Test all endpoints locally
   curl http://localhost:8787/api/test
   ```

2. **Check Logs**:
   ```bash
   # Real-time logs
   wrangler tail

   # Or in dashboard:
   # Workers & Pages > my-worker > Logs
   ```

3. **Test Production**:
   ```bash
   # Deploy first
   wrangler deploy

   # Test production URL
   curl https://my-worker.your-subdomain.workers.dev/api/test
   ```

4. **Monitor Performance**:
   - Check Cloudflare Dashboard
   - View request count
   - Check error rates
   - Monitor CPU time usage

### Common Issues & Solutions

**Worker not updating:**
```bash
# Clear cache and redeploy
wrangler deploy --force
```

**Database connection fails:**
- Verify `database_id` in `wrangler.toml`
- Check D1 binding name matches code
- Run `wrangler d1 list` to confirm database exists

**Exceeded CPU time:**
- Optimize database queries
- Use KV for caching
- Reduce external API calls
- Consider pagination for large datasets

## Efficient Usage Tips

### 1. Cache Aggressively with KV

```typescript
// Cache expensive operations
async function getCachedData(key: string, env: Env) {
  // Try cache first
  let data = await env.KV.get(key, 'json');

  if (!data) {
    // Fetch and cache
    data = await fetchExpensiveData();
    await env.KV.put(key, JSON.stringify(data), {
      expirationTtl: 3600 // 1 hour
    });
  }

  return data;
}
```

### 2. Use Durable Objects for State

For real-time features (chat, collaboration):
```bash
# Enable Durable Objects
wrangler d1 create my-objects
```

### 3. Optimize Database Queries

```typescript
// Bad - Multiple queries
for (const userId of userIds) {
  await env.DB.prepare('SELECT * FROM users WHERE id = ?')
    .bind(userId).first();
}

// Good - Single query
const placeholders = userIds.map(() => '?').join(',');
await env.DB.prepare(`SELECT * FROM users WHERE id IN (${placeholders})`)
  .bind(...userIds).all();
```

### 4. Handle Errors Gracefully

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    try {
      // Your code here
      const result = await processRequest(request, env);
      return Response.json(result);

    } catch (error) {
      console.error('Error:', error);

      return Response.json({
        error: 'Internal server error',
        message: error.message
      }, { status: 500 });
    }
  }
};
```

### 5. Use TypeScript

```typescript
// Define your environment interface
interface Env {
  DB: D1Database;
  KV: KVNamespace;
  STORAGE: R2Bucket;
  API_KEY: string;
  STRIPE_SECRET_KEY: string;
}

// Get full type safety
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    // env.DB is properly typed!
    const result = await env.DB.prepare('SELECT * FROM users').all();
    return Response.json(result);
  }
};
```

## Pricing Reality Check

### Micro-SaaS Scenario
- **100 active users**
- **50 requests per user per day** = 5,000 requests/day
- **150,000 requests/month**
- **Cost**: $0 (within free tier)

### Small SaaS Scenario
- **1,000 active users**
- **50 requests per user per day** = 50,000 requests/day
- **1.5M requests/month**
- **Cost**: $5/month (paid plan)

### Growing SaaS Scenario
- **10,000 active users**
- **50 requests per user per day** = 500,000 requests/day
- **15M requests/month**
- **Cost**: $5 + $2.50 overage = $7.50/month

### Comparison to Alternatives
- **AWS Lambda**: ~$25-50/month at same scale
- **Heroku**: $25-50/month minimum
- **DigitalOcean**: $12+/month for VPS
- **Vercel**: $20+/month for serverless

**Cloudflare Workers is 3-10x cheaper** than alternatives!

## Integration with Cloudflare Services

### Use with Pages Functions
Deploy frontend on Pages, backend logic in Workers:
```typescript
// pages/functions/api/[[path]].ts
export async function onRequest(context) {
  // Access same bindings as Workers
  const result = await context.env.DB.prepare(
    'SELECT * FROM users'
  ).all();

  return Response.json(result);
}
```

### Combined Stack
- **Pages**: Frontend (React/Vue/Astro)
- **Workers**: API layer
- **D1**: Database
- **R2**: File storage
- **KV**: Caching & sessions

All integrated, all cheap, all fast!

## Official Resources

- **Documentation**: https://developers.cloudflare.com/workers/
- **Tutorials**: https://developers.cloudflare.com/workers/tutorials/
- **Examples**: https://github.com/cloudflare/workers-sdk/tree/main/templates
- **Discord Community**: https://discord.cloudflare.com
- **Workers Playground**: https://workers.cloudflare.com/playground

## Real-World Success Stories

Workers power:
- **Discord** - Handles billions of requests
- **Shopify** - Checkout flows
- **Zerodha** - India's largest stockbroker
- Thousands of micro-SaaS applications

## Why It's Perfect for SaaS

1. **Ultra-low startup costs** - Free tier generous
2. **Global from day one** - Edge deployment
3. **Scales automatically** - No infrastructure management
4. **Fast development** - Deploy in seconds
5. **Integrated ecosystem** - D1, KV, R2 work seamlessly
6. **Production-ready** - Enterprise-grade reliability
7. **Cost-effective scaling** - Pricing grows with you

For modern web applications and SaaS products, Cloudflare Workers provides unmatched value in terms of performance, cost, and developer experience.
