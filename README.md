# Astro + Hono + Cloudflare Fullstack Template

A modern fullstack template with:
- **Client**: Astro + React (deployed on Cloudflare Pages)
- **Server**: Hono (deployed on Cloudflare Workers)
- **Package Manager**: Bun

## Project Structure

```
.
├── client/                    # Astro frontend
│   ├── src/
│   │   ├── components/       # React/Astro components
│   │   ├── layouts/          # Astro layouts
│   │   └── pages/             # Astro pages/routes
│   ├── public/               # Static assets
│   ├── astro.config.mjs      # Astro configuration
│   └── wrangler.jsonc        # Cloudflare Pages config
├── server/                    # Hono backend
│   ├── src/
│   │   └── index.ts          # Main server file
│   ├── wrangler.jsonc        # Cloudflare Workers config
│   └── package.json
├── package.json              # Root workspace configuration
└── README.md                 # This file
```

## Prerequisites

- [Bun](https://bun.sh) installed (>= 1.0.0)
- Cloudflare account
- Wrangler CLI (installed via dependencies)

## Quick Start

1. **Install dependencies:**
   ```bash
   bun run install:all
   ```

2. **Set up Cloudflare:**
   - Configure your `wrangler.jsonc` files in both `client/` and `server/`
   - Set up D1 database if needed (see server README)

3. **Start development:**
   ```bash
   bun run dev
   ```

   - Client: http://localhost:4321
   - Server: http://localhost:8787

## Scripts

| Command | Description |
|---------|-------------|
| `bun run dev` | Start both client and server |
| `bun run dev:client` | Start only the client |
| `bun run dev:server` | Start only the server |
| `bun run build` | Build both client and server |
| `bun run deploy` | Deploy both to Cloudflare |
| `bun run deploy:client` | Deploy client to Cloudflare Pages |
| `bun run deploy:server` | Deploy server to Cloudflare Workers |
| `bun run cf-typegen` | Generate Cloudflare types for both |

## Features

- ✅ **Modern Stack**: Astro 5, React 19, Hono 4
- ✅ **Type-Safe**: Full TypeScript support
- ✅ **Fast Development**: Hot reload for both client and server
- ✅ **Cloudflare Native**: Optimized for Cloudflare Pages and Workers
- ✅ **Bun Powered**: Fast package management and runtime

## Documentation

- [Client README](./client/README.md) - Client-specific setup
- [Server README](./server/README.md) - Server-specific setup

## License

MIT

