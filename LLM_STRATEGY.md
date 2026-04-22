# LLM Strategy: Tiered Intelligence

SentinelClaw uses a hybrid LLM approach to balance privacy, cost, and high-level reasoning.

## Tier 1: Local Intelligence (Lemonade Server)
**Model**: Llama 3 (8B/70B) or Mistral.
**Role**: The "Sentry."
- **Task**: Continuous log parsing and noise reduction.
- **Reason**: High-volume log data is kept local (privacy). It identifies patterns (e.g., "IP X attempted login 50 times") without incurring per-token costs.
- **Action**: Generates "Signal Summaries" for the Tier 2 model.

## Tier 2: Cloud Intelligence (OpenRouter - Claude 3.5 Sonnet)
**Model**: Claude 3.5 Sonnet (via OpenRouter).
**Role**: The "Architect."
- **Task**: Incident response, complex threat hunting, and user communication.
- **Reason**: Superior reasoning capabilities for "connecting the dots" (e.g., "This blocked DNS query matches the traffic spike seen in darkstat, indicating a potential beacon").
- **Action**: Issues commands to the router via SSH and sends URGENT alerts to the user.

## Alternative: ChatGPT OAuth
- Can be used as a fallback for Tier 2 if OpenRouter is unreachable.
- Provides a familiar interface for the user to "chat" with the firewall via OpenClaw.
