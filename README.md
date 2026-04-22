# SentinelClaw: Autonomous SOC & Firewall Agent

SentinelClaw is a specialized AI agent designed to run within the **OpenClaw** framework. It acts as a Senior Cybersecurity Engineer and Threat Hunter for the Linksys UTM (OpenWrt) environment.

## Vision

To move from a "reactive" firewall (static rules) to an "active" defense posture where an intelligent agent continuously observes, reasons, and adjusts the network security based on real-time data.

## Primary Roles

1.  **Cybersecurity Engineer**: Manages firewall rules, service health, and network configuration.
2.  **Threat Hunter**: Analyzes logs from CrowdSec, AdGuard Home, and nftables to find patterns of malicious intent.
3.  **SOC Analyst**: Filters noise and provides the human owner with high-signal alerts and periodic intelligence digests.

## Documentation Index

- [ARCHITECTURE.md](ARCHITECTURE.md): The technical data flow and integration points.
- [AGENT_PROMPT.md](AGENT_PROMPT.md): The system instructions and behavioral guidelines.
- [TOOL_DEFINITIONS.md](TOOL_DEFINITIONS.md): The "capabilities" the agent has on the router.
- [LOG_HANDLING.md](LOG_HANDLING.md): Setup for streaming logs from OpenWrt to the agent.
