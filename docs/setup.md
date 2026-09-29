# Connecting the TrackIQ Amazon MCP

One server, `https://trackiq.com/mcp`, connected the way your assistant
expects. You need a TrackIQ account ($69/month) and the Amazon account you
want to read. Authorisation runs through Amazon's own OAuth — TrackIQ never
sees your password.

## Claude Code

```bash
claude mcp add trackiq "https://trackiq.com/mcp"
claude mcp list          # trackiq · connected
```

Then ask it something. The first call opens the Amazon authorisation flow.

## Claude desktop

The same command registers it; restart Claude desktop afterwards. To edit the
config by hand instead, add the server under `mcpServers` in
`claude_desktop_config.json` — **Settings → Developer → Edit Config** opens
the file.

## Claude.ai

**Settings → Connectors → Add custom connector**, then paste
`https://trackiq.com/mcp` and authorise.

## ChatGPT

Add it as a connector in **Settings → Connectors**, using the same URL. You
need a plan that allows custom connectors.

## Cursor

Add the server to `~/.cursor/mcp.json`, or use **Settings → MCP → Add new
global MCP server**, with the same URL.

## Checking it works

Ask for something small and verifiable:

```
List the Amazon marketplaces I can read.
```

You should get your account and marketplace back. If the assistant answers
from general knowledge instead of calling a tool, the server is not connected
— check `claude mcp list`, or the connector's status in the client.

## Then what

Install the skills so the assistant knows what to do with the data:

```
/plugin marketplace add TrackIQ-HQ/amazon-seller-skills
/plugin install trackiq-amazon-wasted-spend@trackiq
```

[The full catalog →](https://github.com/TrackIQ-HQ/amazon-seller-skills) ·
[What the tools return →](tools.md) ·
[Example questions →](examples.md)
