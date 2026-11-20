# SE AI — MCP server for medical equipment troubleshooting

**SE AI (Service Engineer AI)** is a troubleshooting assistant for engineers who service medical equipment: ultrasound, anaesthesia machines and ventilators, patient monitors, X-ray, CT, MRI and lab analysers.

Describe the brand, model and symptom (or error code) in any language. SE AI searches manufacturer service manuals and repairs confirmed by engineers, names the likely cause and the checks in order, and labels every statement by its source: manual, confirmed field case, or unconfirmed colleague suggestion. When there is no direct answer it says so, and it never invents part numbers.

This repository documents the **hosted remote MCP server**. There is nothing to install or run locally.

| | |
|---|---|
| Endpoint | `https://api.serviceengineer.academy/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 with PKCE (S256) and dynamic client registration, scope `se_ai` |
| Registry name | `academy.serviceengineer/se-ai` ([official MCP registry](https://registry.modelcontextprotocol.io/v0/servers?search=academy.serviceengineer)) |
| Website | https://serviceengineer.academy/ai/ |
| Demo (45 s) | https://youtu.be/esLCSFoDp_A |

## Tools

| Tool | What it does | Counts toward limit |
|---|---|---|
| `ask_se_ai` | Ask about a fault: brand, model, symptom or error code. Returns the likely cause, checks in order, parts, the records relied on (`[K123]` refs with trust labels) and a `chat_id` to continue the conversation. May draft a work order and service report for the engineer to approve in the app. | Yes |
| `search_parts` | Search spare parts taken from manufacturers' illustrated parts lists (about 168,000 part lines, about 1,300 machines) by part number or by part name plus machine. Read-only. | No (free) |
| `list_cases` | The engineer's recent SE AI cases: work orders, status, suspected cause and parts drafts. Read-only. | No |

## Connect

You need a free SE AI account (sign up at https://serviceengineer.academy/ai/). 3 questions are free, then $12/month. `search_parts` is always free.

**Claude (claude.ai / Claude Desktop):** Settings → Connectors → Add custom connector → URL `https://api.serviceengineer.academy/mcp`, then sign in.

**Claude Code:**
```bash
claude mcp add --transport http se-ai https://api.serviceengineer.academy/mcp
```

**ChatGPT:** enable developer mode for connectors, then add a custom connector with URL `https://api.serviceengineer.academy/mcp` and OAuth. A listing in the ChatGPT app directory is in review.

**VS Code / Cursor / Cline / any client with remote MCP + OAuth:**
```json
{
  "mcpServers": {
    "se-ai": {
      "type": "streamable-http",
      "url": "https://api.serviceengineer.academy/mcp"
    }
  }
}
```

**Gemini CLI:** `gemini extensions install https://github.com/makanovsv/se-ai-mcp`

## Example

> Draeger Fabius GS: leak test fails, leakage around 400 ml/min. What should I check first?

SE AI answers: most likely a leak in the breathing system, not the electronics; then an ordered check list (circuit and Y-piece first, absorber and canister O-rings, vaporiser seating, valves and APL, pump intake filter), the source of each point, and "no confirmed parts, no catalogue numbers found" when that is the case.

## About

Built by Service Engineer Ltd (AIFC, Astana, Kazakhstan), the team behind [Service Engineer Academy](https://serviceengineer.academy). Contact: ceo@serviceengineer.app.

The service itself is proprietary; the documentation in this repository is MIT-licensed.
