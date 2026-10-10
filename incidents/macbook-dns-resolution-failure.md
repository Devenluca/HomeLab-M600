# Incident: MacBook DNS Resolution Failure

## Summary

The MacBook used to administer the M600 homelab experienced a client-side DNS resolution failure while connected to workplace Wi-Fi. Basic IP connectivity was available, but name resolution and web browsing failed. Temporarily configuring public DNS resolvers restored name resolution and normal browsing. The exact root cause was not confirmed.

This incident concerns the administration client; it does not establish a failure of the M600 server.

## Symptoms

- The MacBook was connected to workplace Wi-Fi.
- Web browsing was failing.
- `ping 8.8.8.8` succeeded.
- `nslookup google.com` failed with:

  ```text
  connection timed out; no servers could be reached
  ```

## Investigation

The successful ping to `8.8.8.8` demonstrated basic IP connectivity to that address without requiring DNS resolution. The failed `nslookup google.com` showed that the DNS lookup could not obtain a response from the resolver path used by that command.

Together, these observations supported investigating DNS resolution on the MacBook. They did not identify the original DNS server or establish why it was unavailable.

This record is based on reported observations. No screenshots or captured runtime logs are included.

## Root Cause

**Not confirmed.** The following are unverified possibilities, not findings:

- Stale DNS settings on the MacBook.
- An unreachable DNS server.
- VPN or Tailscale DNS interaction.
- Bad DNS settings supplied by the workplace network.

Recovery after changing resolvers does not distinguish between these possibilities.

## Resolution

The MacBook was temporarily configured to use public DNS resolvers `1.1.1.1` and `8.8.8.8`. Name resolution and normal web browsing worked again after this change.

This was a workaround; it did not confirm or repair the underlying cause. No M600 server change is recorded for this incident.

## Verification

- **Reported before the change:** `ping 8.8.8.8` succeeded, while `nslookup google.com` timed out.
- **Reported after the change:** name resolution and normal web browsing worked again.
- **Evidence limit:** no post-change command output or screenshots are included. The original resolver state and exact root cause remain unconfirmed.

## Follow-Up

For a future incident, capture resolver state before changing settings:

```bash
scutil --dns | grep 'nameserver'
networksetup -getdnsservers Wi-Fi
```

These are recommended future checks, not commands with recorded results from this incident. Preserve the outputs alongside the failed lookup and connectivity checks, sanitizing identifying information before publication. The filtered `scutil` output lists nameserver entries; it does not preserve the full resolver context. The `networksetup` command reports DNS settings for the Wi-Fi network service.

To remove the temporary manual DNS settings and restore automatic DNS later:

```bash
sudo networksetup -setdnsservers Wi-Fi Empty
```

Restoring automatic DNS has not been confirmed. After restoring it, repeat the name-resolution and browsing checks and record the actual results.

## Troubleshooting Flow

1. Confirm the client is connected to Wi-Fi and record the browsing symptom.
2. Test basic IP connectivity with `ping 8.8.8.8`.
3. Test DNS resolution with `nslookup google.com`.
4. If IP connectivity succeeds but DNS fails, capture resolver state before making changes.
5. Temporarily change DNS resolvers, then repeat name-resolution and browsing checks.
6. Record the observed outcome, retain uncertainty about the root cause, and restore automatic DNS when appropriate.

This is a reusable troubleshooting procedure. Resolver-state capture and restoration of automatic DNS are follow-up steps, not completed actions documented for this incident.

## Skills Practiced

- Separating basic IP connectivity from DNS resolution during troubleshooting.
- Using `ping` and `nslookup` to narrow a client networking issue.
- Applying a temporary DNS workaround and checking the reported recovery.
- Documenting observed evidence separately from unverified hypotheses.
