# User Interaction Model

SentinelClaw communicates via the OpenClaw messaging gateway (Telegram/WhatsApp/Slack).

## Inbound Commands (User -> Agent)

| Command | Description |
| :--- | :--- |
| `/status` | Returns health of AdGuard Home, CrowdSec, and WAN latency. |
| `/report` | Generates a summary of the last 24 hours of blocks. |
| `/unblock <IP>` | Manually removes an IP from the `banIP` custom blocklist. |
| `/pause` | Temporarily suspends the agent's autonomous blocking authority. |
| `/whois <IP>` | Asks the agent to research an IP's reputation and origin. |

## Outbound Alerts (Agent -> User)

### High Priority (Immediate)
> "🚨 **Critical Alert**: Successful SSH login to Router from unknown IP: `203.0.113.5`. Action Taken: User session monitored. Response needed: Block this IP?"

### Medium Priority (Digest Only)
> "📝 **Daily Security Intelligence**: 
> - Total Ads Blocked: 1,245
> - Malicious IPs Banned: 12
> - Top Attacker Origin: Russia (AS12345)"
