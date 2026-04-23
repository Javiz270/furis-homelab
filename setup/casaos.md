# CasaOS Installation

Dashboard for managing self-hosted services on the homelab.

---

## Install via Official Script

```bash
curl -fsSL https://get.casaos.io | sudo bash
```

The script automatically detects the OS, installs Docker, and sets up the CasaOS web interface.

---

## Access Dashboard

After installation, access CasaOS from any device on the local network:

```
http://<server-local-ip>:80
```

Find the server's local IP with:

```bash
ip a | grep inet
```

---

## Services Installed via CasaOS

| Service | Purpose |
|---------|---------|
| Jellyfin | Media server (movies, local library) |
| Minecraft Server | Game server (Java Edition) |

Both services managed and monitored through the CasaOS dashboard.

---

*For external access configuration, see the main README — tunnel setup via Pinggy and DNS via Cloudflare.*
