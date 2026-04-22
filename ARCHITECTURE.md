# Technical Architecture

The agent operates on a **Observe -> Orient -> Decide -> Act (OODA)** loop, integrated across your Linksys Router and your OpenClaw host machine.

## 1. Data Ingestion (Observe)
- **Log Streaming**: The router uses `syslog-ng` or standard `remote-log` to send all kernel and service logs to the OpenClaw host.
- **API Polling**: The agent periodically queries:
    - **AdGuard Home API**: For DNS-level query trends and top-blocked domains.
    - **CrowdSec LAPI**: For recent decisions and local behavioral alerts.
    - **darkstat**: For bandwidth anomalies.

## 2. Reasoning Engine (Orient & Decide)
- **Framework**: OpenClaw.
- **Tiered Intelligence**:
    - **Tier 1 (Sentry)**: Local **Lemonade Server** (e.g., Llama 3) handles routine log parsing and anomaly detection to ensure data privacy and zero cost.
    - **Tier 2 (Architect)**: **OpenRouter (Claude 3.5 Sonnet)** handles deep reasoning, incident investigation, and high-stakes decision making.
- **Context Window**: Maintained with recent logs, current firewall state, and known internal IP identities.

## 3. Execution (Act)
- **Transport**: SSH (Key-based) from OpenClaw host to Router.
- **Permissions**: Restricted to `uci`, `nft`, `tailscale`, and service restarts.

## 4. Communication Channel
- **Urgent**: Pushed to User via Telegram/WhatsApp immediately.
- **Non-Urgent**: Batched into a local SQLite DB and summarized daily.
