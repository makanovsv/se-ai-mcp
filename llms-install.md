# Installing SE AI (for AI agents such as Cline)

SE AI is a hosted remote MCP server. Do not clone or build anything.

1. Add a remote server named `se-ai`:
   - URL: `https://api.serviceengineer.academy/mcp`
   - Transport: streamable HTTP
2. On first use the client opens an OAuth sign-in page (OAuth 2.1, PKCE S256, dynamic client registration, scope `se_ai`). The user signs in or creates a free SE AI account there. No API key is needed.
3. Verify by calling `search_parts` with `{"query": "flow sensor", "equipment": "Aisys"}`. It is read-only and free.

Cline `cline_mcp_settings.json` example:
```json
{
  "mcpServers": {
    "se-ai": {
      "type": "streamableHttp",
      "url": "https://api.serviceengineer.academy/mcp"
    }
  }
}
```
