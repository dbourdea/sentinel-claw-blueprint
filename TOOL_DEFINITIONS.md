# Agent Tool Definitions

To interact with the firewall, the agent needs the following programmatic tools (implemented as OpenClaw skills):

## 1. `firewall_ssh_exec`
Executes a single command on the router via SSH.
- **Input**: `command` (string)
- **Examples**: `logread | tail -n 100`, `uci show firewall`.

## 2. `ip_block_action`
Adds an IP to the `banIP` custom blocklist.
- **Input**: `ip_address`, `reason`.
- **Logic**: Executes `uci add_list banip.custom.ban_ip=$IP`.

## 3. `fetch_agh_stats`
Queries the AdGuard Home API for top blocked domains.
- **Output**: JSON object of recent DNS threats.

## 4. `check_service_health`
Checks if `crowdsec`, `adguardhome`, and `tailscaled` are running.
- **Logic**: Wraps `/etc/init.d/$SERVICE status`.

## 5. `notify_user`
Sends a formatted message to the user's mobile device.
- **Input**: `priority` (URGENT/DIGEST), `message` (string).
