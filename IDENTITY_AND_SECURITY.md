# Identity & Secret Management

SentinelClaw requires specific credentials to manage the UTM. These must be handled according to the Principle of Least Privilege.

## 1. Agent SSH Identity
- **Key Type**: ED25519.
- **Location**: The private key is stored securely on the OpenClaw Host; the public key is in `/etc/dropbear/authorized_keys` on the router.
- **Rotation**: Keys should be rotated every 90 days.

## 2. GitHub PAT (Personal Access Token)
- **Scope**: Restricted to `repo` and `workflow`.
- **Storage**: NEVER hardcode the PAT in agent prompts or scripts. Use environment variables or an OpenClaw-managed vault.

## 3. Least Privilege (Future Implementation)
Currently, the agent uses the `root` account.
- **Goal**: Create a limited user `sentinel` on OpenWrt that only has sudo access to `uci`, `nft`, and `logread`.

## 4. Model Privacy
- **Rule**: Tier 1 (Lemonade Local) processes raw, unredacted logs.
- **Rule**: Tier 2 (OpenRouter Cloud) MUST receive redacted logs where possible (e.g., masking the middle octets of internal IPs) unless deep investigation is required.
