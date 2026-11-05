# Setup AgentShield GitHub Action

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Setup%20AgentShield-blue?logo=github&style=for-the-badge)](https://github.com/marketplace/actions/setup-agentshield)
[![npm version](https://img.shields.io/npm/v/@ritualdev-lab/agentshield.svg?style=for-the-badge&color=00F59B)](https://www.npmjs.com/package/@ritualdev-lab/agentshield)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![SOC 2 / DPDP Compliant](https://img.shields.io/badge/Security-Air--Gapped%20Zero--Leak-00F59B?style=for-the-badge)](https://ritualdev.in/trust)

Enterprise-grade Zero-Leak Secret Defense & Sandbox GitHub Action for Autonomous AI Coding Agents (Claude Code, Cursor, Windsurf, Aider, OpenHands).

---

## 🚀 Quickstart

Add `RitualDev-Lab/setup-agentshield` to your GitHub Actions workflow:

```yaml
name: AI Agent PR Security Gate

on:
  pull_request:
    branches: [main, master]
  push:
    branches: [main, master]

jobs:
  agent-shield-check:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Setup AgentShield Defense
        uses: RitualDev-Lab/setup-agentshield@v1
        with:
          version: 'latest'
          air-gapped: 'true'
          check-leaks: 'true'
```

---

## ⚙️ Inputs

| Input | Description | Required | Default |
| :--- | :--- | :---: | :---: |
| `version` | Package version of `@ritualdev-lab/agentshield` to install | No | `latest` |
| `air-gapped` | Force 100% offline isolation (`AGENTSHIELD_AIR_GAPPED=1`), blocking all external network requests | No | `true` |
| `strict-level` | Enforcement mode (`audit`, `redact`, `terminate`) | No | `redact` |
| `check-leaks` | Automatically execute `agentshield ci --enforce` and fail the build if unmasked secrets are committed | No | `false` |

---

## 📤 Outputs

| Output | Description |
| :--- | :--- |
| `agentshield-version` | The resolved semantic version of AgentShield installed on the CI runner. |
| `scan-status` | Result of the automated workspace leak check (`passed`, `failed`, or `skipped`). |

---

## 🛡️ Autonomous Agent Sandboxing Workflow

If your CI pipeline runs automated AI code generation agents (e.g., Aider, Claude Code, auto-fix bots):

```yaml
jobs:
  run-ai-coder:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup AgentShield
        uses: RitualDev-Lab/setup-agentshield@v1

      - name: Execute Autonomous Agent Under Sandbox
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: |
          # AgentShield wraps the agent execution, intercepting any attempt
          # to dump /proc/self/environ, echo raw tokens, or exfiltrate .env
          agentshield wrap --strict -- npx aider --message "Refactor auth controller"
```

---

## 🏛️ Enterprise Trust & Compliance

AgentShield is architected for defense-in-depth and compliance:
- **Zero Cloud Exfiltration**: Runs 100% locally with `AGENTSHIELD_AIR_GAPPED=1`.
- **Statutory Alignment**: Pre-built controls for **India DPDP Act 2023**, **EU GDPR Article 32**, and **SOC 2 Type II**.
- **Interactive Playground**: Test evasion vectors live in the browser at [ritualdev.in/playground](https://ritualdev.in/playground).
- **Vendor Assessment Packet**: View SIG Lite controls and architecture whitepaper at [ritualdev.in/trust](https://ritualdev.in/trust).

---

## 📄 License

MIT © [RitualDev Studio](https://ritualdev.in)
