# FindUtils Tools

315+ free online tools at [findutils.com](https://findutils.com) -- calculators, converters, generators, developer utilities, and more. All tools run in your browser with no data uploaded to any server.

## For AI / LLM Integration

### MCP Server

Connect 52 tools directly to Claude, Cursor, Windsurf, ChatGPT, and any MCP-compatible client.

**Claude Desktop / Claude Code:**

Add to your MCP config (`~/.claude/claude_desktop_config.json` or `~/.claude.json`):

```json
{
  "mcpServers": {
    "findutils": {
      "url": "https://mcp.findutils.com/"
    }
  }
}
```

**Any MCP Client (Streamable HTTP):**

```
MCP Server URL: https://mcp.findutils.com/
```

**52 MCP Tools:** Base64, URL Encode/Decode, UUID, Hash (MD5/SHA), HMAC, JSON Format/Validate/Flatten/Unflatten/Query, Percentage, Unit Convert, Color Convert, Unix Timestamp, Number Base, Case Convert, Word Count, Lorem Ipsum, JWT Decode, Regex Test, Date Diff, CSV to JSON, JSON to CSV, XML to JSON, YAML to JSON, Markdown to HTML, HTML Strip, Slug Generate, IP Validate, Email Validate, Credit Card Validate, Password Generate, Random Number/String, Text Reverse/Truncate/Repeat, String Escape, Whitespace Clean, Line Sort/Dedupe, Cron Describe, Chmod Calculate, CIDR Calculate, Morse Code, Roman Numeral, BMI Calculate, Tip Calculate, Aspect Ratio, QR Text.

### REST API

50 tools available as HTTP endpoints. No authentication required.

**Base URL:** `https://api.findutils.com`

**Example:**

```bash
# Encode text to Base64
curl -X POST https://api.findutils.com/api/tools/base64/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello, World!", "action": "encode"}'

# Generate a UUID
curl -X POST https://api.findutils.com/api/tools/uuid/execute \
  -H "Content-Type: application/json" -d '{}'

# SHA-256 hash
curl -X POST https://api.findutils.com/api/tools/hash/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "hello world", "algorithm": "sha-256"}'
```

**Response format:**

```json
{
  "success": true,
  "result": { "result": "SGVsbG8sIFdvcmxkIQ==" },
  "meta": { "tool": "base64", "executionMs": 0 }
}
```

**Endpoint pattern:** `POST /api/tools/{tool-id}/execute`

Full API documentation: [findutils.com/en/api](https://findutils.com/en/api/)

### Claude Code Skill

This repo includes a Claude Code skill at `.claude/skills/findutils-api/SKILL.md`. When cloned, Claude Code automatically picks it up and can help you:
- Call any of the 50 API tools from your code
- Set up the MCP server connection
- Generate API client code in TypeScript, Python, Go, or curl
- Test endpoints interactively

### llms.txt

Machine-readable content for AI systems:
- Site overview (315+ tools): [findutils.com/llms.txt](https://findutils.com/llms.txt)
- API reference (50 tools): [findutils.com/api/llms.txt](https://findutils.com/api/llms.txt)
- OpenAPI 3.1 spec: [findutils.com/api/openapi.json](https://findutils.com/api/openapi.json)

## WVW (World Vibe Web)

This repo hosts `apps.json` for the [WVW distributed app store](https://wvw.dev). The file is auto-generated and synced from [findutils.com/apps.json](https://findutils.com/apps.json).

## Content

### [Guides](guides/) (85)

In-depth tutorials covering developer tools, security, design, PDF manipulation, financial calculators, and more. Each guide links back to the full interactive version on FindUtils.

### [Blog](blog/) (30)

Articles on developer productivity, free tool roundups, security best practices, financial planning, and technical deep-dives.

### [Cheatsheets](cheatsheets/) (25)

Quick-reference cards for Linux, Git, Docker, Kubernetes, JavaScript, Python, SQL, React, CSS, and more. Each cheatsheet links to the interactive, searchable version on FindUtils.

## Tool Categories

- **[Productivity](https://findutils.com/en?categories=productivity&persona=everyone)** -- PDF editor, timers, mind maps, spreadsheets
- **[Developer](https://findutils.com/en?categories=developer&persona=everyone)** -- JSON formatter, regex tester, JWT decoder, API tools
- **[Financial](https://findutils.com/en?categories=financial&persona=everyone)** -- Loan, mortgage, investment, tax calculators
- **[Converters](https://findutils.com/en?categories=converters&persona=everyone)** -- Image, video, audio, CSV, JSON, PDF format converters
- **[Security](https://findutils.com/en?categories=security&persona=everyone)** -- Password generator, hash tools, encryption, SSL checker
- **[Generators](https://findutils.com/en?categories=generators&persona=everyone)** -- QR codes, UUIDs, barcodes, lorem ipsum, signatures
- **[Text Tools](https://findutils.com/en?categories=text&persona=everyone)** -- Word counter, case converter, diff checker
- **[Design](https://findutils.com/en?categories=design&persona=everyone)** -- Color palettes, gradients, CSS generators, photo editors
- **[Calculators](https://findutils.com/en?categories=calculators&persona=everyone)** -- BMI, percentage, date, GPA, scientific, and more
- **[Mockups](https://findutils.com/en?categories=mockups&persona=everyone)** -- Device frames, browser mockups, screenshots

## Emoji Search

Fast emoji search engine at [emoji.findutils.com](https://emoji.findutils.com) -- search, browse, and copy emojis with instant results.

## Links

- Website: [findutils.com](https://findutils.com)
- GitHub Pages: [olgunozoktas.github.io/findutils-tools](https://olgunozoktas.github.io/findutils-tools/)
- Emoji Search: [emoji.findutils.com](https://emoji.findutils.com)
- Guides: [findutils.com/en/guides](https://findutils.com/en/guides/)
- Blog: [findutils.com/en/blog](https://findutils.com/en/blog/)
- Cheatsheets: [findutils.com/en/cheatsheets](https://findutils.com/en/cheatsheets/)
- MCP Server: [findutils.com/en/mcp](https://findutils.com/en/mcp/)
- API Docs: [findutils.com/en/api](https://findutils.com/en/api/)
