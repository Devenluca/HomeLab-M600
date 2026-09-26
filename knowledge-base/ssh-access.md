# SSH Access

SSH is used to administer the Ubuntu Server remotely without a local monitor or keyboard.

## Local Network Access

Replace the uppercase placeholders with your server username and address.

```bash
ssh <USERNAME>@<SERVER_LAN_IP>
```

## Remote Access with Tailscale

Connect the client to your Tailscale network before using the server's Tailscale address.

```bash
ssh <USERNAME>@<SERVER_TAILSCALE_IP>
```

## Authentication

SSH uses an Ed25519 key pair. The private key remains on the client device; the public key is stored in the server user's `~/.ssh/authorized_keys`. Password-based SSH login was disabled after key authentication was verified.

## Quick Health Check

After connecting:

```bash
hostname
docker ps
df -h
```

These commands show the host name, running containers, and mounted filesystem usage.

## Disconnect

```bash
exit
```

## Troubleshooting Commands

Run these on the server to inspect SSH, listening ports, Tailscale, and network interfaces:

```bash
systemctl status ssh
ss -lntp
tailscale status
ip addr
```

Check for port 22 in the listening-port output. See [service ports](service-ports.md) for the other documented services.
