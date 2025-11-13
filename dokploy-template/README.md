# EDData Dokploy Template

This folder contains the Dokploy template for the EDData API Platform.

## Structure

```
dokploy-template/
├── blueprints/
│   └── eddata/
│       ├── docker-compose.yml    # Service definitions
│       ├── template.toml         # Dokploy configuration
│       └── logo.svg              # Template logo
├── meta.json                     # Template metadata
└── README.md                     # This file
```

## Template Information

- **Name**: EDData API Platform
- **Services**: 
  - eddata-collector (EDDN data collector)
  - eddata-api (REST API)
  - eddata-auth (OAuth authentication)
  - eddata-www (Web frontend)

## How to Use

### For Dokploy Users

1. In Dokploy, go to "Create Service" → "From Template"
2. Search for "EDData"
3. Fill in required configuration:
   - **Domain**: Your domain (e.g., `eddata-api.com`)
   - **EDDATA_AUTH_CLIENT_ID**: Your Frontier OAuth Client ID
4. Deploy!

### Required Configuration

You **must** provide a Frontier OAuth Client ID:

1. Create account at: https://auth.frontierstore.net/developer
2. Create OAuth Client
3. Set Callback URL to: `https://auth.YOUR-DOMAIN.com/auth/callback`
4. Copy the Client ID and paste in Dokploy template config

### DNS Setup

Point these subdomains to your server:
- `eddata-api.com` (main domain)
- `www.eddata-api.com`
- `api.eddata-api.com`
- `auth.eddata-api.com`
- `collector.eddata-api.com` (optional, for monitoring)

## Template Features

- ✅ Automatic SSL certificates
- ✅ Service health checks
- ✅ Proper startup order (Collector → API → Auth → WWW)
- ✅ Persistent data volumes
- ✅ Auto-generated security secrets
- ✅ Read-only database access for API (security)

## Contributing to Dokploy Templates

To submit this template to the official Dokploy templates repository:

1. Fork https://github.com/Dokploy/templates
2. Copy the `blueprints/eddata/` folder to the forked repo's `blueprints/` directory
3. Add the entry from `meta.json` to the root `meta.json` file
4. Run `node dedupe-and-sort-meta.js`
5. Create a Pull Request

## More Information

See the main [README.md](../README.md) for complete documentation about the EDData platform.
