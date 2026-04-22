# SentinelClaw Roadmap

Future development milestones for the project.

## Phase 1: Foundation (Current)
- [x] OpenWrt Flashed & Hardened.
- [x] External storage (`/opt`) setup.
- [x] Log pipeline blueprint created.
- [x] Tiered LLM Strategy defined.

## Phase 2: Implementation (Next)
- [ ] Implement `firewall_ssh_exec` Skill for OpenClaw.
- [ ] Set up `syslog-ng` streaming from Linksys to OpenClaw Host.
- [ ] Create the "Sentry" loop on Lemonade Server (Llama 3).
- [ ] Deploy first "Daily Intelligence Digest."

## Phase 3: Advanced Hunting
- [ ] **External Intelligence**: Integrate AlienVault OTX or VirusTotal APIs for IP/URL reputation.
- [ ] **Dynamic Throttling**: Automatically adjust SQM priority for devices showing suspicious but non-critical behavior.
- [ ] **User Feedback Loop**: Allow the user to say "This device is a guest" and have the agent automatically adjust its behavioral profile.

## Phase 4: Multi-Node
- [ ] Support for multiple routers (e.g., managing a secondary AP).
- [ ] Integration with Home Assistant for physical presence detection (e.g., "Nobody is home, increase firewall sensitivity").
