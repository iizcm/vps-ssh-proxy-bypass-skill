---
name: vps-ssh-proxy-bypass
description: "Bypass ISP-level website blocking (crypto exchanges, X/Twitter, OpenSea, bridges) when VPN apps/extensions/Cloudflare-Warp/ProtonVPN all FAIL because the ISP uses DPI or whitelists only certain tunnels. Technique: turn the user's OWN VPS (which they already SSH into daily, so the ISP does NOT block it) into a local SOCKS proxy via an SSH dynamic tunnel, then point Windows/Edge proxy settings at 127.0.0.1:1080. Guaranteed to work when the VPS is reachable."
version: 1.0.0
author: Community
license: MIT
platforms: [linux, macos, windows]
tags: [general]
---

# Vps Ssh Proxy Bypass — Skill

Bypass ISP-level website blocking (crypto exchanges, X/Twitter, OpenSea, bridges) when VPN apps/extensions/Cloudflare-Warp/ProtonVPN all FAIL because the ISP uses DPI or whitelists only certain tunnels. Technique: turn the user's OWN VPS (which they already SSH into daily, so the ISP does NOT block it) into a local SOCKS proxy via an SSH dynamic tunnel, then point Windows/Edge proxy settings at 127.0.0.1:1080. Guaranteed to work when the VPS is reachable.

## Install

```bash
cp -r <skill-name> ~/.hermes/skills/<skill-path>/
```

Or clone this repository:

```bash
git clone https://github.com/iizcm/vps-ssh-proxy-bypass-skill.git ~/.hermes/skills/<skill-path>/
```

## Usage

Invoke your AI agent with a clear instruction matching this skill's purpose. The agent will route tasks to this skill when the instruction matches its description or trigger keywords.

Refer to `README.md` in this repository for:
- Detailed step-by-step installation guide
- Bilingual documentation (English + Indonesian)
- Troubleshooting table
- Security best practices
- Customization tips

## Safety rules

- Never commit private keys, seed phrases, API tokens, or personal data to version control
- Use placeholders (`<YOUR_...>`) in all examples and code snippets
- Validate all outputs before acting on them
- Keep real credentials in your runtime's secure credential store only
