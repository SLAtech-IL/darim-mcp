<img src="icon.png" alt="Дарим" width="96" align="right">

# Darim MCP server

Remote [Model Context Protocol](https://modelcontextprotocol.io) server for
[Дарим](https://www.darim.ai/) (darim.ai), a service for group greeting cards
in Russian. Colleagues or friends each add a greeting, a photo or a voice
message, and the card opens for the recipient on a set date.

With this server an AI assistant can start such a card in the middle of a
conversation and give back the link to send to the group.

```
https://api.darim.ai/mcp
```

Streamable HTTP. No account, no API key, no sign-in.

This repository holds the description of the server, not its code. The server
itself runs at the address above.

## Tools

| Tool | What it does | Changes data |
|---|---|---|
| `list_occasions` | Lists the supported occasions (birthday, anniversary, retirement, a colleague leaving or going on maternity leave and others) with the value to pass on | no |
| `suggest_prompts` | Suggests ready questions that help participants write, for an occasion, optionally with the recipient's name filled in | no |
| `create_board` | Creates the card and returns the invite link for participants | yes |
| `board_status` | Shows how many people have signed, when collection closes and when the card opens | no |

`create_board` requires the organiser's email address: the links for managing
the card are sent there. The assistant is told to ask for it and never to
invent one.

## Try it

```
Сделай общую открытку для Ольги на выход на пенсию 1 марта, моя почта you@example.com
```
```
Какие вопросы задать коллегам для открытки на проводы Ольги?
```
```
Как там открытка? Вот ссылка: https://www.darim.ai/m/...
```

## Connect

**Claude** (claude.ai or the desktop app): Settings, Connectors, Add custom
connector, then paste `https://api.darim.ai/mcp`.

**Claude Code**

```
claude mcp add --transport http darim https://api.darim.ai/mcp
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "darim": { "url": "https://api.darim.ai/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "darim": { "type": "http", "url": "https://api.darim.ai/mcp" }
  }
}
```

Any other client that speaks streamable HTTP takes the same address.

## Data

The server stores the recipient's name and the organiser's email. Email is
sent through Amazon SES. No payment data, no credentials. Nothing is sent to
the card's recipient by the server.

- For assistants: https://www.darim.ai/dlya-assistentov/
- Privacy: https://www.darim.ai/privacy/
- Terms: https://www.darim.ai/usloviya/
- Support: https://www.darim.ai/podderzhka/

## Registry

Published in the official MCP Registry as `ai.darim/darim`; `server.json` here
is the manifest sent there. The Hebrew sister service is
[yahad-mcp](https://github.com/SLAtech-IL/yahad-mcp).

Made by SLATECH LTD.
