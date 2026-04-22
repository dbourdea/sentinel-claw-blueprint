# Log Handling & Aggregation

For the agent to "Hunt" threats, it needs high-fidelity data.

## Configuration on Router

1.  **Configure Remote Logging**:
    ```bash
    uci set system.@system[0].log_ip='<OPENCLAW_HOST_IP>'
    uci set system.@system[0].log_port='514'
    uci set system.@system[0].log_proto='udp'
    uci commit system
    /etc/init.d/system restart
    ```

2.  **Service-Specific Logs**:
    - **CrowdSec**: Ensure `acquis.yaml` is watching `/var/log/messages` and `/var/log/auth.log`.
    - **AdGuard Home**: Logs are accessible via the internal API on port 3000.

## Implementation on OpenClaw Host

1.  **Syslog Receiver**: Run a lightweight syslog server (or a simple Python listener) that writes incoming packets to a local rotating file.
2.  **Log Tailing**: The agent uses a tool to tail the most recent entries of this file, filtering for "Critical", "Alert", and "Emergency" levels.
