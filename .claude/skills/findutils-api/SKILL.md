---
name: findutils-api
description: FindUtils Tool API and MCP Server integration for Claude Code. Use when calling FindUtils tools via HTTP API, setting up the MCP server in Claude Desktop or Claude Code CLI, generating API client code, or testing endpoints. Triggers on: findutils API, MCP server, tool API, findutils-tool-api, findutils-mcp.
---

# FindUtils API & MCP Server

52 free utility tools available as a REST API and MCP server. No auth. No signup.

**Tool API:** `https://findutils-tool-api.codewitholgun.workers.dev/api`
**MCP Server:** `https://findutils-mcp.codewitholgun.workers.dev/`
**Docs:** `https://findutils.com/en/api/`
**OpenAPI spec:** `https://findutils-tool-api.codewitholgun.workers.dev/api/openapi.json`

---

## MCP Setup (Recommended)

Add FindUtils tools directly to Claude in one step.

### Claude Desktop

Edit `~/.claude/claude_desktop_config.json` (macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "findutils": {
      "url": "https://findutils-mcp.codewitholgun.workers.dev/"
    }
  }
}
```

Restart Claude Desktop. All FindUtils tools are now available in the tools panel.

### Claude Code CLI

```bash
claude mcp add findutils --transport http https://findutils-mcp.codewitholgun.workers.dev/
```

---

## REST API Quick Start

```bash
# List all tools
curl https://findutils-tool-api.codewitholgun.workers.dev/api/tools

# Get tool schema
curl https://findutils-tool-api.codewitholgun.workers.dev/api/tools/hash_generate

# Execute a tool
curl -X POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/hash_generate/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "hello world", "algorithm": "SHA-256"}'
```

---

## Available Tools

### Encoding / Crypto

| Tool ID | Description | Key Params |
|---|---|---|
| `base64_encode` | Encode text to Base64 | `text` |
| `base64_decode` | Decode Base64 to plain text | `text` |
| `url_encode` | Percent-encode for URLs | `text` |
| `url_decode` | Decode percent-encoded string | `text` |
| `hash_generate` | MD5, SHA-1, SHA-256, SHA-512 | `text`, `algorithm` |
| `hmac_generate` | HMAC-SHA-256/512 signature | `message`, `secret`, `algorithm` |
| `jwt_decode` | Decode JWT header/payload | `token` |
| `string_escape` | Escape/unescape JSON, HTML, URL, regex | `text`, `format`, `mode` |

### Generators

| Tool ID | Description | Key Params |
|---|---|---|
| `uuid_generate` | Generate UUID v4 | `count` |
| `password_generate` | Secure random password | `length`, `uppercase`, `lowercase`, `numbers`, `symbols`, `count` |
| `random_number` | Random integer or float | `min`, `max`, `count`, `float`, `decimals` |
| `random_string` | Random string from charset | `length`, `count`, `charset`, `custom` |
| `lorem_ipsum_generate` | Lorem ipsum placeholder text | `type`, `count` |
| `slug_generate` | URL-friendly slug from text | `text`, `separator` |
| `qr_text` | QR code as ASCII art | `text` |

### Text Manipulation

| Tool ID | Description | Key Params |
|---|---|---|
| `case_convert` | camelCase, snake_case, kebab-case, etc. | `text`, `to` |
| `word_count` | Words, chars, sentences, reading time | `text` |
| `text_reverse` | Reverse chars, words, or lines | `text`, `mode` |
| `text_truncate` | Truncate with suffix | `text`, `length`, `suffix`, `word_boundary` |
| `text_repeat` | Repeat string N times | `text`, `times`, `separator` |
| `whitespace_clean` | Trim, collapse spaces, normalize newlines | `text`, `trim`, `collapse_spaces`, `remove_blank_lines` |
| `line_sort` | Sort lines alpha, numeric, or by length | `text`, `order`, `mode`, `case_sensitive` |
| `line_dedupe` | Remove duplicate lines | `text`, `case_sensitive`, `trim_lines` |
| `regex_test` | Test regex, return all matches + groups | `pattern`, `input`, `flags` |

### Data Conversion

| Tool ID | Description | Key Params |
|---|---|---|
| `csv_to_json` | CSV text to JSON array | `csv`, `delimiter` |
| `json_to_csv` | JSON array to CSV text | `json`, `delimiter` |
| `markdown_to_html` | Markdown to HTML | `markdown` |
| `html_strip` | Strip HTML tags to plain text | `html` |
| `xml_to_json` | XML document to JSON | `xml` |
| `yaml_to_json` | YAML to JSON | `yaml` |
| `json_format` | Pretty-print JSON | `json`, `indent` |
| `json_validate` | Validate JSON | `json` |
| `json_flatten` | Nested JSON to dot-notation | `json`, `separator` |
| `json_unflatten` | Flat dot-notation to nested JSON | `json`, `separator` |
| `json_query` | Query JSON with dot-notation path | `json`, `path` |

### Number / Unit Conversion

| Tool ID | Description | Key Params |
|---|---|---|
| `unit_convert` | Length, weight, temp, volume, area, speed | `value`, `from`, `to` |
| `color_convert` | HEX, RGB, HSL, HSV | `color`, `from`, `to` |
| `number_base_convert` | Binary, octal, decimal, hex | `value`, `from`, `to` |
| `percentage_calculate` | % of, what %, % change | `mode`, `a`, `b` |
| `morse_code` | Text to/from Morse code | `text`, `mode` |
| `roman_numeral` | Arabic to/from Roman numerals | `input`, `mode` |

### Date / Time

| Tool ID | Description | Key Params |
|---|---|---|
| `unix_timestamp_convert` | Unix timestamp to/from date | `mode`, `value`, `timezone` |
| `date_difference` | Difference between two dates | `start`, `end` |
| `cron_describe` | Cron expression to plain English | `expression` |

### Validation

| Tool ID | Description | Key Params |
|---|---|---|
| `ip_validate` | Validate IPv4/IPv6 | `ip` |
| `email_validate` | Validate email format | `email` |
| `credit_card_validate` | Luhn check + card type | `number` |

### Developer / Networking

| Tool ID | Description | Key Params |
|---|---|---|
| `chmod_calculate` | Octal <-> symbolic chmod | `input` |
| `cidr_calculate` | CIDR block details | `cidr` |

### Calculators

| Tool ID | Description | Key Params |
|---|---|---|
| `bmi_calculate` | BMI from height and weight | `weight`, `height`, `unit` |
| `tip_calculate` | Tip + split bill calculator | `bill`, `tip_percent`, `people` |
| `aspect_ratio` | Aspect ratio or scaled dimensions | `width`, `height`, `new_width`, `new_height` |

---

## Code Examples

### JavaScript / TypeScript

```typescript
const BASE = 'https://findutils-tool-api.codewitholgun.workers.dev/api';

async function findutils(toolId: string, params: Record<string, unknown>) {
  const res = await fetch(`${BASE}/tools/${toolId}/execute`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(params),
  });
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

// Examples
await findutils('hash_generate', { text: 'hello', algorithm: 'SHA-256' });
await findutils('uuid_generate', { count: 5 });
await findutils('case_convert', { text: 'hello world', to: 'camel' });
await findutils('unit_convert', { value: 100, from: 'km', to: 'miles' });
await findutils('csv_to_json', { csv: 'name,age\nAlice,30\nBob,25' });
```

### Python

```python
import requests

BASE = 'https://findutils-tool-api.codewitholgun.workers.dev/api'

def findutils(tool_id: str, params: dict):
    r = requests.post(f'{BASE}/tools/{tool_id}/execute', json=params, timeout=30)
    r.raise_for_status()
    return r.json()

# Examples
print(findutils('hash_generate', {'text': 'hello', 'algorithm': 'SHA-256'}))
print(findutils('uuid_generate', {'count': 3}))
print(findutils('unit_convert', {'value': 72, 'from': 'F', 'to': 'C'}))
print(findutils('json_flatten', {'json': '{"a":{"b":{"c":1}}}'}))
```

### Go

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io"
    "net/http"
)

func findutils(toolID string, params map[string]any) (map[string]any, error) {
    body, _ := json.Marshal(params)
    resp, err := http.Post(
        "https://findutils-tool-api.codewitholgun.workers.dev/api/tools/"+toolID+"/execute",
        "application/json",
        bytes.NewReader(body),
    )
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()
    data, _ := io.ReadAll(resp.Body)
    var result map[string]any
    json.Unmarshal(data, &result)
    return result, nil
}

func main() {
    result, _ := findutils("hash_generate", map[string]any{
        "text": "hello", "algorithm": "SHA-256",
    })
    fmt.Println(result)
}
```

### curl

```bash
# Hash
curl -sX POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/hash_generate/execute \
  -H "Content-Type: application/json" -d '{"text":"hello","algorithm":"SHA-256"}'

# UUID
curl -sX POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/uuid_generate/execute \
  -H "Content-Type: application/json" -d '{"count":5}'

# Case convert
curl -sX POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/case_convert/execute \
  -H "Content-Type: application/json" -d '{"text":"hello world","to":"camel"}'

# Unit convert
curl -sX POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/unit_convert/execute \
  -H "Content-Type: application/json" -d '{"value":100,"from":"km","to":"miles"}'

# CSV to JSON
curl -sX POST https://findutils-tool-api.codewitholgun.workers.dev/api/tools/csv_to_json/execute \
  -H "Content-Type: application/json" -d '{"csv":"name,age\nAlice,30"}'
```

---

## MCP Protocol (Direct Usage)

Transport: Streamable HTTP — POST JSON-RPC 2.0 to the root URL.

```bash
# 1. Initialize (required first call)
curl -sX POST https://findutils-mcp.codewitholgun.workers.dev/ \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2024-11-05","capabilities":{},"clientInfo":{"name":"my-app","version":"1.0"}}}'

# 2. List tools
curl -sX POST https://findutils-mcp.codewitholgun.workers.dev/ \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}'

# 3. Call a tool
curl -sX POST https://findutils-mcp.codewitholgun.workers.dev/ \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"uuid_generate","arguments":{"count":3}}}'
```

Tool results are returned as MCP content objects:

```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "result": {
    "content": [{"type": "text", "text": "{\"uuids\":[...]}"}]
  }
}
```

Batch up to 50 calls in one request by passing a JSON array.

---

## Rate Limits

| Surface | Per Minute | Per IP/Day | Global/Day |
|---|---|---|---|
| Tool API | 60 req | 500 req | 50,000 req |
| MCP Server | 120 req | 1,000 req | 100,000 req |

HTTP 429 is returned when limits are exceeded. No API keys required.

---

## Error Reference

### HTTP Status Codes

| Code | Meaning |
|---|---|
| 200 | Success |
| 400 | Bad request (malformed JSON, missing required params) |
| 404 | Tool not found |
| 413 | Payload too large (max 1MB) |
| 429 | Rate limit exceeded |

### MCP JSON-RPC Error Codes

| Code | Meaning |
|---|---|
| -32700 | Parse error (invalid JSON) |
| -32600 | Invalid request (bad envelope) |
| -32601 | Method or tool not found |
| -32602 | Invalid params (missing required field or wrong type) |
| -32603 | Internal error |

---

## Key Parameter Values

**`case_convert` to:** `camel`, `pascal`, `snake`, `kebab`, `screaming_snake`, `title`, `sentence`, `lower`, `upper`

**`hash_generate` algorithm:** `MD5`, `SHA-1`, `SHA-256`, `SHA-512`

**`hmac_generate` algorithm:** `SHA-256`, `SHA-512`

**`color_convert` from/to:** `hex`, `rgb`, `hsl`, `hsv`

**`unit_convert` examples:** `km`/`miles`, `kg`/`lbs`, `C`/`F`, `L`/`gal`, `m/s`/`mph`

**`unix_timestamp_convert` mode:** `to_date`, `to_timestamp`, `now`

**`percentage_calculate` mode:** `percent_of`, `what_percent`, `percent_change`

**`morse_code` mode:** `encode`, `decode`

**`roman_numeral` mode:** `to_roman`, `to_arabic`, `auto`

**`string_escape` format:** `json`, `html`, `url`, `regex` — **mode:** `escape`, `unescape`

**`random_string` charset:** `alphanumeric`, `alphabetic`, `numeric`, `hex`, `custom`

**`text_reverse` mode:** `chars`, `words`, `lines`

**`line_sort` mode:** `alpha`, `numeric`, `length`

**`bmi_calculate` unit:** `metric` (kg/cm), `imperial` (lbs/inches)

---

## Self-Hosting

The MCP server is open source. Deploy your own instance to Cloudflare Workers:

```bash
git clone https://github.com/olgunozoktas/findutils-mcp.git
cd findutils-mcp
npm install
npx wrangler deploy
```

Requires a Cloudflare account (free tier is sufficient).

---

## Links

- Site: https://findutils.com
- API docs: https://findutils.com/en/api/
- MCP source: https://github.com/olgunozoktas/findutils-mcp
- Tool mirror: https://github.com/olgunozoktas/findutils-tools
