# Recovery & "Break Glass" Procedures

In the event that SentinelClaw misconfigures the firewall or locks out administrative access, use the following steps.

## 1. Physical Emergency Access
- **Method**: Connect a computer directly to a LAN port on the Linksys.
- **IP**: The router defaults to `192.168.100.1`.
- **Action**: Manually log in via SSH or LuCI to revert the last change.

## 2. Disabling the Agent
If the agent is stuck in a "reboot loop" or making incorrect autonomous changes:
1.  Log into the OpenClaw host machine.
2.  Stop the OpenClaw service: `pnpm openclaw stop` (or equivalent).
3.  On the router, disable the agent's SSH key by commenting it out in `/etc/dropbear/authorized_keys`.

## 3. Reverting UCI Changes
The agent should log every `uci set` command it runs. To see the history and revert:
```bash
uci changes
# To revert everything uncommitted:
uci revert firewall
```

## 4. Hardware Reset
As a last resort, hold the **Reset Button** on the back of the EA8100 for 10 seconds to restore OpenWrt to its post-flash default state. (Note: This will require re-mounting the `/opt` drive and re-running the setup).
