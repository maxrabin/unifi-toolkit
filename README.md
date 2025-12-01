# UI Toolkit

A suite of tools for UniFi network management.

> **Note:** This project is not affiliated with, endorsed by, or sponsored by Ubiquiti Inc. UniFi is a trademark of Ubiquiti Inc.

## Tools

### Wi-Fi Stalker
Track specific Wi-Fi client devices through UniFi infrastructure. Monitor connection status, detect roaming between access points, and maintain historical logs.

**Features:** Device tracking, roaming detection, connection history, webhooks (Slack/Discord/n8n)

### IDS Monitor *(Coming Soon)*
View blocked IPs and intrusion detection/prevention system events.

### UI Product Selector *(External)*
Build the perfect UniFi network at [uiproductselector.com](https://uiproductselector.com)

## Quick Start

### Requirements
- Python 3.9-3.12 (3.13+ not supported yet)
- UniFi Controller (any version)

### Installation

```bash
git clone git@github.com:Crosstalk-Solutions/unifi-toolkit.git
cd unifi-toolkit

python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

pip install -r requirements.txt

cp .env.example .env
```

Generate an encryption key and add it to `.env`:
```bash
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
```

Start the application:
```bash
python run.py
```

Access at `http://localhost:8000`

### Docker

```bash
git clone git@github.com:Crosstalk-Solutions/unifi-toolkit.git
cd unifi-toolkit

cp .env.example .env
# Add ENCRYPTION_KEY to .env

docker compose up -d
```

## Configuration

### Required
- `ENCRYPTION_KEY` - Encrypts UniFi credentials (generate with command above)

### Optional
UniFi settings can be configured via `.env` or the web UI:

| Variable | Description |
|----------|-------------|
| `UNIFI_CONTROLLER_URL` | Controller URL (e.g., `https://192.168.1.1`) |
| `UNIFI_USERNAME` | Username (legacy controllers) |
| `UNIFI_PASSWORD` | Password (legacy controllers) |
| `UNIFI_API_KEY` | API key (UniFi OS devices: UDM, UCG) |
| `UNIFI_SITE_ID` | Site ID (default: `default`) |
| `UNIFI_VERIFY_SSL` | SSL verification (default: `false`) |
| `STALKER_REFRESH_INTERVAL` | Device refresh interval in seconds (default: `60`) |

## Troubleshooting

**Can't connect to UniFi controller**
- Set `UNIFI_VERIFY_SSL=false` for self-signed certificates
- UniFi OS devices (UDM, UCG) require an API key, not username/password

**Device not showing as online**
- Wait 60 seconds for refresh
- Verify MAC address is correct
- Check device is connected in UniFi dashboard

**Docker issues**
- Verify `.env` contains `ENCRYPTION_KEY`
- Check logs: `docker compose logs`

## Migrating from Wi-Fi Stalker

See [docs/MIGRATION.md](docs/MIGRATION.md) for migration instructions from the standalone wifi-stalker application.

## Support

- Issues: https://github.com/Crosstalk-Solutions/unifi-toolkit/issues

## Credits

Developed by [Crosstalk Solutions](https://www.crosstalksolutions.com/)
- YouTube: [@CrosstalkSolutions](https://www.youtube.com/@CrosstalkSolutions)

## License

MIT License
