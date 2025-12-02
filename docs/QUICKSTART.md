# UI Toolkit Quick Start Guide

Get up and running in 5 minutes.

---

## Ubuntu Server (Docker)

### Local Deployment (LAN Only)

```bash
# Install Docker
sudo apt update && sudo apt install -y docker.io docker-compose
sudo usermod -aG docker $USER && newgrp docker

# Clone and setup
git clone https://github.com/CrosstalkSolutions/unifi-toolkit.git
cd unifi-toolkit
./setup.sh  # Select 1 for Local

# Start
docker-compose up -d

# Access at http://localhost:8000
```

### Production Deployment (Internet-Facing)

```bash
# Install Docker
sudo apt update && sudo apt install -y docker.io docker-compose
sudo usermod -aG docker $USER && newgrp docker

# Clone and setup
git clone https://github.com/CrosstalkSolutions/unifi-toolkit.git
cd unifi-toolkit
./setup.sh  # Select 2 for Production
# Enter: domain, username, password

# Open firewall
sudo ufw allow 80/tcp && sudo ufw allow 443/tcp

# Start with Caddy (HTTPS)
docker-compose --profile production up -d

# Access at https://your-domain.com
```

---

## Common Commands

| Action | Command |
|--------|---------|
| Start (local) | `docker-compose up -d` |
| Start (production) | `docker-compose --profile production up -d` |
| Stop | `docker-compose down` |
| View logs | `docker-compose logs -f` |
| Restart | `docker-compose restart` |
| Reset password | `./reset_password.sh` |
| Update | `git pull && docker-compose build && docker-compose up -d` |

---

## First-Time Setup

1. Open UI Toolkit in browser
2. Click **Wi-Fi Stalker** or **Threat Watch**
3. Click **Settings** (gear icon)
4. Enter UniFi controller details
5. Click **Test Connection**
6. Start tracking devices or monitoring threats

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Can't start | Run `./setup.sh` to create `.env` |
| Can't connect to UniFi | Check URL, credentials, set `UNIFI_VERIFY_SSL=false` |
| Certificate error | Wait 2 minutes, check DNS, ensure port 80 is open |
| Forgot password | Run `./reset_password.sh` then restart |
| Rate limited | Wait 5 minutes |

---

For detailed instructions, see [INSTALLATION.md](INSTALLATION.md).
