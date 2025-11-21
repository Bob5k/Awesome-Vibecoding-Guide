# Cloudflare CLI (Wrangler) Cheat Sheet

Quick reference for Wrangler commands and Cloudflare development workflows.

## Installation

```bash
# Install globally
npm install -g wrangler

# Or use with npx (no install needed)
npx wrangler [command]

# Check version
wrangler --version

# Update wrangler
npm update -g wrangler
```

## Authentication

```bash
# Login to Cloudflare
wrangler login

# Logout
wrangler logout

# Check who's logged in
wrangler whoami

# Use API token instead of OAuth
export CLOUDFLARE_API_TOKEN=your_token_here
```

## Cloudflare Pages

### Development

```bash
# Local development server
npm run dev
# Or
wrangler pages dev ./dist

# Dev with specific port
wrangler pages dev ./dist --port 3000

# Dev with live reload
wrangler pages dev ./dist --live-reload

# Dev with specific binding
wrangler pages dev ./dist --binding KEY=value
```

### Deployment

```bash
# Deploy to Cloudflare Pages
npm run build && wrangler pages deploy ./dist

# Deploy to specific project
wrangler pages deploy ./dist --project-name=my-site

# Deploy to specific branch
wrangler pages deploy ./dist --branch=staging

# Deploy with commit message
wrangler pages deploy ./dist --commit-message="Deploy v1.2.0"
```

### Project Management

```bash
# Create new Pages project
wrangler pages project create my-site

# List all projects
wrangler pages project list

# View project details
wrangler pages project get my-site

# Delete project (careful!)
wrangler pages project delete my-site
```

### Deployment Management

```bash
# List deployments
wrangler pages deployment list --project-name=my-site

# View deployment details
wrangler pages deployment get <deployment-id>

# Tail deployment logs
wrangler pages deployment tail
```

## Cloudflare Workers

### Development

```bash
# Initialize new Worker
wrangler init my-worker

# Start local dev server
wrangler dev

# Dev with remote resources (D1, KV, etc.)
wrangler dev --remote

# Dev with specific port
wrangler dev --port 8787

# Dev with local mode (faster, but no remote resources)
wrangler dev --local
```

### Deployment

```bash
# Deploy Worker
wrangler deploy

# Deploy to specific environment
wrangler deploy --env production

# Deploy with name
wrangler deploy --name my-worker

# Publish (alias for deploy)
wrangler publish
```

### Worker Management

```bash
# List Workers
wrangler list

# Delete Worker
wrangler delete my-worker

# View Worker details
wrangler status

# Tail Worker logs
wrangler tail

# Tail specific Worker
wrangler tail my-worker
```

## D1 Database

### Database Management

```bash
# Create database
wrangler d1 create my-database

# List databases
wrangler d1 list

# Delete database
wrangler d1 delete my-database

# Get database info
wrangler d1 info my-database
```

### Run SQL Commands

```bash
# Execute SQL command
wrangler d1 execute my-database --command="SELECT * FROM users"

# Execute SQL file
wrangler d1 execute my-database --file=schema.sql

# Execute with remote database
wrangler d1 execute my-database --remote --command="SELECT * FROM users"

# Execute with local database
wrangler d1 execute my-database --local --command="SELECT * FROM users"
```

### Migrations

```bash
# Create migration
wrangler d1 migrations create my-database create_users_table

# List migrations
wrangler d1 migrations list my-database

# Apply migrations (local)
wrangler d1 migrations apply my-database --local

# Apply migrations (remote/production)
wrangler d1 migrations apply my-database --remote
```

### Example: Complete D1 Setup

```bash
# 1. Create database
wrangler d1 create my-app-db

# 2. Note the database ID, add to wrangler.toml:
# [[d1_databases]]
# binding = "DB"
# database_name = "my-app-db"
# database_id = "xxxx-xxxx-xxxx-xxxx"

# 3. Create migration
wrangler d1 migrations create my-app-db create_users

# 4. Edit migration file (migrations/0001_create_users.sql):
# CREATE TABLE users (
#   id INTEGER PRIMARY KEY AUTOINCREMENT,
#   email TEXT UNIQUE NOT NULL,
#   name TEXT NOT NULL,
#   created_at INTEGER DEFAULT (unixepoch())
# );

# 5. Apply migration locally (for testing)
wrangler d1 migrations apply my-app-db --local

# 6. Test queries locally
wrangler d1 execute my-app-db --local --command="INSERT INTO users (email, name) VALUES ('test@example.com', 'Test User')"
wrangler d1 execute my-app-db --local --command="SELECT * FROM users"

# 7. Apply migration to production
wrangler d1 migrations apply my-app-db --remote

# 8. Verify production
wrangler d1 execute my-app-db --remote --command="SELECT * FROM users"
```

## KV (Key-Value Storage)

### Namespace Management

```bash
# Create KV namespace
wrangler kv:namespace create MY_KV

# Create preview namespace (for wrangler dev)
wrangler kv:namespace create MY_KV --preview

# List namespaces
wrangler kv:namespace list

# Delete namespace
wrangler kv:namespace delete --namespace-id=xxxx
```

### Key-Value Operations

```bash
# Put key-value
wrangler kv:key put --namespace-id=xxxx "my-key" "my-value"

# Put from file
wrangler kv:key put --namespace-id=xxxx "my-key" --path=./file.txt

# Get value
wrangler kv:key get --namespace-id=xxxx "my-key"

# List keys
wrangler kv:key list --namespace-id=xxxx

# List keys with prefix
wrangler kv:key list --namespace-id=xxxx --prefix="user:"

# Delete key
wrangler kv:key delete --namespace-id=xxxx "my-key"
```

### Bulk Operations

```bash
# Bulk put (from JSON file)
# Format: [{"key": "key1", "value": "value1"}, ...]
wrangler kv:bulk put --namespace-id=xxxx ./data.json

# Bulk delete (from JSON file)
# Format: ["key1", "key2", ...]
wrangler kv:bulk delete --namespace-id=xxxx ./keys.json
```

### Example: Complete KV Setup

```bash
# 1. Create namespace
wrangler kv:namespace create MY_CACHE

# Output:
# Add the following to your wrangler.toml:
# [[kv_namespaces]]
# binding = "MY_CACHE"
# id = "xxxx"

# 2. Create preview namespace
wrangler kv:namespace create MY_CACHE --preview

# Output:
# Add to wrangler.toml:
# preview_id = "yyyy"

# 3. Add to wrangler.toml:
# [[kv_namespaces]]
# binding = "MY_CACHE"
# id = "xxxx"
# preview_id = "yyyy"

# 4. Use in code:
# export default {
#   async fetch(request, env) {
#     await env.MY_CACHE.put('key', 'value');
#     const value = await env.MY_CACHE.get('key');
#     return new Response(value);
#   }
# }
```

## R2 (Object Storage)

### Bucket Management

```bash
# Create bucket
wrangler r2 bucket create my-bucket

# List buckets
wrangler r2 bucket list

# Delete bucket
wrangler r2 bucket delete my-bucket
```

### Object Operations

```bash
# Put object
wrangler r2 object put my-bucket/path/to/file.jpg --file=./local-file.jpg

# Get object
wrangler r2 object get my-bucket/path/to/file.jpg --file=./downloaded-file.jpg

# List objects
wrangler r2 object list my-bucket

# List with prefix
wrangler r2 object list my-bucket --prefix="uploads/"

# Delete object
wrangler r2 object delete my-bucket/path/to/file.jpg
```

### Example: Complete R2 Setup

```bash
# 1. Create bucket
wrangler r2 bucket create my-app-uploads

# 2. Add to wrangler.toml:
# [[r2_buckets]]
# binding = "MY_BUCKET"
# bucket_name = "my-app-uploads"

# 3. Upload test file
wrangler r2 object put my-app-uploads/test.txt --file=./test.txt

# 4. Verify upload
wrangler r2 object list my-app-uploads

# 5. Use in code:
# export default {
#   async fetch(request, env) {
#     const object = await env.MY_BUCKET.get('test.txt');
#     return new Response(await object.text());
#   }
# }
```

## Configuration

### wrangler.toml

```toml
# Basic configuration
name = "my-worker"
main = "src/index.js"
compatibility_date = "2024-01-01"

# For Pages Functions
pages_build_output_dir = "./dist"

# Environment variables
[vars]
ENVIRONMENT = "production"
API_URL = "https://api.example.com"

# Secrets (use wrangler secret put instead)
# [secrets]
# API_KEY = "use wrangler secret put API_KEY"

# D1 Database
[[d1_databases]]
binding = "DB"
database_name = "my-database"
database_id = "xxxx-xxxx-xxxx-xxxx"

# KV Namespace
[[kv_namespaces]]
binding = "MY_KV"
id = "xxxx"
preview_id = "yyyy"

# R2 Bucket
[[r2_buckets]]
binding = "MY_BUCKET"
bucket_name = "my-bucket"

# Durable Objects
[[durable_objects.bindings]]
name = "MY_DO"
class_name = "MyDurableObject"

# Environment-specific configuration
[env.staging]
name = "my-worker-staging"
vars = { ENVIRONMENT = "staging" }

[env.production]
name = "my-worker-production"
vars = { ENVIRONMENT = "production" }
```

## Secrets Management

```bash
# Set secret (interactive)
wrangler secret put API_KEY

# Set secret from file
cat ./secret.txt | wrangler secret put API_KEY

# List secrets (names only, not values)
wrangler secret list

# Delete secret
wrangler secret delete API_KEY

# Set secret for specific environment
wrangler secret put API_KEY --env production
```

## Environment Variables

```bash
# Set in wrangler.toml:
# [vars]
# MY_VAR = "value"

# Or via command line
wrangler dev --var MY_VAR:value

# Access in code:
# env.MY_VAR
```

## Tail Logs (Real-Time Logging)

```bash
# Tail logs for current Worker
wrangler tail

# Tail specific Worker
wrangler tail my-worker

# Tail with filters
wrangler tail --status error
wrangler tail --method POST
wrangler tail --search "user-login"

# Tail with format
wrangler tail --format json
wrangler tail --format pretty

# Tail Pages Functions
wrangler pages deployment tail
```

## Common Workflows

### New Astro Site on Cloudflare Pages

```bash
# 1. Create Astro project
npm create astro@latest my-site
cd my-site

# 2. Install wrangler (optional, for local dev)
npm install -D wrangler

# 3. Build
npm run build

# 4. Test locally
npx wrangler pages dev ./dist

# 5. Deploy
npx wrangler pages deploy ./dist --project-name=my-site

# 6. Connect to Git (via Cloudflare dashboard)
# Go to dashboard, connect GitHub repo, automatic deploys on push
```

### Add D1 Database to Existing Project

```bash
# 1. Create database
wrangler d1 create my-app-db

# 2. Add binding to wrangler.toml
# [[d1_databases]]
# binding = "DB"
# database_name = "my-app-db"
# database_id = "paste-id-from-step-1"

# 3. Create schema migration
wrangler d1 migrations create my-app-db init

# 4. Edit migration file, add schema
# migrations/0001_init.sql

# 5. Apply locally for testing
wrangler d1 migrations apply my-app-db --local

# 6. Test locally
wrangler pages dev ./dist --d1 DB=my-app-db

# 7. Apply to production
wrangler d1 migrations apply my-app-db --remote

# 8. Deploy
npm run build && wrangler pages deploy ./dist
```

### Add KV Storage

```bash
# 1. Create namespace
wrangler kv:namespace create MY_CACHE

# 2. Create preview namespace
wrangler kv:namespace create MY_CACHE --preview

# 3. Add to wrangler.toml (use IDs from above)
# [[kv_namespaces]]
# binding = "MY_CACHE"
# id = "production-id"
# preview_id = "preview-id"

# 4. Test locally
wrangler pages dev ./dist

# 5. Deploy
npm run build && wrangler pages deploy ./dist
```

### Add R2 Storage

```bash
# 1. Create bucket
wrangler r2 bucket create my-uploads

# 2. Add to wrangler.toml
# [[r2_buckets]]
# binding = "UPLOADS"
# bucket_name = "my-uploads"

# 3. Test locally
wrangler pages dev ./dist

# 4. Deploy
npm run build && wrangler pages deploy ./dist
```

## Troubleshooting

### Common Issues

#### "Error: No account_id found"
```bash
# Login first
wrangler login

# Or set account ID in wrangler.toml
account_id = "your-account-id"

# Find account ID
wrangler whoami
```

#### "Error: Not authorized"
```bash
# Re-authenticate
wrangler logout
wrangler login

# Or check API token permissions
# Token needs Workers, Pages, D1, KV, R2 permissions as needed
```

#### "Error: 'wrangler' is not recognized"
```bash
# Install globally
npm install -g wrangler

# Or use npx
npx wrangler [command]

# Check PATH
echo $PATH

# Reinstall Node.js if needed
```

#### Local dev not working with D1/KV
```bash
# Use --remote flag to use production resources
wrangler pages dev ./dist --remote

# Or use --local for local D1
wrangler pages dev ./dist --local

# For D1, apply migrations locally first
wrangler d1 migrations apply my-db --local
```

#### Deploy fails with "Invalid binding"
```bash
# Check wrangler.toml syntax
# Ensure IDs are correct
# Ensure namespaces/buckets exist

# List resources
wrangler d1 list
wrangler kv:namespace list
wrangler r2 bucket list

# Recreate if needed
```

### Debug Mode

```bash
# Enable debug output
wrangler dev --debug

# Verbose output
wrangler deploy --verbose

# Show help
wrangler --help
wrangler pages --help
wrangler d1 --help
```

## Useful Aliases

Add to your shell config (`.bashrc`, `.zshrc`):

```bash
# Wrangler shortcuts
alias wd='wrangler dev'
alias wdp='wrangler pages dev ./dist'
alias wb='npm run build'
alias wbd='npm run build && wrangler pages dev ./dist'
alias wdeploy='npm run build && wrangler pages deploy ./dist'

# D1 shortcuts
alias d1list='wrangler d1 list'
alias d1exec='wrangler d1 execute'
alias d1migrate='wrangler d1 migrations apply'

# KV shortcuts
alias kvlist='wrangler kv:namespace list'
alias kvget='wrangler kv:key get'
alias kvput='wrangler kv:key put'

# R2 shortcuts
alias r2list='wrangler r2 bucket list'
alias r2objects='wrangler r2 object list'
```

## Quick Reference

### Most Common Commands

```bash
# Development
wrangler pages dev ./dist              # Local dev server
wrangler dev                            # Worker dev server
wrangler dev --remote                   # Dev with remote resources

# Deployment
wrangler pages deploy ./dist            # Deploy Pages
wrangler deploy                         # Deploy Worker

# D1 Database
wrangler d1 create my-db                # Create database
wrangler d1 migrations create my-db name  # Create migration
wrangler d1 migrations apply my-db --local  # Apply locally
wrangler d1 migrations apply my-db --remote # Apply to prod
wrangler d1 execute my-db --command="..."   # Run SQL

# KV Storage
wrangler kv:namespace create MY_KV      # Create namespace
wrangler kv:key put --namespace-id=xxx "key" "value"  # Put
wrangler kv:key get --namespace-id=xxx "key"          # Get
wrangler kv:key list --namespace-id=xxx               # List

# R2 Storage
wrangler r2 bucket create my-bucket     # Create bucket
wrangler r2 object put bucket/key --file=file  # Upload
wrangler r2 object get bucket/key --file=file  # Download
wrangler r2 object list bucket          # List

# Secrets
wrangler secret put SECRET_NAME         # Set secret
wrangler secret list                    # List secrets

# Logs
wrangler tail                           # Tail logs
wrangler pages deployment tail          # Tail Pages logs
```

---

**Pro Tips:**
- Use `wrangler dev --remote` to test with production data (carefully!)
- Always test D1 migrations locally before applying to production
- Use environment-specific configs in wrangler.toml
- Keep secrets in Wrangler secrets, not in code
- Use `wrangler tail` for real-time debugging
