# Deployment Guide

## Dokploy with Nixpacks

This project is ready to deploy on Dokploy using Nixpacks.

### Prerequisites
- Dokploy instance running
- GitHub/GitLab repository connected to Dokploy

### Deployment Steps

1. **Create a new application** in Dokploy
2. **Select Nixpacks** as the build provider
3. **Connect your repository**
4. **Set environment variables** (optional):
   - `PORT` - Server port (default: 3000)

### Configuration Files

The project includes:
- `nixpacks.toml` - Nixpacks configuration
- `server.js` - Simple Node.js static server
- `.dockerignore` - Files to exclude from Docker build

### Build Process

Nixpacks will automatically:
1. Install Node.js 20 and pnpm
2. Run `pnpm install --frozen-lockfile`
3. Run `pnpm build` (production build)
4. Start the server with `pnpm start`

### Local Testing

```bash
# Install dependencies
pnpm install

# Development mode (watch for changes)
pnpm dev

# In another terminal, start the server
pnpm serve

# Visit http://localhost:3000
```

### Production Build

```bash
# Build for production
pnpm build

# Start production server
pnpm start
```

### Port Configuration

- **Development**: Fixed port 3000
- **Production**: Uses `PORT` environment variable (default: 3000)

The custom `server.js` ensures consistent port behavior across environments.

### Troubleshooting

**Port already in use:**
```bash
# Find and kill process on port 3000
lsof -ti:3000 | xargs kill -9
```

**Build fails:**
- Ensure `pnpm-lock.yaml` is committed
- Check Node.js version compatibility (requires Node 20+)

**Static files not found:**
- Verify `dist/` directory contains built files
- Check `server.js` DIST_DIR path
