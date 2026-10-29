# Holdsport/SportMember API MCP server

Holdsport/SportMember API is available as a hosted [Model Context Protocol](https://modelcontextprotocol.io) (MCP)
server, so AI agents such as Claude, ChatGPT, Cursor and VS Code can call it as tools.

| | |
| --- | --- |
| Server URL | `https://app.getelva.ai/mcp/elvademo/holdsportsportmember-api` |
| Install page | https://app.getelva.ai/mcp/elvademo/holdsportsportmember-api/install |
| Tools | 8, one per operation in [`openapi.yml`](openapi.yml) |
| Calls | `https://api.holdsport.dk/v1` |
| Authentication | None, the API is public. |

## Install

**[Open the install page](https://app.getelva.ai/mcp/elvademo/holdsportsportmember-api/install)** for step-by-step setup in Claude, ChatGPT,
Cursor, VS Code and other clients, or use one of the options below.

[![Install in Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=Holdsport%2FSportMember%20API&config=eyJ1cmwiOiJodHRwczovL2FwcC5nZXRlbHZhLmFpL21jcC9lbHZhZGVtby9ob2xkc3BvcnRzcG9ydG1lbWJlci1hcGkifQ%3D%3D)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_MCP-0098FF?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=holdsportsportmember-api&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapp.getelva.ai%2Fmcp%2Felvademo%2Fholdsportsportmember-api%22%7D)

### Claude Code

```bash
claude mcp add --transport http holdsportsportmember-api https://app.getelva.ai/mcp/elvademo/holdsportsportmember-api
```

### Claude (claude.ai and Claude Desktop)

Settings → Connectors → **Add custom connector**, then paste the server URL.

### ChatGPT

Settings → Apps & Connectors → Advanced settings → turn on **Developer mode**, then
**Create** a connector and paste the server URL.

### Any other MCP client

```json
{
  "mcpServers": {
    "holdsportsportmember-api": {
      "url": "https://app.getelva.ai/mcp/elvademo/holdsportsportmember-api"
    }
  }
}
```

---

Generated from this repository's OpenAPI spec and hosted by [Elva](https://getelva.ai?utm_source=github&utm_medium=Holdsport/holdsport-api&utm_campaign=githubprs).
