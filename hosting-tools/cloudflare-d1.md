# Cloudflare D1 Database

## Overview

Cloudflare D1 is a serverless SQL database built on SQLite, designed to run on Cloudflare's global network. It's specifically optimized for Workers and Pages Functions, providing a native database solution that's fast, scalable, and incredibly cost-effective.

## Key Benefits

### SQLite-Based Power
- **Full SQL support** - Standard SQLite syntax
- **ACID compliance** - Reliable transactions
- **Joins, indexes, constraints** - All standard SQL features
- **JSON support** - Store and query JSON data
- **Foreign keys** - Maintain data integrity

### Edge-Native Integration
- **Zero cold starts** - Always ready
- **Native Workers binding** - No connection strings
- **Global replication** - Data close to users (coming soon)
- **Automatic backups** - Point-in-time recovery
- **Read replicas** - Scale reads globally

### Incredibly Cheap & Scalable
- **Super generous free tier**
- **Linear pricing** - Predictable costs
- **No per-database charges** - Pay per usage
- **Scales automatically** - No capacity planning
- **Superior performance** - Edge latency

### Perfect for Micro-SaaS
- **Start free** - Zero upfront costs
- **Grow with your app** - Smooth scaling
- **Production-ready** - Enterprise reliability
- **Fast queries** - Sub-10ms latency
- **Easy migrations** - Standard SQL

## Pricing

### Free Tier (Very Generous)
- **5 GB storage** per account
- **5 million rows read** per day
- **100,000 rows written** per day
- **Unlimited databases**
- Perfect for side projects and micro-SaaS

### Paid Plan ($5/month)
When you exceed free tier:
- **25 billion rows read** per month ($0.001 per million after)
- **50 million rows written** per month ($1.00 per million after)
- **5 GB storage** included ($0.75 per GB after)

### Cost Reality Check

**Small SaaS** (1,000 active users):
- ~500K reads/day = 15M reads/month
- ~50K writes/day = 1.5M writes/month
- ~1 GB storage
- **Cost: $0** (within free tier!)

**Growing SaaS** (10,000 users):
- ~5M reads/day = 150M reads/month
- ~500K writes/day = 15M writes/month
- ~10 GB storage
- **Cost: $5-10/month**

**Comparison**:
- **AWS RDS**: $50-200/month minimum
- **PlanetScale**: $29+/month
- **Supabase**: $25+/month
- **D1**: $0-10/month for same workload

**D1 is 5-20x cheaper** than alternatives!

## Getting Started

### Prerequisites
- Cloudflare account
- Wrangler CLI installed (`npm install -g wrangler`)
- Worker or Pages project

### Creating Your First Database

```bash
# Create a new D1 database
wrangler d1 create my-database

# Output shows:
[[d1_databases]]
binding = "DB"
database_name = "my-database"
database_id = "xxxx-xxxx-xxxx-xxxx"

# Copy this to your wrangler.toml
```

### Add to wrangler.toml

```toml
name = "my-worker"
main = "src/index.ts"
compatibility_date = "2024-01-01"

[[d1_databases]]
binding = "DB"
database_name = "my-database"
database_id = "your-database-id-here"
```

### Create Schema

Create a `schema.sql` file:

```sql
-- schema.sql
CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  email TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  password_hash TEXT NOT NULL,
  created_at INTEGER DEFAULT (strftime('%s', 'now')),
  updated_at INTEGER DEFAULT (strftime('%s', 'now'))
);

CREATE INDEX idx_users_email ON users(email);

CREATE TABLE IF NOT EXISTS subscriptions (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  plan TEXT NOT NULL CHECK(plan IN ('free', 'pro', 'enterprise')),
  status TEXT NOT NULL CHECK(status IN ('active', 'cancelled', 'expired')),
  started_at INTEGER NOT NULL,
  expires_at INTEGER,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

CREATE INDEX idx_subscriptions_user_id ON subscriptions(user_id);
CREATE INDEX idx_subscriptions_status ON subscriptions(status);

CREATE TABLE IF NOT EXISTS api_keys (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  key TEXT UNIQUE NOT NULL,
  name TEXT,
  last_used_at INTEGER,
  created_at INTEGER DEFAULT (strftime('%s', 'now')),
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

CREATE INDEX idx_api_keys_key ON api_keys(key);
```

### Apply Schema

```bash
# For production database
wrangler d1 execute my-database --file=schema.sql

# For local development (uses --local flag)
wrangler d1 execute my-database --local --file=schema.sql
```

## Basic Usage in Workers

### Simple Query Example

```typescript
interface Env {
  DB: D1Database;
}

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    // Get all users
    if (url.pathname === '/api/users') {
      const { results } = await env.DB.prepare(
        'SELECT id, email, name, created_at FROM users ORDER BY created_at DESC'
      ).all();

      return Response.json(results);
    }

    // Get single user
    if (url.pathname.startsWith('/api/users/')) {
      const userId = url.pathname.split('/')[3];

      const user = await env.DB.prepare(
        'SELECT id, email, name, created_at FROM users WHERE id = ?'
      ).bind(userId).first();

      if (!user) {
        return Response.json({ error: 'User not found' }, { status: 404 });
      }

      return Response.json(user);
    }

    return new Response('Not found', { status: 404 });
  },
};
```

### Insert Data

```typescript
// Create new user
if (url.pathname === '/api/users' && request.method === 'POST') {
  const { email, name, password } = await request.json();

  // Hash password (use bcrypt or similar in production)
  const passwordHash = await hashPassword(password);

  const result = await env.DB.prepare(
    'INSERT INTO users (email, name, password_hash) VALUES (?, ?, ?)'
  ).bind(email, name, passwordHash).run();

  if (!result.success) {
    return Response.json(
      { error: 'Failed to create user' },
      { status: 500 }
    );
  }

  return Response.json({
    success: true,
    userId: result.meta.last_row_id,
  });
}
```

### Update Data

```typescript
// Update user
if (url.pathname.startsWith('/api/users/') && request.method === 'PUT') {
  const userId = url.pathname.split('/')[3];
  const { name } = await request.json();

  const result = await env.DB.prepare(
    'UPDATE users SET name = ?, updated_at = strftime(\'%s\', \'now\') WHERE id = ?'
  ).bind(name, userId).run();

  if (result.meta.changes === 0) {
    return Response.json({ error: 'User not found' }, { status: 404 });
  }

  return Response.json({ success: true });
}
```

### Delete Data

```typescript
// Delete user
if (url.pathname.startsWith('/api/users/') && request.method === 'DELETE') {
  const userId = url.pathname.split('/')[3];

  const result = await env.DB.prepare(
    'DELETE FROM users WHERE id = ?'
  ).bind(userId).run();

  if (result.meta.changes === 0) {
    return Response.json({ error: 'User not found' }, { status: 404 });
  }

  return Response.json({ success: true });
}
```

## Advanced Queries

### Joins

```typescript
// Get user with their subscription
async function getUserWithSubscription(userId: string, db: D1Database) {
  const result = await db.prepare(`
    SELECT
      u.id,
      u.email,
      u.name,
      s.plan,
      s.status,
      s.expires_at
    FROM users u
    LEFT JOIN subscriptions s ON u.id = s.user_id
    WHERE u.id = ? AND (s.status = 'active' OR s.status IS NULL)
  `).bind(userId).first();

  return result;
}
```

### Aggregations

```typescript
// Get user count by subscription plan
async function getSubscriptionStats(db: D1Database) {
  const { results } = await db.prepare(`
    SELECT
      plan,
      COUNT(*) as user_count,
      SUM(CASE WHEN status = 'active' THEN 1 ELSE 0 END) as active_count
    FROM subscriptions
    GROUP BY plan
    ORDER BY user_count DESC
  `).all();

  return results;
}
```

### Pagination

```typescript
async function getUsers(page: number, limit: number, db: D1Database) {
  const offset = (page - 1) * limit;

  const { results } = await db.prepare(`
    SELECT id, email, name, created_at
    FROM users
    ORDER BY created_at DESC
    LIMIT ? OFFSET ?
  `).bind(limit, offset).all();

  // Get total count
  const { total } = await db.prepare(
    'SELECT COUNT(*) as total FROM users'
  ).first() as { total: number };

  return {
    users: results,
    pagination: {
      page,
      limit,
      total,
      totalPages: Math.ceil(total / limit),
    },
  };
}
```

### Full-Text Search

```typescript
// Create FTS table
await db.prepare(`
  CREATE VIRTUAL TABLE IF NOT EXISTS posts_fts USING fts5(
    title,
    content,
    content='posts',
    content_rowid='id'
  )
`).run();

// Search posts
async function searchPosts(query: string, db: D1Database) {
  const { results } = await db.prepare(`
    SELECT p.*, rank
    FROM posts_fts
    JOIN posts p ON posts_fts.rowid = p.id
    WHERE posts_fts MATCH ?
    ORDER BY rank
    LIMIT 20
  `).bind(query).all();

  return results;
}
```

## Transactions

```typescript
async function transferCredits(
  fromUserId: string,
  toUserId: string,
  amount: number,
  db: D1Database
) {
  try {
    // Start transaction
    await db.prepare('BEGIN TRANSACTION').run();

    // Deduct from sender
    await db.prepare(
      'UPDATE users SET credits = credits - ? WHERE id = ?'
    ).bind(amount, fromUserId).run();

    // Add to receiver
    await db.prepare(
      'UPDATE users SET credits = credits + ? WHERE id = ?'
    ).bind(amount, toUserId).run();

    // Record transaction
    await db.prepare(
      'INSERT INTO transactions (from_user_id, to_user_id, amount) VALUES (?, ?, ?)'
    ).bind(fromUserId, toUserId, amount).run();

    // Commit
    await db.prepare('COMMIT').run();

    return { success: true };

  } catch (error) {
    // Rollback on error
    await db.prepare('ROLLBACK').run();
    throw error;
  }
}
```

## Batch Operations

```typescript
// Insert multiple records efficiently
async function batchInsertUsers(users: Array<{ email: string, name: string }>, db: D1Database) {
  const statements = users.map(user =>
    db.prepare(
      'INSERT INTO users (email, name, password_hash) VALUES (?, ?, ?)'
    ).bind(user.email, user.name, 'temporary-hash')
  );

  // Execute all in one batch
  const results = await db.batch(statements);

  return {
    success: true,
    count: results.length,
  };
}
```

## JSON Support

```typescript
// Store JSON data
await db.prepare(`
  CREATE TABLE IF NOT EXISTS settings (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL,
    preferences TEXT NOT NULL, -- JSON stored as TEXT
    FOREIGN KEY (user_id) REFERENCES users(id)
  )
`).run();

// Insert JSON
async function saveUserPreferences(userId: string, preferences: object, db: D1Database) {
  await db.prepare(
    'INSERT OR REPLACE INTO settings (user_id, preferences) VALUES (?, ?)'
  ).bind(userId, JSON.stringify(preferences)).run();
}

// Query JSON
async function getUserPreferences(userId: string, db: D1Database) {
  const result = await db.prepare(
    'SELECT preferences FROM settings WHERE user_id = ?'
  ).bind(userId).first();

  if (!result) return null;

  return JSON.parse(result.preferences as string);
}

// Query JSON fields (SQLite JSON functions)
async function getUsersByTheme(theme: string, db: D1Database) {
  const { results } = await db.prepare(`
    SELECT u.id, u.name
    FROM users u
    JOIN settings s ON u.id = s.user_id
    WHERE json_extract(s.preferences, '$.theme') = ?
  `).bind(theme).all();

  return results;
}
```

## Using with Pages Functions

```typescript
// functions/api/users/[id].ts

interface Env {
  DB: D1Database;
}

export const onRequestGet: PagesFunction<Env> = async (context) => {
  const userId = context.params.id as string;

  const user = await context.env.DB.prepare(
    'SELECT id, email, name FROM users WHERE id = ?'
  ).bind(userId).first();

  if (!user) {
    return Response.json({ error: 'User not found' }, { status: 404 });
  }

  return Response.json(user);
};

export const onRequestPut: PagesFunction<Env> = async (context) => {
  const userId = context.params.id as string;
  const { name } = await context.request.json();

  await context.env.DB.prepare(
    'UPDATE users SET name = ? WHERE id = ?'
  ).bind(name, userId).run();

  return Response.json({ success: true });
};
```

## Local Development

```bash
# Run worker with local D1
wrangler dev --local

# Execute SQL locally
wrangler d1 execute my-database --local --command="SELECT * FROM users"

# Import data locally
wrangler d1 execute my-database --local --file=seed.sql
```

### Seed Data for Development

```sql
-- seed.sql
INSERT INTO users (email, name, password_hash) VALUES
  ('alice@example.com', 'Alice', 'hash1'),
  ('bob@example.com', 'Bob', 'hash2'),
  ('charlie@example.com', 'Charlie', 'hash3');

INSERT INTO subscriptions (user_id, plan, status, started_at) VALUES
  (1, 'pro', 'active', strftime('%s', 'now')),
  (2, 'free', 'active', strftime('%s', 'now')),
  (3, 'enterprise', 'active', strftime('%s', 'now'));
```

```bash
# Load seed data
wrangler d1 execute my-database --local --file=seed.sql
```

## Migrations

### Managing Schema Changes

Create migration files:

```sql
-- migrations/001_initial.sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  email TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  created_at INTEGER DEFAULT (strftime('%s', 'now'))
);

-- migrations/002_add_subscriptions.sql
CREATE TABLE subscriptions (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  plan TEXT NOT NULL,
  status TEXT NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

-- migrations/003_add_api_keys.sql
CREATE TABLE api_keys (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  key TEXT UNIQUE NOT NULL,
  created_at INTEGER DEFAULT (strftime('%s', 'now')),
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

Apply migrations:

```bash
# Apply each migration in order
wrangler d1 execute my-database --file=migrations/001_initial.sql
wrangler d1 execute my-database --file=migrations/002_add_subscriptions.sql
wrangler d1 execute my-database --file=migrations/003_add_api_keys.sql
```

## Ensuring It Works

### Testing Checklist

1. **Local Testing**:
   ```bash
   # Start dev server
   wrangler dev --local

   # Test endpoints
   curl http://localhost:8787/api/users
   ```

2. **Verify Schema**:
   ```bash
   # Check tables
   wrangler d1 execute my-database --command="SELECT name FROM sqlite_master WHERE type='table'"

   # Check indexes
   wrangler d1 execute my-database --command="SELECT name FROM sqlite_master WHERE type='index'"
   ```

3. **Test Queries**:
   ```bash
   # Test data insertion
   wrangler d1 execute my-database --command="INSERT INTO users (email, name, password_hash) VALUES ('test@example.com', 'Test User', 'hash')"

   # Verify data
   wrangler d1 execute my-database --command="SELECT * FROM users"
   ```

4. **Production Deployment**:
   ```bash
   # Deploy worker
   wrangler deploy

   # Test production endpoint
   curl https://my-worker.workers.dev/api/users
   ```

### Monitoring

```bash
# View real-time logs
wrangler tail

# Check metrics in dashboard:
# - Query count
# - Storage usage
# - Error rates
```

### Common Issues & Solutions

**Database not found:**
- Verify `database_id` in `wrangler.toml`
- Check binding name matches code
- Confirm database exists: `wrangler d1 list`

**Schema not applied:**
- Re-run schema file: `wrangler d1 execute db-name --file=schema.sql`
- Check for SQL syntax errors

**Slow queries:**
- Add indexes on frequently queried columns
- Use `EXPLAIN QUERY PLAN` to analyze queries
- Consider denormalization for complex joins

## Efficient Usage Tips

### 1. Use Indexes Wisely

```sql
-- Index frequently queried columns
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_subscriptions_user_status ON subscriptions(user_id, status);

-- Composite indexes for complex queries
CREATE INDEX idx_api_keys_user_last_used ON api_keys(user_id, last_used_at);
```

### 2. Optimize Queries

```typescript
// Bad - N+1 query problem
for (const user of users) {
  const subscription = await db.prepare(
    'SELECT * FROM subscriptions WHERE user_id = ?'
  ).bind(user.id).first();
}

// Good - Single query with join
const { results } = await db.prepare(`
  SELECT u.*, s.plan, s.status
  FROM users u
  LEFT JOIN subscriptions s ON u.id = s.user_id
  WHERE u.id IN (?, ?, ?)
`).bind(...userIds).all();
```

### 3. Cache Frequent Queries in KV

```typescript
async function getUserCached(userId: string, env: Env) {
  // Try cache first
  const cached = await env.KV.get(`user:${userId}`, 'json');
  if (cached) return cached;

  // Query database
  const user = await env.DB.prepare(
    'SELECT * FROM users WHERE id = ?'
  ).bind(userId).first();

  // Cache for 5 minutes
  await env.KV.put(`user:${userId}`, JSON.stringify(user), {
    expirationTtl: 300,
  });

  return user;
}
```

### 4. Use Prepared Statements

```typescript
// Reuse prepared statements for better performance
const getUserStmt = env.DB.prepare(
  'SELECT * FROM users WHERE id = ?'
);

// Execute multiple times
const user1 = await getUserStmt.bind('1').first();
const user2 = await getUserStmt.bind('2').first();
```

### 5. Batch Operations

```typescript
// Bad - Multiple individual operations
for (const user of users) {
  await db.prepare(
    'INSERT INTO users (email, name) VALUES (?, ?)'
  ).bind(user.email, user.name).run();
}

// Good - Batch operation
const statements = users.map(user =>
  db.prepare('INSERT INTO users (email, name) VALUES (?, ?)').bind(user.email, user.name)
);
await db.batch(statements);
```

## Real-World Example: Micro-SaaS API

Complete example of a URL shortener with analytics:

```typescript
interface Env {
  DB: D1Database;
  KV: KVNamespace;
}

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    // Redirect short URL
    if (url.pathname.startsWith('/s/')) {
      const code = url.pathname.slice(3);

      // Check cache
      let targetUrl = await env.KV.get(`link:${code}`);

      if (!targetUrl) {
        // Get from database
        const link = await env.DB.prepare(
          'SELECT url FROM links WHERE code = ? AND active = 1'
        ).bind(code).first() as { url: string } | null;

        if (!link) {
          return new Response('Link not found', { status: 404 });
        }

        targetUrl = link.url;
        await env.KV.put(`link:${code}`, targetUrl, { expirationTtl: 3600 });
      }

      // Track click
      await env.DB.prepare(
        'INSERT INTO clicks (link_code, clicked_at, user_agent, country) VALUES (?, ?, ?, ?)'
      ).bind(code, Date.now(), request.headers.get('user-agent'), request.cf?.country).run();

      return Response.redirect(targetUrl, 301);
    }

    // Create short link
    if (url.pathname === '/api/shorten' && request.method === 'POST') {
      const { url: targetUrl, customCode } = await request.json();

      const code = customCode || generateCode(6);

      // Check if code exists
      const existing = await env.DB.prepare(
        'SELECT 1 FROM links WHERE code = ?'
      ).bind(code).first();

      if (existing) {
        return Response.json({ error: 'Code already exists' }, { status: 400 });
      }

      // Create link
      await env.DB.prepare(
        'INSERT INTO links (code, url, created_at, active) VALUES (?, ?, ?, 1)'
      ).bind(code, targetUrl, Date.now()).run();

      return Response.json({
        shortUrl: `${url.origin}/s/${code}`,
        code,
      });
    }

    // Get link analytics
    if (url.pathname.startsWith('/api/analytics/')) {
      const code = url.pathname.split('/')[3];

      const stats = await env.DB.prepare(`
        SELECT
          COUNT(*) as total_clicks,
          COUNT(DISTINCT country) as unique_countries,
          DATE(clicked_at / 1000, 'unixepoch') as date,
          COUNT(*) as clicks_per_day
        FROM clicks
        WHERE link_code = ?
        GROUP BY date
        ORDER BY date DESC
        LIMIT 30
      `).bind(code).all();

      return Response.json(stats.results);
    }

    return new Response('Not found', { status: 404 });
  },
};

function generateCode(length: number): string {
  const chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
  return Array.from({ length }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
}
```

## Official Resources

- **Documentation**: https://developers.cloudflare.com/d1/
- **API Reference**: https://developers.cloudflare.com/d1/platform/client-api/
- **Pricing**: https://developers.cloudflare.com/d1/platform/pricing/
- **Examples**: https://developers.cloudflare.com/d1/examples/
- **SQLite Reference**: https://www.sqlite.org/docs.html
- **Discord Community**: https://discord.cloudflare.com

## Why D1 is Perfect for Micro-SaaS

1. **Zero to production fast** - Create database in minutes
2. **SQLite simplicity** - No complex setup
3. **Edge performance** - Sub-10ms queries
4. **Incredibly cheap** - $0-10/month for most apps
5. **Native Workers integration** - No connection strings
6. **Scales automatically** - No capacity planning
7. **Full SQL power** - Not limited like NoSQL
8. **Production-ready** - Enterprise reliability

For micro-SaaS applications and modern web apps, D1 provides the perfect balance of simplicity, performance, and cost-effectiveness. Combined with Workers, Pages, KV, and R2, you have a complete edge-native stack that can scale from zero to millions of users while keeping costs incredibly low.
