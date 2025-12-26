# Setup Guide

Follow these steps to get your fullstack template up and running.

## 1. Install Bun

If you haven't already, install Bun:

```bash
curl -fsSL https://bun.sh/install | bash
```

## 2. Install Dependencies

```bash
bun run install:all
```

Or install individually:

```bash
bun install
bun --cwd client install
bun --cwd server install
```

## 3. Configure Cloudflare

### Client Configuration

Edit `client/wrangler.jsonc`:
- Update `name` to your desired Cloudflare Pages project name
- Configure any bindings or environment variables as needed

### Server Configuration

Edit `server/wrangler.jsonc`:
- Update `name` to your desired Cloudflare Worker name
- Add D1 database binding if needed:
  ```jsonc
  "d1_databases": [
    {
      "binding": "DB",
      "database_name": "my-database",
      "database_id": "your-database-id"
    }
  ]
  ```

## 4. Set Up D1 Database (Optional)

If you need a database:

1. **Create a D1 database:**
   ```bash
   cd server
   wrangler d1 create my-database
   ```

2. **Copy the database ID** from the output

3. **Update `server/wrangler.jsonc`** with the database configuration

4. **Run migrations** (if you have any):
   ```bash
   wrangler d1 migrations apply my-database --local
   ```

## 5. Configure Environment Variables

### Client Environment

Create `client/.env` if needed:
```bash
PUBLIC_API_URL=http://localhost:8787
```

For production, update with your Cloudflare Worker URL.

### Server Environment

Create `server/.env` if needed:
```bash
CLOUDFLARE_ACCOUNT_ID=your_account_id
```

## 6. Run Development Servers

### Option 1: Run both together
```bash
bun run dev
```

### Option 2: Run separately
```bash
# Terminal 1 - Client
bun run dev:client

# Terminal 2 - Server
bun run dev:server
```

- Client: http://localhost:4321
- Server: http://localhost:8787

## 7. Generate Cloudflare Types

Generate TypeScript types for Cloudflare bindings:

```bash
bun run cf-typegen
```

This will generate types in both client and server projects.

## 8. Deploy to Cloudflare

### Deploy Server (Workers)

```bash
bun run deploy:server
```

After deployment, note your Worker URL and update `client/.env` with `PUBLIC_API_URL`.

### Deploy Client (Pages)

```bash
bun run deploy:client
```

### Deploy Both

```bash
bun run deploy
```

## Troubleshooting

### Database Issues

If you get database errors:
1. Make sure you've run migrations: `wrangler d1 migrations apply <DATABASE_NAME> --local`
2. Verify your `wrangler.jsonc` has the correct database ID

### CORS Issues

If you see CORS errors, update the CORS configuration in your server code to allow your client domain.

### Port Conflicts

If ports 4321 or 8787 are in use:
- Client: Update port in `astro.config.mjs` or use `--port` flag
- Server: Update port in `wrangler.jsonc` or use `--port` flag

### Type Generation

If types aren't generating:
- Make sure you're authenticated with Cloudflare: `wrangler login`
- Check that your `wrangler.jsonc` files are valid JSONC

