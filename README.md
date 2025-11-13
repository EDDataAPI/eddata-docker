# EDData - Docker Setup for Dokdploy

Complete Docker Compose setup for the EDData API platform with all services.

## 📋 Services

The platform consists of 4 services started in the following order:

1. **eddata-collector** (Port 3002) - Collects data from EDDN
2. **eddata-api** (Port 3001) - REST API for Elite Dangerous data
3. **eddata-auth** (Port 3003) - Authentication service
4. **eddata-www** (Port 3000) - Web frontend

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Dokdploy (or another hosting with Traefik/SSL)
- Domain with DNS records for all subdomains

### 1. Clone Repository

```bash
git clone <your-repo-url>
cd eddata-docker
```

### 2. Configure Environment Variables

```bash
cp .env.example .env
```

Edit `.env` and set the following **important** values:

```bash
# Domain Configuration
EDDATA_DOMAIN=your-domain.com

# Security Secrets (IMPORTANT! Generate secure random values!)
EDDATA_SESSION_SECRET=<64-byte-hex-string>
EDDATA_AUTH_JWT_SECRET=<64-byte-hex-string>

# Frontier OAuth Client ID
EDDATA_AUTH_CLIENT_ID=<your-frontier-client-id>
```

#### Generate Secrets

Run the following commands to generate secure secrets:

```bash
# Session Secret
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"

# JWT Secret
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

### 3. Start Services

```bash
docker-compose up -d
```

### 4. Check Status

```bash
# Show all services
docker-compose ps

# Follow logs
docker-compose logs -f

# Single service
docker-compose logs -f eddata-collector
```

## 🔧 Configuration

### DNS Records

Set up the following DNS A-Records pointing to your server IP:

- `eddata-api.com` (oder deine Domain)
- `www.eddata-api.com`
- `api.eddata-api.com`
- `auth.eddata-api.com`
- `collector.eddata-api.com` (optional, for monitoring)

### Environment Variables

All available environment variables can be found in `.env.example`.

**Important Variables:**

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `EDDATA_DOMAIN` | Your main domain | `eddata-api.com` | Yes |
| `EDDATA_SESSION_SECRET` | Session secret for auth | - | **Yes** |
| `EDDATA_AUTH_JWT_SECRET` | JWT secret for tokens | - | **Yes** |
| `EDDATA_AUTH_CLIENT_ID` | Frontier OAuth Client ID | - | **Yes** |

### Volumes

Data is stored in the following Docker volumes:

- `eddata-data` - Main database and cache
- `eddata-backup` - Database backups
- `eddata-downloads` - Download files

## 📊 Service Overview

### eddata-collector

**Function:** Collects real-time data from Elite Dangerous Data Network (EDDN)

**Important:** This service MUST start first as it creates the databases!

**Endpoints:**
- `http://localhost:3002/` - Status
- `http://localhost:3002/health` - Health Check

**Volumes:**
- Write access to all volumes (creates and updates databases)

### eddata-api

**Function:** REST API for accessing collected data

**Depends on:** collector (with `service_healthy`)

**Endpoints:**
- `http://localhost:3001/api/v2/stats` - Statistics
- `http://localhost:3001/api/v2/systems` - System data
- Full API documentation: see [eddata-api README](https://github.com/EDDataAPI/eddata-api)

**Volumes:**
- Read-only access to data

### eddata-auth

**Function:** OAuth authentication with Frontier Developments API

**Depends on:** api (with `service_healthy`)

**Endpoints:**
- `http://localhost:3003/auth/signin` - Start login
- `http://localhost:3003/health` - Health check

**Important:** Requires valid Frontier OAuth credentials!

### eddata-www

**Function:** Web frontend for users

**Depends on:** api, auth (with `service_healthy`)

**Endpoints:**
- `http://localhost:3000/` - Main page

## 🔍 Health Checks

All services have integrated health checks:

```bash
# Collector
curl http://localhost:3002/health

# API
curl http://localhost:3001/api/v2/stats

# Auth
curl http://localhost:3003/health

# WWW
curl http://localhost:3000/
```

## 🐳 Docker Commands

### Manage Services

```bash
# Start all services
docker-compose up -d

# Stop all services
docker-compose down

# Restart services
docker-compose restart

# Restart single service
docker-compose restart eddata-api
```

### Logs

```bash
# All logs
docker-compose logs -f

# Collector only
docker-compose logs -f eddata-collector

# API only
docker-compose logs -f eddata-api

# Last 100 lines
docker-compose logs --tail=100 -f
```

### Updates

```bash
# Update images
docker-compose pull

# Restart services with new images
docker-compose up -d --force-recreate
```

## 🔒 Security

### HTTPS / SSL

The setup is prepared for Traefik (Dokdploy default):

- Automatic SSL certificates via Let's Encrypt
- HSTS headers
- Automatic HTTP → HTTPS redirect

### Secrets

**IMPORTANT:** Change all secrets in `.env` before deployment!

```bash
# NEVER use default values!
EDDATA_SESSION_SECRET=<generate-new-value>
EDDATA_AUTH_JWT_SECRET=<generate-new-value>
```

### Non-Root User

All containers run as non-root user (`eddata:1001`) for better security.

## 📦 Volumes & Data

### Create Backup

```bash
# Manual backup
docker-compose exec eddata-collector npm run backup

# Show backup files
docker volume inspect eddata-backup
```

### Database Statistics

```bash
# Generate statistics
docker-compose exec eddata-collector npm run stats

# Show statistics
docker-compose exec eddata-collector cat /app/eddata-data/cache/database-stats.json
```

### Optimize Databases

```bash
# Optimize databases
docker-compose exec eddata-collector npm run optimize
```

## 🐛 Troubleshooting

### Collector Won't Start

**Problem:** Collector cannot connect to EDDN

**Solution:**
```bash
# Check EDDN server
docker-compose logs eddata-collector | grep "EDDN"

# Test manually
docker-compose exec eddata-collector ping eddn.edcd.io
```

### API Shows No Data

**Problem:** Databases not yet created

**Solution:**
```bash
# Wait until collector has gathered data (may take a few minutes)
docker-compose logs -f eddata-collector

# Check if databases exist
docker-compose exec eddata-api ls -lh /app/eddata-data/
```

### Auth Fails

**Problem:** Missing or invalid Frontier OAuth credentials

**Solution:**
```bash
# Check environment variables
docker-compose exec eddata-auth env | grep EDDATA_AUTH

# Create Frontier Developer Account and get Client ID
# https://auth.frontierstore.net/developer
```

### Port Already in Use

**Problem:** Port 3000-3003 already in use

**Solution:**
```bash
# Change ports in docker-compose.yml
# Example: "8001:3001" instead of "3001:3001"
```

## 🔧 Maintenance

### Automatic Maintenance

The collector performs automatic weekly maintenance:

- Thursdays 7:00-9:00 UTC (Elite Dangerous maintenance window)
- Database optimization
- Backup creation
- Clean old data

### Manual Maintenance

```bash
# Backup
docker-compose exec eddata-collector npm run backup

# Optimierung
docker-compose exec eddata-collector npm run optimize

# Statistiken
docker-compose exec eddata-collector npm run stats
```

## 📊 Monitoring

### Service Status

```bash
# All services
docker-compose ps

# Health checks
curl http://localhost:3002/health  # Collector
curl http://localhost:3001/api/v2/stats  # API
curl http://localhost:3003/health  # Auth
curl http://localhost:3000/  # WWW
```

### Resource Usage

```bash
# Container stats
docker stats

# Disk usage
docker system df

# Volume size
docker system df -v
```

## 🌐 Dokdploy-Specific

### Setup in Dokdploy

1. **Create Project:**
   - Name: `eddata`
   - Type: `Docker Compose`

2. **Connect Repository:**
   - GitHub Repository URL
   - Branch: `main`
   - Compose File: `docker-compose.yml`

3. **Set Environment Variables:**
   - All values from `.env.example`
   - **Important:** Mark secrets as "Secret"!

4. **Configure Domains:**
   - Main domain for WWW
   - Subdomains for API, Auth, Collector

5. **Deployment:**
   - Click "Deploy" button
   - Monitor logs

### Traefik Integration

The setup includes all necessary Traefik labels for:

- Automatic SSL certificates
- Load balancing
- Health checks
- Security headers

## 📚 Additional Resources

- [EDData Collector](https://github.com/EDDataAPI/eddata-collector)
- [EDData API](https://github.com/EDDataAPI/eddata-api)
- [EDData Auth](https://github.com/EDDataAPI/eddata-auth)
- [EDData WWW](https://github.com/EDDataAPI/eddata-www)
- [EDDN](https://github.com/EDCD/EDDN)

## 🤝 Support

- Issues: GitHub Issues in respective repositories
- Documentation: README files of individual services

## ⚠️ Important Notes

1. **Startup Order:** Collector → API → Auth → WWW
2. **Secrets:** Never use default values!
3. **Frontier OAuth:** Valid Client ID required
4. **Databases:** Created on first start by collector
5. **SSL:** Requires valid DNS entries
6. **Maintenance:** Automatic Thursdays 7-9 UTC
