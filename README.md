# Syntari Nexus — Claude Code Plugin

Investment intelligence for PE deals, CRE underwriting, credit analysis, LP management, and financial modeling. Built by [Syntari International](https://syntari-ai.com).

## What's Included

### Commands (6)
| Command | Description |
|---------|-------------|
| `/nexus-quick-cut` | Generate 10-section Syntari credit memo |
| `/nexus-underwrite` | CRE underwriting from OM parsing to returns |
| `/nexus-screen` | 100-point PE/CRE deal scoring |
| `/nexus-model` | Wall Street-grade LBO/DCF/M&A/Comps |
| `/nexus-research` | Market intelligence + competitive analysis |
| `/nexus-debate` | AGI: Adversarial bull/bear/market thesis debate |

### Skills (17)
Core investment skills that auto-activate based on conversation context — credit memos, underwriting, deal screening, financial modeling, portfolio analysis, and 7 consulting frameworks (MBB + Big4).

### Agents (4)
| Agent | Team Composition |
|-------|-----------------|
| `deal-team` | Analyst + Risk Manager + Portfolio Manager |
| `cre-team` | Underwriter + Market Analyst + Asset Manager |
| `credit-team` | Credit Analyst + Trader + CLO Manager |
| `debate-team` | AGI: Bull + Bear + Market (FREE-MAD protocol) |

### AGI Capabilities
- **Confidence Calibration** (SteerConf) — three-pass calibrated confidence on all outputs
- **Adversarial Debate** (FREE-MAD) — heterogeneous multi-model debate (91% accuracy)
- **Self-Improving Feedback** — deal outcomes feed back into agent accuracy metrics

## Installation

### From Marketplace
```bash
claude plugin marketplace add Syntari-International-Inc/syntari-nexus-plugin
```

### From Local Directory
```bash
claude plugin add ./plugins/syntari-nexus
```

## Data Connections

### Inherited (from `financial-analysis` dependency)
This plugin depends on Anthropic's `financial-analysis` core plugin, which provides 11 data connectors:
- BigData.com, PitchBook, Chronograph, LSEG, Moody's, S&P Global/Kensho, FactSet, Aiera, Morningstar, MT Newswires, Egnyte

### Nexus MCP Server (Optional)
Connect to a running Nexus instance for platform data:

1. Get an API key from your Nexus admin (Settings > API Keys)
2. The plugin's `.mcp.json` points to `nexus.syntari-ai.com/api/mcp`
3. Authenticate via OAuth when prompted in Claude

**Without Nexus MCP**: All skills work standalone — provide data manually or use the inherited financial connectors.

## Configuration

### Environment Variables (for Nexus MCP)
```bash
NEXUS_API_URL=https://nexus.syntari-ai.com  # Your Nexus instance
NEXUS_API_KEY=nxs_live_...                   # API key from admin
```

## Architecture

```
Plugin (Claude Code)  →  Nexus MCP Server (HTTPS)  →  Nexus Platform
     Skills                 12 tools                     PostgreSQL
     Commands               5 resources                  Qdrant (vector)
     Agents                 OAuth 2.0                    Neptune (graph)
     Hooks                  Tenant isolation             Redis (cache)
```

## License

MIT — see [LICENSE](../../LICENSE)
