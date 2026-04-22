# Resource Constraints & Guardrails

SentinelClaw must operate within the strict physical limits of the Linksys EA8100 v2 hardware to prevent system crashes or "OOM" (Out of Memory) kills.

## Hardware Specs
- **CPU**: MediaTek MT7621AT (Dual-core, 880 MHz)
- **RAM**: 256 MB
- **Flash**: 32 MB (Total), ~24 MB (Available for /overlay)

## Critical Constraints

### 1. Storage (The /opt Mandate)
- **Rule**: NO persistent data larger than 10KB should be stored in `/etc` or `/root`.
- **Reason**: The internal flash memory is extremely limited and has a finite write cycle.
- **Action**: Use `/opt` (external 2GB partition) for all logs, databases (CrowdSec), and binary storage.

### 2. Memory (RAM)
- **Rule**: Avoid running multiple intensive scans simultaneously.
- **Reason**: 256MB is barely enough to run AdGuard Home and CrowdSec together.
- **Action**: The agent should monitor `free -m` and kill/restart non-essential processes if available RAM drops below 20MB.

### 3. CPU (Traffic Impact)
- **Rule**: Extensive `nft` rule generation or complex regex log parsing should be offloaded to the OpenClaw host.
- **Reason**: Heavy CPU usage on the router causes packet latency and drops SQM performance.
- **Action**: Stream raw logs to the host; only send "Action" commands (e.g., specific IP bans) back to the router.
