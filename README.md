# ProxyDeck

A powerful, self-hosted reverse proxy manager with built-in SSL certificate management, Web Application Firewall (WAF), bot protection, and real-time analytics.

## Screenshots

### Dashboard
![Dashboard](images/dashboard.png)
*Real-time overview of traffic, requests, and system health*

### Proxy Hosts
![Proxy Hosts](images/hosts.png)
*Manage reverse proxy configurations with SSL settings*

### SSL Certificates
![SSL Certificates](images/certs.png)
*Let's Encrypt integration with automatic renewal*

### WAF & Security
![WAF Events](images/waf.png)
*Web Application Firewall with real-time event logging*

### Bot Protection
![Bot Protection](images/bot-protection.png)
*JavaScript challenges and threat scoring*

### Analytics
![Analytics](images/analytics.png)
*Traffic analytics with geographic distribution*

### Status Monitoring
![Status](images/status.png)
*Uptime monitoring and health checks*

### User Management
![Users](images/users.png)
*Multi-user support with MFA and Passkeys*

### DNS Management
![DNS](images/dns.png)
*Manage DNS zones and records with Cloudflare/Hetzner integration*

### Profile
![Profile](images/profile.png)
*User profile with MFA and Passkey management*

### Audit Log
![Audit](images/audit.png)
*Complete audit trail of all system changes*

### Settings
![Settings](images/settings.png)
*Backup, API keys, webhooks, and SMTP configuration*

## Features

### Reverse Proxy Management
- **Easy Host Configuration** - Add and manage proxy hosts through an intuitive web interface
- **Multiple Backends** - Support for HTTP and HTTPS upstream servers
- **Load Balancing** - Distribute traffic across multiple backend servers
- **WebSocket Support** - Full WebSocket proxying capabilities
- **HTTP/3 (QUIC)** - Modern protocol support for improved performance

### SSL/TLS Certificate Management
- **Let's Encrypt Integration** - Automatic SSL certificate issuance and renewal
- **HTTP-01 & DNS-01 Challenges** - Support for both validation methods
- **Wildcard Certificates** - Issue wildcard certs via DNS-01 challenge
- **Custom Certificates** - Import your own SSL certificates
- **Certificate Monitoring** - Automatic expiry alerts and health checks
- **Rate Limit Tracking** - Prevents hitting Let's Encrypt rate limits

### DNS Management
- **Multi-Provider Support** - Cloudflare and Hetzner DNS integration
- **Zone Management** - View and manage all your DNS zones
- **Record Management** - Create, update, and delete DNS records (A, AAAA, CNAME, MX, TXT, etc.)
- **Available Domains** - See which domains from your DNS zones can be used for new proxy hosts
- **Credential Verification** - Validate API tokens before saving
- **DNS-01 Automation** - Automatic DNS record creation for Let's Encrypt wildcard certificates

### Web Application Firewall (WAF)
- **SQL Injection Protection** - Detects and blocks SQL injection attempts
- **XSS Prevention** - Cross-site scripting attack mitigation
- **Path Traversal Detection** - Blocks directory traversal attacks
- **Custom Rules** - Define your own WAF rules per host
- **Real-time Event Logging** - View and analyze security events

### Bot Protection
- **JavaScript Challenge** - Browser verification for suspicious requests
- **Threat Scoring** - Intelligent threat analysis and scoring
- **Automatic Banning** - Block malicious IPs automatically
- **GeoIP Integration** - Country-based access control
- **Configurable Thresholds** - Fine-tune protection levels per host

### Rate Limiting
- **Request Rate Limiting** - Protect against DDoS and abuse
- **Per-Host Configuration** - Different limits for different services
- **Burst Handling** - Allow temporary traffic spikes
- **IP Whitelisting** - Bypass limits for trusted IPs
- **Redis-backed** - Distributed rate limiting across instances

### Analytics & Monitoring
- **Real-time Dashboard** - Live traffic and request monitoring
- **Traffic Analytics** - Detailed request statistics and trends
- **Geographic Distribution** - Visualize traffic origins on a world map
- **Protocol Distribution** - HTTP/HTTPS/HTTP2/HTTP3 breakdown
- **Top Endpoints** - Most accessed paths and resources
- **Uptime Monitoring** - Backend health checks with alerting

### User Management
- **Multi-User Support** - Multiple admin accounts with role-based access
- **Two-Factor Authentication (MFA)** - TOTP-based 2FA with backup codes
- **Passkey Support** - WebAuthn/FIDO2 passwordless authentication
- **SSO Integration** - Single Sign-On with Microsoft Entra ID (Azure AD)
- **Session Management** - Automatic idle timeout and session control
- **Audit Logging** - Track all user actions and changes

### System Features
- **Backup & Restore** - Full configuration backup with encryption
- **API Access** - RESTful API with API key authentication
- **Webhooks** - Event notifications to external services
- **SMTP Integration** - Email notifications for alerts
- **Dark Mode UI** - Modern, responsive web interface
- **Multi-language** - English and German interface

## Architecture

ProxyDeck runs as a Docker container with the following components:

- **Nginx** - High-performance reverse proxy server
- **Node.js** - Backend API and management server
- **PostgreSQL** - Configuration and analytics database
- **Redis** - Caching and distributed rate limiting
- **Supervisord** - Process management

## Requirements

- Docker and Docker Compose
- 2GB RAM minimum (4GB recommended)
- 2 CPU cores minimum
- Ports 80, 443, and 8070 available

## Quick Start

### 1. Clone this repository

```bash
git clone https://github.com/pamsler/proxydeck.git
cd proxydeck
```

### 2. Create environment file

```bash
cp .env.example .env
```

### 3. Configure required variables

Edit `.env` and set at minimum:

```bash
# Admin credentials
ADMIN_USER=admin
ADMIN_PASS=your-secure-password-here

# Security keys (generate with: openssl rand -hex 64)
JWT_SECRET=your-64-char-hex-secret
MFA_ENCRYPTION_KEY=your-64-char-hex-key

# Optional: Let's Encrypt email for SSL certificates
ACME_EMAIL=your-email@example.com
```

### 4. Create backup directory

```bash
mkdir -p backup
```

### 5. Start ProxyDeck

```bash
docker compose -f docker-compose.prod.yml up -d
```

### 6. Access the dashboard

Open `http://your-server-ip:8070` in your browser and log in with your admin credentials.

## Configuration

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `IMAGE_TAG` | No | `latest` | Docker image version tag |
| `ADMIN_USER` | Yes | - | Admin username |
| `ADMIN_PASS` | Yes | - | Admin password |
| `JWT_SECRET` | Yes | - | JWT signing secret (64+ chars) |
| `MFA_ENCRYPTION_KEY` | Yes | - | MFA encryption key (64+ chars) |
| `ADMIN_EMAIL` | No | - | Admin email for notifications |
| `ACME_EMAIL` | No | - | Let's Encrypt registration email |
| `ACME_ACCOUNT` | No | - | Specific LE account to use |
| `FRONTEND_URL` | No | - | Auto-setup proxy for this URL |
| `TZ` | No | `Europe/Zurich` | Timezone |
| `ENABLE_H3` | No | `1` | Enable HTTP/3 (QUIC) |
| `MICROCACHE_SECS` | No | `5` | Micro-cache duration |
| `ISOLATION_HEADERS` | No | `0` | Enable COOP/COEP/CORP headers |

### Ports

| Port | Protocol | Description |
|------|----------|-------------|
| 80 | HTTP | HTTP traffic and ACME challenges |
| 443 | HTTPS | HTTPS traffic |
| 8070 | HTTP | Management dashboard |

### Volumes

| Volume | Description |
|--------|-------------|
| `confd` | Nginx configuration files |
| `data` | Application data |
| `certs` | SSL certificates |
| `acme` | ACME challenge files |
| `le_etc` | Let's Encrypt configuration |
| `le_var` | Let's Encrypt work directory |
| `le_log` | Let's Encrypt logs |
| `pgdata` | PostgreSQL database |
| `redis_data` | Redis persistence |

## Updating

To update to a new version:

```bash
# Pull the latest image
docker compose -f docker-compose.prod.yml pull

# Restart with new image
docker compose -f docker-compose.prod.yml up -d
```

Or specify a specific version in `.env`:

```bash
IMAGE_TAG=v1.2.0
```

## Security Recommendations

1. **Change default credentials** - Never use default passwords in production
2. **Enable MFA** - Set up two-factor authentication for all admin accounts
3. **Use HTTPS** - Set up SSL for the management dashboard
4. **Restrict access** - Use firewall rules to limit dashboard access
5. **Regular backups** - Enable automatic backups in settings
6. **Keep updated** - Regularly update to the latest version

## API Documentation

ProxyDeck provides a RESTful API for automation. Generate API keys in Settings > API Keys.

Example:
```bash
curl -H "X-API-Key: your-api-key" http://localhost:8070/api/proxies
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Note**: This repository contains only the deployment configuration. The application is distributed as a Docker image via Docker Hub.
