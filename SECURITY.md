# Security Policy

## Supported Versions

| Version | Supported |
|---|---|
| 1.x | ✅ |
| < 1.0 (pre-release) | ❌ |

## Scope

Bubble Weather Pro is a **frontend dashboard module** (YAML/Lovelace templating) for Bubble Card. It does not run server-side code, does not make outbound network calls of its own, and does not handle credentials, tokens, or personal data beyond what Home Assistant's frontend already exposes to any Lovelace card.

Realistic security-relevant issues in scope include:

- Template injection or XSS-style issues arising from how the module renders entity state/attributes
- Logic that could cause unintended entity/service calls
- Supply-chain concerns in the module import URL or release process

Out of scope: vulnerabilities in Home Assistant core, Bubble Card itself, or third-party weather integrations — please report those upstream.

## Reporting a Vulnerability

Please **do not** open a public GitHub issue for security concerns.

Instead, use GitHub's [private vulnerability reporting](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/security/advisories/new) feature on this repository, or contact the maintainer directly via the email listed on their GitHub profile.

Please include:

- A description of the issue and potential impact
- Steps to reproduce (config snippet, HA/Bubble Card versions)
- Any suggested fix, if you have one

### What to expect

- Acknowledgement within **5 business days**
- An initial assessment within **14 days**
- Credit in the release notes for validated reports, unless you'd prefer to remain anonymous

Thank you for helping keep the project and its users safe.
