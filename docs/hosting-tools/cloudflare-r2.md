# Cloudflare R2 Storage

## Overview

Cloudflare R2 (Ridiculously Resilient) Storage is an S3-compatible object storage service designed to store large amounts of unstructured data like images, videos, audio files, documents, and backups. The key differentiator: **zero egress fees**.

## Key Benefits

### Cost-Effective Storage
- **10 GB free storage** on free tier
- **No egress fees** (unlike AWS S3 which charges for downloads)
- **No API request fees** on free tier
- Pay only for storage and operations at scale

### S3-Compatible
- **Drop-in replacement** for AWS S3
- Use existing S3 libraries and tools
- **Seamless migration** from S3
- Standard S3 API compatibility

### Fast & Reliable
- **Global distribution** via Cloudflare's network
- **Automatic caching** when used with Workers/Pages
- **High availability** with automatic replication
- **Low latency** access worldwide

### Perfect Use Cases
- **Image/video hosting** for web applications
- **User-generated content** storage
- **Static asset hosting** (CSS, JS, fonts)
- **Backup storage** for databases and files
- **Media libraries** for content platforms
- **File upload/download** features in SaaS apps

## Pricing

### Free Tier
- **10 GB storage** included
- **1 million Class A operations** per month (writes, lists)
- **10 million Class B operations** per month (reads)
- **No egress charges** ever!

### Paid Pricing (when you exceed free tier)
- **Storage**: $0.015 per GB/month (~$15 per TB)
- **Class A operations**: $4.50 per million (writes)
- **Class B operations**: $0.36 per million (reads)
- **Egress**: $0 (FREE!) 🎉

### Cost Comparison

**Example**: Serving 100 GB of images with 1 TB downloads/month

| Service | Storage | Egress | Total |
|---------|---------|--------|-------|
| AWS S3 | $2.30 | $92.00 | **$94.30** |
| Google Cloud Storage | $2.00 | $120.00 | **$122.00** |
| Cloudflare R2 | $1.50 | $0.00 | **$1.50** |

**R2 is 60-80x cheaper** for content delivery!

## Getting Started

### Prerequisites
- Cloudflare account
- Wrangler CLI installed (`npm install -g wrangler`)
- Basic understanding of object storage

### Creating an R2 Bucket

#### Via Wrangler CLI

```bash
# Create a new bucket
wrangler r2 bucket create my-images

# List all buckets
wrangler r2 bucket list

# Delete a bucket (when empty)
wrangler r2 bucket delete my-bucket-name
```

#### Via Cloudflare Dashboard

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Select **R2** from left sidebar
3. Click **Create bucket**
4. Enter bucket name (e.g., `my-app-storage`)
5. Choose location (optional)
6. Click **Create bucket**

### Bucket Configuration

```bash
# Set CORS policy (if needed for direct browser uploads)
wrangler r2 bucket cors put my-images --config cors.json
```

Example CORS configuration:
```json
{
  "cors_rules": [
    {
      "allowed_origins": ["https://yourdomain.com"],
      "allowed_methods": ["GET", "PUT", "POST", "DELETE"],
      "allowed_headers": ["*"],
      "max_age_seconds": 3600
    }
  ]
}
```

## Using R2 with Workers

### Binding R2 to a Worker

In `wrangler.toml`:
```toml
name = "my-worker"
main = "src/index.ts"

[[r2_buckets]]
binding = "STORAGE"
bucket_name = "my-images"
```

### Basic Upload Example

```typescript
interface Env {
  STORAGE: R2Bucket;
}

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    // Upload file
    if (url.pathname === '/upload' && request.method === 'POST') {
      const formData = await request.formData();
      const file = formData.get('file') as File;

      if (!file) {
        return Response.json({ error: 'No file provided' }, { status: 400 });
      }

      // Generate unique filename
      const filename = `${Date.now()}-${file.name}`;

      // Upload to R2
      await env.STORAGE.put(filename, file.stream(), {
        httpMetadata: {
          contentType: file.type,
        },
      });

      return Response.json({
        success: true,
        url: `/files/${filename}`,
        filename,
      });
    }

    // Download file
    if (url.pathname.startsWith('/files/')) {
      const filename = url.pathname.slice(7);

      const object = await env.STORAGE.get(filename);

      if (!object) {
        return new Response('File not found', { status: 404 });
      }

      const headers = new Headers();
      object.writeHttpMetadata(headers);
      headers.set('etag', object.httpEtag);

      return new Response(object.body, { headers });
    }

    return new Response('Not found', { status: 404 });
  },
};
```

### Image Upload with Validation

```typescript
const ALLOWED_TYPES = ['image/jpeg', 'image/png', 'image/gif', 'image/webp'];
const MAX_SIZE = 5 * 1024 * 1024; // 5MB

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    if (request.method !== 'POST') {
      return Response.json({ error: 'Method not allowed' }, { status: 405 });
    }

    const formData = await request.formData();
    const file = formData.get('image') as File;

    // Validate file
    if (!file) {
      return Response.json({ error: 'No file provided' }, { status: 400 });
    }

    if (!ALLOWED_TYPES.includes(file.type)) {
      return Response.json({ error: 'Invalid file type' }, { status: 400 });
    }

    if (file.size > MAX_SIZE) {
      return Response.json({ error: 'File too large' }, { status: 400 });
    }

    // Generate filename with UUID
    const extension = file.name.split('.').pop();
    const filename = `${crypto.randomUUID()}.${extension}`;
    const key = `images/${filename}`;

    // Upload to R2
    await env.STORAGE.put(key, file.stream(), {
      httpMetadata: {
        contentType: file.type,
      },
      customMetadata: {
        originalName: file.name,
        uploadedAt: new Date().toISOString(),
      },
    });

    return Response.json({
      success: true,
      url: `https://your-worker.workers.dev/files/${key}`,
      filename,
    });
  },
};
```

### Listing Files

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    if (url.pathname === '/api/files') {
      // List all objects
      const listed = await env.STORAGE.list({
        limit: 100,
        prefix: 'images/', // Optional: filter by prefix
      });

      const files = listed.objects.map(obj => ({
        key: obj.key,
        size: obj.size,
        uploaded: obj.uploaded,
      }));

      return Response.json({
        files,
        truncated: listed.truncated,
        cursor: listed.cursor,
      });
    }

    return new Response('Not found', { status: 404 });
  },
};
```

### Deleting Files

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);

    if (url.pathname === '/api/delete' && request.method === 'DELETE') {
      const { filename } = await request.json();

      // Delete from R2
      await env.STORAGE.delete(filename);

      return Response.json({ success: true });
    }

    return new Response('Not found', { status: 404 });
  },
};
```

## Advanced Features

### Multipart Uploads (Large Files)

For files larger than 5MB, use multipart uploads:

```typescript
async function uploadLargeFile(file: File, env: Env) {
  const filename = `large-files/${crypto.randomUUID()}-${file.name}`;

  // Create multipart upload
  const multipart = await env.STORAGE.createMultipartUpload(filename);

  const CHUNK_SIZE = 5 * 1024 * 1024; // 5MB chunks
  const chunks: R2UploadedPart[] = [];

  let offset = 0;
  let partNumber = 1;

  // Upload in chunks
  while (offset < file.size) {
    const chunk = file.slice(offset, offset + CHUNK_SIZE);
    const buffer = await chunk.arrayBuffer();

    const part = await multipart.uploadPart(partNumber, buffer);
    chunks.push(part);

    offset += CHUNK_SIZE;
    partNumber++;
  }

  // Complete the upload
  const object = await multipart.complete(chunks);

  return {
    success: true,
    key: filename,
    size: object.size,
  };
}
```

### Conditional Requests (Caching)

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);
    const filename = url.pathname.slice(1);

    const object = await env.STORAGE.get(filename);

    if (!object) {
      return new Response('Not found', { status: 404 });
    }

    // Check if client has cached version
    const ifNoneMatch = request.headers.get('If-None-Match');
    if (ifNoneMatch === object.httpEtag) {
      return new Response(null, { status: 304 }); // Not Modified
    }

    const headers = new Headers();
    object.writeHttpMetadata(headers);
    headers.set('etag', object.httpEtag);
    headers.set('cache-control', 'public, max-age=31536000'); // 1 year

    return new Response(object.body, { headers });
  },
};
```

### Custom Metadata

```typescript
// Store metadata with files
await env.STORAGE.put('user-123/profile.jpg', file.stream(), {
  httpMetadata: {
    contentType: 'image/jpeg',
  },
  customMetadata: {
    userId: '123',
    uploadedBy: 'john@example.com',
    category: 'profile-pictures',
    originalName: file.name,
  },
});

// Retrieve metadata
const object = await env.STORAGE.head('user-123/profile.jpg');
console.log(object.customMetadata);
```

## Using R2 with Pages Functions

```typescript
// functions/upload.ts

interface Env {
  STORAGE: R2Bucket;
}

export const onRequestPost: PagesFunction<Env> = async (context) => {
  const formData = await context.request.formData();
  const file = formData.get('file') as File;

  if (!file) {
    return Response.json({ error: 'No file' }, { status: 400 });
  }

  const filename = `${Date.now()}-${file.name}`;

  await context.env.STORAGE.put(filename, file.stream(), {
    httpMetadata: { contentType: file.type },
  });

  return Response.json({ success: true, filename });
};
```

## Public Bucket Access

### Custom Domain for Public Files

1. Create bucket: `my-public-assets`
2. Add custom domain in R2 dashboard
3. Configure DNS (automatic if domain on Cloudflare)
4. Files accessible at: `https://cdn.yourdomain.com/filename.jpg`

### Worker as CDN

Use a Worker to serve R2 files with custom logic:

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);
    const key = url.pathname.slice(1);

    // Add security checks, analytics, etc.
    const object = await env.STORAGE.get(key);

    if (!object) {
      return new Response('Not found', { status: 404 });
    }

    const headers = new Headers();
    object.writeHttpMetadata(headers);

    // Add custom headers
    headers.set('Cache-Control', 'public, max-age=86400');
    headers.set('CDN-Cache-Control', 'public, max-age=31536000');

    return new Response(object.body, { headers });
  },
};
```

## S3 API Compatibility

R2 supports S3 API, so you can use AWS SDK:

### Setup S3 Client

```bash
npm install @aws-sdk/client-s3
```

```typescript
import { S3Client, PutObjectCommand } from '@aws-sdk/client-s3';

const S3 = new S3Client({
  region: 'auto',
  endpoint: `https://${accountId}.r2.cloudflarestorage.com`,
  credentials: {
    accessKeyId: 'your-access-key-id',
    secretAccessKey: 'your-secret-access-key',
  },
});

// Upload file
await S3.send(new PutObjectCommand({
  Bucket: 'my-bucket',
  Key: 'test.jpg',
  Body: fileBuffer,
  ContentType: 'image/jpeg',
}));
```

### Generate Access Keys

1. Go to R2 dashboard
2. Click **Manage R2 API Tokens**
3. Create API token
4. Save Access Key ID and Secret Access Key

## Ensuring It Works

### Testing Checklist

1. **Test Upload**:
   ```bash
   curl -X POST https://your-worker.workers.dev/upload \
     -F "file=@test-image.jpg"
   ```

2. **Test Download**:
   ```bash
   curl https://your-worker.workers.dev/files/test-image.jpg \
     --output downloaded.jpg
   ```

3. **Verify in Dashboard**:
   - Go to R2 bucket in Cloudflare dashboard
   - Check file is listed
   - Verify size and metadata

4. **Test Delete**:
   ```bash
   curl -X DELETE https://your-worker.workers.dev/api/delete \
     -H "Content-Type: application/json" \
     -d '{"filename": "test-image.jpg"}'
   ```

### Common Issues & Solutions

**Upload fails silently:**
- Check bucket name in `wrangler.toml`
- Verify binding name matches code
- Check file size limits

**CORS errors in browser:**
- Configure CORS policy on bucket
- Add appropriate `Access-Control-Allow-*` headers

**Files not accessible:**
- Check if bucket is public or requires Worker
- Verify custom domain configuration
- Check firewall/security settings

## Efficient Usage Tips

### 1. Use Folders/Prefixes

```typescript
// Organize files logically
await env.STORAGE.put('users/123/avatar.jpg', file);
await env.STORAGE.put('products/456/image-1.jpg', file);
await env.STORAGE.put('documents/2024/report.pdf', file);

// Easy to list by category
const userFiles = await env.STORAGE.list({ prefix: 'users/123/' });
```

### 2. Implement Caching

```typescript
// Add cache headers for static assets
headers.set('Cache-Control', 'public, max-age=31536000, immutable');
headers.set('CDN-Cache-Control', 'public, max-age=31536000');
```

### 3. Optimize Images on Upload

```typescript
// Use Workers to resize/optimize images
import { Image } from '@cloudflare/workers-image';

const image = await Image.load(await file.arrayBuffer());
const optimized = await image
  .resize(1200) // Max width
  .quality(85)
  .toBuffer('jpeg');

await env.STORAGE.put(filename, optimized);
```

### 4. Store Metadata in D1

```typescript
// Store file metadata in database for fast queries
await env.DB.prepare(`
  INSERT INTO files (key, size, type, uploaded_by, created_at)
  VALUES (?, ?, ?, ?, ?)
`).bind(filename, file.size, file.type, userId, Date.now()).run();

// Query files without listing R2
const files = await env.DB.prepare(`
  SELECT * FROM files WHERE uploaded_by = ? ORDER BY created_at DESC
`).bind(userId).all();
```

### 5. Implement Signed URLs

```typescript
// Generate temporary access URLs
function generateSignedUrl(key: string, expiresIn: number): string {
  const expires = Date.now() + expiresIn;
  const signature = await crypto.subtle.sign(
    'HMAC',
    await getSigningKey(),
    new TextEncoder().encode(`${key}:${expires}`)
  );

  return `/files/${key}?expires=${expires}&sig=${btoa(String.fromCharCode(...new Uint8Array(signature)))}`;
}
```

## Real-World Use Cases

### 1. User Avatar Storage

```typescript
async function uploadAvatar(file: File, userId: string, env: Env) {
  const key = `avatars/${userId}.jpg`;

  await env.STORAGE.put(key, file.stream(), {
    httpMetadata: { contentType: 'image/jpeg' },
    customMetadata: { userId, uploadedAt: new Date().toISOString() },
  });

  await env.DB.prepare(
    'UPDATE users SET avatar_url = ? WHERE id = ?'
  ).bind(`/avatars/${userId}.jpg`, userId).run();

  return { success: true, url: `/avatars/${userId}.jpg` };
}
```

### 2. Document Management System

```typescript
async function uploadDocument(file: File, folder: string, env: Env) {
  const filename = `${crypto.randomUUID()}.${file.name.split('.').pop()}`;
  const key = `documents/${folder}/${filename}`;

  await env.STORAGE.put(key, file.stream(), {
    httpMetadata: { contentType: file.type },
    customMetadata: {
      originalName: file.name,
      folder,
      uploadedAt: new Date().toISOString(),
    },
  });

  return { key, url: `/files/${key}` };
}
```

### 3. Video Platform Storage

```typescript
async function uploadVideo(file: File, env: Env) {
  // Use multipart upload for large videos
  const key = `videos/${crypto.randomUUID()}.mp4`;

  const multipart = await env.STORAGE.createMultipartUpload(key);

  // Upload in chunks (implementation from multipart example above)
  // ...

  return { key, url: `/videos/${key}` };
}
```

## Integration with Other Services

### With Workers
- Serve files through custom CDN logic
- Add authentication/authorization
- Implement usage tracking

### With Pages
- Store user uploads from frontend
- Serve static assets
- Handle form submissions with file uploads

### With D1
- Store file metadata for querying
- Track file usage and analytics
- Implement file permissions

### With KV
- Cache frequently accessed file metadata
- Store temporary upload tokens
- Implement rate limiting

## Official Resources

- **Documentation**: https://developers.cloudflare.com/r2/
- **API Reference**: https://developers.cloudflare.com/r2/api/
- **Pricing**: https://developers.cloudflare.com/r2/pricing/
- **Examples**: https://developers.cloudflare.com/r2/examples/
- **Discord Community**: https://discord.cloudflare.com

## Why R2 is Perfect for Modern Apps

1. **No egress fees** - Save 90% on bandwidth costs
2. **S3-compatible** - Easy migration from AWS
3. **Fast globally** - Cloudflare's network
4. **Generous free tier** - 10GB free
5. **Worker integration** - Custom logic at the edge
6. **Simple pricing** - No surprise bills
7. **Reliable storage** - Enterprise-grade infrastructure

For any application that needs to store and serve files - images, videos, documents, backups - Cloudflare R2 offers unbeatable value and performance.
