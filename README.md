# FindUtils Tools

316+ free online tools at [findutils.com](https://findutils.com) -- calculators, converters, generators, developer utilities, and more. All tools run in your browser with no data uploaded to any server.

## For AI / LLM Integration

### MCP Server

Connect 22 tools directly to Claude, Cursor, Windsurf, ChatGPT, and any MCP-compatible client.

**Claude Desktop / Claude Code:**

Add to your MCP config (`~/.claude/claude_desktop_config.json` or `~/.claude.json`):

```json
{
  "mcpServers": {
    "findutils": {
      "url": "https://findutils-mcp.codewitholgun.workers.dev/"
    }
  }
}
```

**Any MCP Client (Streamable HTTP):**

```
MCP Server URL: https://findutils-mcp.codewitholgun.workers.dev/
```

**Available MCP Tools:** Base64, URL Encode/Decode, UUID Generator, Hash Generator, HMAC Generator, JSON Formatter, JSON Validator, Percentage Calculator, Unit Converter, Color Converter, Unix Timestamp, Number Base Converter, Case Converter, Word Counter, Lorem Ipsum Generator, JWT Decoder, Regex Tester, Date Difference, CSV to JSON, JSON to CSV.

### REST API

20 tools available as HTTP endpoints. No authentication required.

**Base URL:** `https://findutils-tool-api.codewitholgun.workers.dev`

**Example:**

```bash
# Encode text to Base64
curl -X POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/base64/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello, World!", "action": "encode"}'

# Generate a UUID
curl -X POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/uuid/execute \
  -H "Content-Type: application/json" -d '{}'

# SHA-256 hash
curl -X POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/hash/execute \
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

### llms.txt

Machine-readable site overview for AI crawlers: [findutils.com/llms.txt](https://findutils.com/llms.txt)

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

- **Calculators** -- BMI, percentage, date, GPA, scientific, and more
- **Converters** -- Image, video, audio, CSV, JSON, PDF format converters
- **Design Tools** -- Color palettes, gradients, CSS generators, photo editors
- **Developer Tools** -- JSON formatter, regex tester, JWT decoder, API tools
- **Financial Tools** -- Loan, mortgage, investment, tax calculators
- **Generators** -- QR codes, UUIDs, barcodes, lorem ipsum, signatures
- **Productivity** -- PDF editor, timers, mind maps, spreadsheets
- **Security** -- Password generator, hash tools, encryption, SSL checker
- **Text Tools** -- Word counter, case converter, diff checker

## Links

- Website: [findutils.com](https://findutils.com)
- Guides: [findutils.com/en/guides](https://findutils.com/en/guides/)
- Blog: [findutils.com/en/blog](https://findutils.com/en/blog/)
- Cheatsheets: [findutils.com/en/cheatsheets](https://findutils.com/en/cheatsheets/)
- MCP Server: [findutils.com/en/mcp](https://findutils.com/en/mcp/)
- API Docs: [findutils.com/en/api](https://findutils.com/en/api/)
