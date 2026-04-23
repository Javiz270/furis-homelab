# 🖥️ furis.art — Personal Homelab & Self-Hosted Infrastructure

> Personal home server running multiple self-hosted services on bare-metal Debian Linux, exposed securely via tunnel and custom domain — no port forwarding required.

---

## Overview

This project documents the setup and architecture of my personal home server, built on an old desktop PC repurposed as an always-on Linux server. The goal was to self-host services accessible from anywhere using a custom domain, without exposing the home network's public IP or opening router ports.

**Live domain:** `furis.art` (managed via Namecheap → Cloudflare DNS)

---

## Hardware

| Component | Spec |
|-----------|------|
| CPU | Intel Pentium G2020 |
| Storage | 256 GB SSD (dedicated, clean install) |
| OS | Debian Linux (bare-metal) |

---

## Stack

| Layer | Technology |
|-------|-----------|
| Operating System | Debian Linux |
| Server Dashboard | CasaOS |
| Media Server | Jellyfin |
| Game Server | Minecraft Java Edition |
| Tunnel / Expose | Pinggy |
| DNS Management | Cloudflare |
| Domain Registrar | Namecheap |

---

## Architecture

```
Local Machine (Debian)
        │
        ├── CasaOS Dashboard
        ├── Jellyfin (media server)
        └── Minecraft Server
                │
                └──► Pinggy Tunnel (TCP)
                            │
                            └──► Cloudflare DNS
                                        │
                                        └──► furis.art (Namecheap)
```

All external traffic is routed through **Pinggy**, eliminating the need to open ports on the router or expose the home IP. Cloudflare handles DNS resolution and adds an additional layer of protection.

---

## Subdomains & Services

| Subdomain | Service | Purpose |
|-----------|---------|---------|
| `mc.furis.art` | Minecraft Server | Direct connect address for players |
| `discord.furis.art` | Redirect | Permanent vanity URL → Discord invite link |

---

## Setup Process

### 1. Debian Installation
- Created bootable USB with Debian installer
- Performed clean install on dedicated 256 GB SSD
- Configured basic networking, SSH, and system users

### 2. CasaOS
- Installed via official one-line script
- Used as dashboard for service management and monitoring

### 3. Jellyfin
- Deployed through CasaOS app store
- Configured local media library

### 4. Minecraft Server
- Deployed Java Edition server on Debian
- Configured `server.properties` for the environment

### 5. Tunnel & DNS
- Cloudflare Tunnel was evaluated but lacked TCP support needed for Minecraft's protocol
- Selected **Pinggy** as an alternative — supports raw TCP tunneling
- Pointed `furis.art` nameservers to Cloudflare
- Created DNS CNAME/A records for each subdomain targeting the Pinggy tunnel endpoint

---

## Key Decisions

**Why Pinggy over Cloudflare Tunnel?**
Cloudflare Tunnel works well for HTTP/HTTPS services but does not support the raw TCP protocol that Minecraft uses. Pinggy fills this gap by providing TCP tunnel support, while Cloudflare still handles DNS for the domain.

**Why a dedicated SSD?**
To avoid repartitioning a drive with existing data and keep the server environment completely isolated from other systems.

**Why CasaOS?**
Provides a lightweight web dashboard for managing services without needing to SSH for every operation — practical for a single-node homelab.

---

## What I Learned

- Linux server administration on bare-metal hardware
- Self-hosting services and managing them as persistent background processes
- DNS management: nameservers, A records, CNAMEs, subdomain routing
- Tunneling protocols and why different services require different approaches (HTTP vs TCP)
- Trade-offs between simplicity, security, and compatibility when choosing infrastructure tools

---

## Status

> Server currently offline. All configuration is preserved and can be restored. Documentation written from the working setup.

---

*Part of my homelab & self-hosting learning path — alongside S.A.R.A. (IoT access control system) and LoRa networking experiments.*
