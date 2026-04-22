# Incident Response Playbooks

This document provides standardized logic for SentinelClaw when specific threat signatures are detected.

## 1. Brute Force Detection (SSH/LuCI)
- **Signature**: >5 failed login attempts within 2 minutes from a single IP.
- **Agent Action**:
    1. Verify if IP is on the internal "Known Device" allowlist.
    2. If external, use `ip_block_action` to ban for 24 hours.
    3. Notify user: "Blocked IP [X] after repeated login failures."

## 2. Potential Exfiltration / C2 Beaconing
- **Signature**: Internal device querying a "Malware" or "C&C" category domain in AdGuard Home.
- **Agent Action**:
    1. Immediately block the domain network-wide.
    2. Identify the internal IP/MAC of the requesting device.
    3. **ESCALATE TO USER**: "Device [Name/IP] is attempting to contact a known malware domain. Domain blocked. Suggest manual scan of device."

## 3. High Egress Spike (The "Zombie" Check)
- **Signature**: `darkstat` reports a device exceeding 1GB of egress traffic in < 1 hour to an unknown external IP.
- **Agent Action**:
    1. Check `ntop` or `darkstat` for the destination port.
    2. If port is unusual (non-443/80), throttle the device's bandwidth via `sqm` (limit to 1Mbps).
    3. Ask User: "Device [X] is sending unusual amounts of data. I have limited its speed. Should I block it entirely?"
