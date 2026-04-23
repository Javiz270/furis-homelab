# Debian Base Setup

Initial configuration applied after clean Debian install on dedicated SSD.

---

## 1. System Update

```bash
apt update && apt upgrade -y
```

## 2. Install Essential Tools

```bash
apt install -y curl wget git sudo ufw htop net-tools
```

## 3. Create Non-Root User

```bash
adduser javi
usermod -aG sudo javi
```

## 4. Configure Firewall (UFW)

```bash
ufw allow OpenSSH
ufw enable
ufw status
```

## 5. Enable SSH

```bash
systemctl enable ssh
systemctl start ssh
```

## 6. Verify Network

```bash
ip a
ping -c 4 google.com
```

---

*Base system ready — proceed to CasaOS installation.*
