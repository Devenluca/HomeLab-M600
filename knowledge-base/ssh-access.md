
## `knowledge-base/ssh-access.md`

```markdown
# SSH Access

## Purpose

SSH is used to administer the Ubuntu Server remotely without requiring a local monitor or keyboard.

## Local Network Access

From a Mac on the home network:

```bash
ssh darrien@10.0.0.167

Remote Access with Tailscale
When away from home:

ssh darrien@100.66.6.30

Authentication
SSH uses an Ed25519 key pair.
The private key remains on the client device.
The public key is stored on the server in:

~/.ssh/authorized_keys

Password-based SSH login was disabled after key authentication was verified.
Quick Health Check
After connecting:

hostname
docker ps
df -h

These commands verify:
- correct host
- running containers
- mounted storage and disk usage

Disconnect
Exit

Useful Troubleshooting Commands
systemctl status ssh
ss -lntp | grep 22
tailscale status
ip addr

