# Cloudflare KV (Key-Value Storage)

## Overview

Cloudflare Workers KV is a global, low-latency key-value data store. It's designed for high-read, low-write scenarios where you need to access data quickly from anywhere in the world. KV is eventually consistent and optimized for edge computing.

## Key Benefits

### Global Low-Latency Reads
- **Sub-millisecond reads** from edge locations
- **Global replication** - Data cached at 300+ locations
- **Eventually consistent** - Perfect for cacheable data
- **Optimized for reads** - 1000x faster than database queries

### Simple Key-Value Model
- **Easy to use** - Just keys and values
- **No schema** - Store any data structure
- **JSON support** - Automatic serialization
- **Binary support** - Store images, files, etc.

### Cost-Effective
- **Generous free tier** - 100,000 reads/day
- **Affordable scaling** - $0.50 per million reads
- **No storage limits** on free tier for reasonable usage
- **Global distribution** included

### Perfect Use Cases
- **Session storage** - User sessions and JWT tokens
- **Configuration data** - App settings, feature flags
- **Cache layer** - Database query results, API responses
- **Rate limiting** - Track request counts per user
- **Authentication** - Store hashed passwords, API keys
- **Temporary data** - Upload tokens, email verification codes

## Pricing

### Free Tier
- **100,000 read operations** per day
- **1,000 write operations** per day
- **1,000 delete operations** per day
- **1,000 list operations** per day
- **1 GB stored** (soft limit)

### Paid Plan ($5/month)
When you exceed free tier:
- **10 million reads** included ($0.50 per million after)
- **1 million writes** included ($5.00 per million after)
- **1 million deletes** included ($5.00 per million after)
- **1 million lists** included ($5.00 per million after)
- **Storage**: First 1 GB free, then $0.50 per GB

### Performance Characteristics
- **Read latency**: <1ms (cached at edge)
- **Write latency**: ~100-500ms (global propagation)
- **Consistency**: Eventually consistent (60 seconds globally)
- **Key size**: Up to 512 bytes
- **Value size**: Up to 25 MB

## Getting Started

### Prerequisites
- Cloudflare account
- Wrangler CLI installed
- Worker or Pages project

### Creating KV Namespace

```bash
# Create production KV namespace
wrangler kv:namespace create "CACHE"

# Output:
[[kv_namespaces]]
binding = "CACHE"
id = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Create preview/dev namespace (optional)
wrangler kv:namespace create "CACHE" --preview

# Output for preview:
[[kv_namespaces]]
binding = "CACHE"
preview_id = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### Configure in wrangler.toml

```toml
name = "my-worker"
main = "src/index.ts"

# Production KV namespace
[[kv_namespaces]]
binding = "CACHE"
id = "your-namespace-id"
preview_id = "your-preview-namespace-id"

# You can have multiple namespaces
[[kv_namespaces]]
binding = "SESSIONS"
id = "another-namespace-id"
```

## Basic Operations

### Write (Put)

```typescript
interface Env {
  CACHE: KVNamespace;
}

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    // Store string
    await env.CACHE.put('key', 'value');

    // Store with expiration (1 hour)
    await env.CACHE.put('session:123', 'user-data', {
      expirationTtl: 3600,
    });

    // Store with absolute expiration time
    const expiresAt = Date.now() / 1000 + 3600; // 1 hour from now
    await env.CACHE.put('token:abc', 'xyz', {
      expiration: expiresAt,
    });

    // Store JSON object
    const userData = { id: 123, name: 'John', email: 'john@example.com' };
    await env.CACHE.put('user:123', JSON.stringify(userData));

    return new Response('Stored successfully');
  },
};
```

### Read (Get)

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    // Get string value
    const value = await env.CACHE.get('key');

    if (!value) {
      return new Response('Not found', { status: 404 });
    }

    // Get as JSON
    const userData = await env.CACHE.get('user:123', 'json');

    // Get as ArrayBuffer (for binary data)
    const imageData = await env.CACHE.get('image:logo', 'arrayBuffer');

    // Get as stream (for large values)
    const stream = await env.CACHE.get('large-file', 'stream');

    // Get with metadata
    const { value, metadata } = await env.CACHE.getWithMetadata('key');

    return Response.json({ value, userData });
  },
};
```

### Delete

```typescript
// Delete a key
await env.CACHE.delete('key');

// Delete returns void, always succeeds (even if key doesn't exist)
await env.CACHE.delete('session:123');
```

### List Keys

```typescript
// List all keys
const list = await env.CACHE.list();

// List with prefix
const userKeys = await env.CACHE.list({ prefix: 'user:' });

// Paginated listing
const firstPage = await env.CACHE.list({ limit: 100 });
const secondPage = await env.CACHE.list({
  limit: 100,
  cursor: firstPage.cursor,
});

// List keys
for (const key of list.keys) {
  console.log(key.name, key.expiration, key.metadata);
}
```

## Advanced Features

### Metadata

Store additional information about keys:

```typescript
// Store with metadata
await env.CACHE.put('user:123', userData, {
  metadata: {
    createdAt: Date.now(),
    version: '1.0',
    tags: ['premium', 'verified'],
  },
});

// Retrieve with metadata
const { value, metadata } = await env.CACHE.getWithMetadata('user:123', 'json');

console.log(metadata.createdAt);
console.log(metadata.tags);
```

### Bulk Operations

```typescript
// Write multiple keys efficiently
async function bulkWrite(data: Record<string, string>, env: Env) {
  await Promise.all(
    Object.entries(data).map(([key, value]) =>
      env.CACHE.put(key, value)
    )
  );
}

// Read multiple keys
async function bulkRead(keys: string[], env: Env) {
  const values = await Promise.all(
    keys.map(key => env.CACHE.get(key))
  );

  return Object.fromEntries(
    keys.map((key, i) => [key, values[i]])
  );
}
```

## Common Use Cases

### 1. Session Management

```typescript
interface Session {
  userId: string;
  email: string;
  createdAt: number;
}

// Create session
async function createSession(userId: string, email: string, env: Env): Promise<string> {
  const sessionId = crypto.randomUUID();
  const session: Session = {
    userId,
    email,
    createdAt: Date.now(),
  };

  // Store session for 24 hours
  await env.SESSIONS.put(`session:${sessionId}`, JSON.stringify(session), {
    expirationTtl: 86400, // 24 hours
  });

  return sessionId;
}

// Validate session
async function validateSession(sessionId: string, env: Env): Promise<Session | null> {
  const session = await env.SESSIONS.get(`session:${sessionId}`, 'json') as Session | null;

  if (!session) return null;

  // Extend session on each request
  await env.SESSIONS.put(`session:${sessionId}`, JSON.stringify(session), {
    expirationTtl: 86400,
  });

  return session;
}

// Logout (delete session)
async function logout(sessionId: string, env: Env) {
  await env.SESSIONS.delete(`session:${sessionId}`);
}
```

### 2. Rate Limiting

```typescript
async function checkRateLimit(ip: string, env: Env): Promise<boolean> {
  const key = `ratelimit:${ip}`;
  const current = await env.CACHE.get(key);

  if (!current) {
    // First request - allow and set counter
    await env.CACHE.put(key, '1', { expirationTtl: 60 }); // 1 minute window
    return true;
  }

  const count = parseInt(current);

  if (count >= 100) {
    // Rate limit exceeded (100 requests per minute)
    return false;
  }

  // Increment counter
  await env.CACHE.put(key, (count + 1).toString(), { expirationTtl: 60 });
  return true;
}

// Usage in Worker
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const ip = request.headers.get('cf-connecting-ip') || 'unknown';

    const allowed = await checkRateLimit(ip, env);

    if (!allowed) {
      return Response.json(
        { error: 'Rate limit exceeded' },
        { status: 429 }
      );
    }

    // Handle request normally
    return Response.json({ success: true });
  },
};
```

### 3. Feature Flags

```typescript
interface FeatureFlags {
  newDashboard: boolean;
  darkMode: boolean;
  betaFeatures: boolean;
}

async function getFeatureFlags(userId: string, env: Env): Promise<FeatureFlags> {
  // Try user-specific flags first
  const userFlags = await env.CACHE.get(`flags:user:${userId}`, 'json') as FeatureFlags | null;

  if (userFlags) return userFlags;

  // Fallback to default flags
  const defaultFlags = await env.CACHE.get('flags:default', 'json') as FeatureFlags | null;

  return defaultFlags || {
    newDashboard: false,
    darkMode: true,
    betaFeatures: false,
  };
}

async function setFeatureFlags(flags: FeatureFlags, env: Env) {
  await env.CACHE.put('flags:default', JSON.stringify(flags));
}

async function setUserFeatureFlags(userId: string, flags: Partial<FeatureFlags>, env: Env) {
  const currentFlags = await getFeatureFlags(userId, env);
  const newFlags = { ...currentFlags, ...flags };

  await env.CACHE.put(`flags:user:${userId}`, JSON.stringify(newFlags));
}
```

### 4. Caching Database Queries

```typescript
interface Env {
  DB: D1Database;
  CACHE: KVNamespace;
}

async function getUserCached(userId: string, env: Env) {
  const cacheKey = `user:${userId}`;

  // Try cache first
  const cached = await env.CACHE.get(cacheKey, 'json');

  if (cached) {
    return cached;
  }

  // Cache miss - query database
  const user = await env.DB.prepare(
    'SELECT id, email, name, created_at FROM users WHERE id = ?'
  ).bind(userId).first();

  if (!user) return null;

  // Store in cache for 5 minutes
  await env.CACHE.put(cacheKey, JSON.stringify(user), {
    expirationTtl: 300,
  });

  return user;
}

async function updateUser(userId: string, data: any, env: Env) {
  // Update database
  await env.DB.prepare(
    'UPDATE users SET name = ? WHERE id = ?'
  ).bind(data.name, userId).run();

  // Invalidate cache
  await env.CACHE.delete(`user:${userId}`);
}
```

### 5. API Key Storage

```typescript
interface APIKey {
  userId: string;
  permissions: string[];
  createdAt: number;
  lastUsed: number;
}

async function createAPIKey(userId: string, permissions: string[], env: Env): Promise<string> {
  const apiKey = `sk_${crypto.randomUUID().replace(/-/g, '')}`;
  const keyData: APIKey = {
    userId,
    permissions,
    createdAt: Date.now(),
    lastUsed: Date.now(),
  };

  await env.CACHE.put(`apikey:${apiKey}`, JSON.stringify(keyData));

  // Store user's API keys list
  const userKeys = await env.CACHE.get(`user:${userId}:apikeys`, 'json') as string[] || [];
  userKeys.push(apiKey);
  await env.CACHE.put(`user:${userId}:apikeys`, JSON.stringify(userKeys));

  return apiKey;
}

async function validateAPIKey(apiKey: string, env: Env): Promise<APIKey | null> {
  const keyData = await env.CACHE.get(`apikey:${apiKey}`, 'json') as APIKey | null;

  if (!keyData) return null;

  // Update last used time
  keyData.lastUsed = Date.now();
  await env.CACHE.put(`apikey:${apiKey}`, JSON.stringify(keyData));

  return keyData;
}

async function revokeAPIKey(apiKey: string, env: Env) {
  await env.CACHE.delete(`apikey:${apiKey}`);
}

// Usage in Worker
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const apiKey = request.headers.get('x-api-key');

    if (!apiKey) {
      return Response.json({ error: 'API key required' }, { status: 401 });
    }

    const keyData = await validateAPIKey(apiKey, env);

    if (!keyData) {
      return Response.json({ error: 'Invalid API key' }, { status: 401 });
    }

    // Check permissions
    if (!keyData.permissions.includes('read')) {
      return Response.json({ error: 'Insufficient permissions' }, { status: 403 });
    }

    // Handle request with authenticated user
    return Response.json({ userId: keyData.userId });
  },
};
```

### 6. Caching External API Responses

```typescript
async function fetchWithCache(url: string, env: Env, cacheTtl: number = 300) {
  const cacheKey = `api:${url}`;

  // Try cache first
  const cached = await env.CACHE.get(cacheKey);

  if (cached) {
    return JSON.parse(cached);
  }

  // Cache miss - fetch from API
  const response = await fetch(url);
  const data = await response.json();

  // Store in cache
  await env.CACHE.put(cacheKey, JSON.stringify(data), {
    expirationTtl: cacheTtl,
  });

  return data;
}

// Usage
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    // Expensive API call cached for 10 minutes
    const data = await fetchWithCache(
      'https://api.example.com/data',
      env,
      600
    );

    return Response.json(data);
  },
};
```

### 7. Email Verification Codes

```typescript
async function generateVerificationCode(email: string, env: Env): Promise<string> {
  const code = Math.random().toString(36).substring(2, 8).toUpperCase();

  await env.CACHE.put(`verify:${email}`, code, {
    expirationTtl: 900, // 15 minutes
  });

  // Send email with code (implementation not shown)
  await sendEmail(email, `Your verification code is: ${code}`);

  return code;
}

async function verifyCode(email: string, code: string, env: Env): Promise<boolean> {
  const storedCode = await env.CACHE.get(`verify:${email}`);

  if (!storedCode || storedCode !== code) {
    return false;
  }

  // Delete code after successful verification
  await env.CACHE.delete(`verify:${email}`);

  return true;
}
```

### 8. Shopping Cart Storage

```typescript
interface CartItem {
  productId: string;
  quantity: number;
  price: number;
}

interface Cart {
  items: CartItem[];
  total: number;
  updatedAt: number;
}

async function addToCart(sessionId: string, item: CartItem, env: Env) {
  const cartKey = `cart:${sessionId}`;
  const cart = await env.CACHE.get(cartKey, 'json') as Cart | null;

  const items = cart?.items || [];
  const existingItem = items.find(i => i.productId === item.productId);

  if (existingItem) {
    existingItem.quantity += item.quantity;
  } else {
    items.push(item);
  }

  const total = items.reduce((sum, i) => sum + (i.price * i.quantity), 0);

  const newCart: Cart = {
    items,
    total,
    updatedAt: Date.now(),
  };

  // Store cart for 7 days
  await env.CACHE.put(cartKey, JSON.stringify(newCart), {
    expirationTtl: 604800,
  });

  return newCart;
}

async function getCart(sessionId: string, env: Env): Promise<Cart | null> {
  return await env.CACHE.get(`cart:${sessionId}`, 'json') as Cart | null;
}

async function clearCart(sessionId: string, env: Env) {
  await env.CACHE.delete(`cart:${sessionId}`);
}
```

## CLI Management

### Working with KV from Command Line

```bash
# Create namespace
wrangler kv:namespace create "MY_KV"

# List namespaces
wrangler kv:namespace list

# Delete namespace
wrangler kv:namespace delete --namespace-id="xxx"

# Put key
wrangler kv:key put "key" "value" --namespace-id="xxx"

# Get key
wrangler kv:key get "key" --namespace-id="xxx"

# Delete key
wrangler kv:key delete "key" --namespace-id="xxx"

# List keys
wrangler kv:key list --namespace-id="xxx"

# Bulk upload from JSON file
wrangler kv:bulk put data.json --namespace-id="xxx"
```

### Bulk Upload Example

```json
// data.json
[
  { "key": "user:1", "value": "{\"name\":\"John\",\"email\":\"john@example.com\"}" },
  { "key": "user:2", "value": "{\"name\":\"Jane\",\"email\":\"jane@example.com\"}" },
  { "key": "config:theme", "value": "dark" }
]
```

```bash
wrangler kv:bulk put data.json --namespace-id="xxx"
```

## Using with Pages Functions

```typescript
// functions/api/session.ts

interface Env {
  SESSIONS: KVNamespace;
}

export const onRequestPost: PagesFunction<Env> = async (context) => {
  const { email, password } = await context.request.json();

  // Validate credentials (implementation not shown)
  const userId = await validateCredentials(email, password);

  if (!userId) {
    return Response.json({ error: 'Invalid credentials' }, { status: 401 });
  }

  // Create session
  const sessionId = crypto.randomUUID();
  await context.env.SESSIONS.put(
    `session:${sessionId}`,
    JSON.stringify({ userId, email }),
    { expirationTtl: 86400 }
  );

  return Response.json({ sessionId });
};

export const onRequestGet: PagesFunction<Env> = async (context) => {
  const sessionId = context.request.headers.get('x-session-id');

  if (!sessionId) {
    return Response.json({ error: 'No session' }, { status: 401 });
  }

  const session = await context.env.SESSIONS.get(`session:${sessionId}`, 'json');

  if (!session) {
    return Response.json({ error: 'Invalid session' }, { status: 401 });
  }

  return Response.json(session);
};
```

## Ensuring It Works

### Testing Checklist

1. **Local Testing**:
   ```bash
   # Start dev server
   wrangler dev --local

   # Test KV operations
   curl http://localhost:8787/api/set
   curl http://localhost:8787/api/get
   ```

2. **Verify in Dashboard**:
   - Go to Workers & Pages > KV
   - Select your namespace
   - View keys and values
   - Manually add/edit/delete keys for testing

3. **CLI Testing**:
   ```bash
   # Write test key
   wrangler kv:key put "test" "hello" --namespace-id="xxx"

   # Read it back
   wrangler kv:key get "test" --namespace-id="xxx"

   # List keys
   wrangler kv:key list --namespace-id="xxx"
   ```

4. **Production Testing**:
   ```bash
   wrangler deploy
   curl https://your-worker.workers.dev/api/test
   ```

### Common Issues & Solutions

**KV namespace not found:**
- Verify `id` in `wrangler.toml` matches actual namespace
- Check binding name matches code
- Run `wrangler kv:namespace list` to verify

**Values not updating:**
- Remember KV is eventually consistent
- Changes propagate within 60 seconds globally
- Use cache headers if serving to browsers

**Hitting limits:**
- Check daily operation limits in dashboard
- Consider upgrading to paid plan
- Implement caching to reduce operations

## Best Practices

### 1. Use Appropriate TTLs

```typescript
// Short TTL for frequently changing data
await env.KV.put('user:online', 'true', { expirationTtl: 60 }); // 1 minute

// Medium TTL for semi-static data
await env.KV.put('api:response', data, { expirationTtl: 300 }); // 5 minutes

// Long TTL for rarely changing data
await env.KV.put('config:settings', data, { expirationTtl: 86400 }); // 24 hours
```

### 2. Use Prefixes for Organization

```typescript
// Organize keys by type
await env.KV.put('user:123', userData);
await env.KV.put('session:abc', sessionData);
await env.KV.put('cache:query:xyz', queryResult);
await env.KV.put('config:feature-flags', flags);

// Easy to list by type
const sessions = await env.KV.list({ prefix: 'session:' });
```

### 3. Handle Missing Keys Gracefully

```typescript
// Always check for null
const value = await env.KV.get('key');

if (!value) {
  // Handle missing key
  return Response.json({ error: 'Not found' }, { status: 404 });
}
```

### 4. Don't Use KV for High-Write Scenarios

KV is optimized for reads, not writes. For high-write use cases:
- Use D1 database instead
- Use Durable Objects for coordination
- Batch writes when possible

### 5. Consider Consistency Model

```typescript
// KV is eventually consistent
await env.KV.put('key', 'value1');

// Immediate read might return old value
const value = await env.KV.get('key'); // Might be null or old value

// For strong consistency, use D1 instead
```

## Efficient Usage Tips

### 1. Combine with D1 for Best Performance

```typescript
// Use KV for hot data, D1 for cold data
async function getUser(userId: string, env: Env) {
  // Try KV cache first (hot data)
  let user = await env.CACHE.get(`user:${userId}`, 'json');

  if (!user) {
    // Miss - get from D1 (cold data)
    user = await env.DB.prepare(
      'SELECT * FROM users WHERE id = ?'
    ).bind(userId).first();

    // Warm the cache
    if (user) {
      await env.CACHE.put(`user:${userId}`, JSON.stringify(user), {
        expirationTtl: 300,
      });
    }
  }

  return user;
}
```

### 2. Use Metadata for Filtering

```typescript
// Store with metadata
await env.KV.put('item:1', data, {
  metadata: {
    category: 'electronics',
    price: 999,
    featured: true,
  },
});

// List and filter by metadata
const list = await env.KV.list({ prefix: 'item:' });
const featured = list.keys.filter(k => k.metadata?.featured === true);
```

### 3. Implement Stale-While-Revalidate

```typescript
async function getWithSWR(key: string, fetcher: () => Promise<any>, env: Env) {
  const cached = await env.KV.getWithMetadata(key, 'json');

  if (cached.value) {
    const age = Date.now() - (cached.metadata?.cachedAt || 0);

    // Return cached if fresh (< 5 minutes)
    if (age < 300000) {
      return cached.value;
    }

    // Revalidate in background if stale (5-10 minutes)
    if (age < 600000) {
      // Return stale data immediately
      env.waitUntil(
        fetcher().then(fresh =>
          env.KV.put(key, JSON.stringify(fresh), {
            metadata: { cachedAt: Date.now() },
          })
        )
      );
      return cached.value;
    }
  }

  // Fetch fresh data if very stale or missing
  const fresh = await fetcher();
  await env.KV.put(key, JSON.stringify(fresh), {
    metadata: { cachedAt: Date.now() },
  });
  return fresh;
}
```

## Official Resources

- **Documentation**: https://developers.cloudflare.com/kv/
- **API Reference**: https://developers.cloudflare.com/kv/api/
- **Pricing**: https://developers.cloudflare.com/kv/platform/pricing/
- **Best Practices**: https://developers.cloudflare.com/kv/learning/kv-best-practices/
- **Limits**: https://developers.cloudflare.com/kv/platform/limits/
- **Discord Community**: https://discord.cloudflare.com

## Why KV is Essential for Edge Apps

1. **Lightning fast reads** - Sub-millisecond access
2. **Global distribution** - Data everywhere your users are
3. **Simple API** - Easy to use key-value interface
4. **Generous free tier** - 100k reads/day free
5. **Perfect for caching** - Reduce database load dramatically
6. **Session storage** - Ideal for authentication
7. **Feature flags** - Instant configuration updates
8. **Rate limiting** - Protect your APIs

KV is the perfect complement to D1 and Workers, providing a high-performance caching layer that dramatically reduces latency and database load. Use KV for hot data and caching, D1 for relational data, R2 for files, and you have a complete edge-native stack!
