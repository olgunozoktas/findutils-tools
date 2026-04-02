---
name: findutils-api
description: "FindUtils Tool API and MCP Server integration. Use when calling FindUtils tools via HTTP API, setting up MCP server connections in Claude Desktop or Claude Code CLI, generating API client code in any language, or testing endpoints. Triggers on: findutils API, MCP server, tool API, findutils-tool-api, findutils-mcp, findutils tools from code."
---

# FindUtils API & MCP Server Integration Skill

Use this skill when a developer wants to:
- Call FindUtils utility tools from their code via HTTP
- Connect Claude Desktop or Claude Code CLI to FindUtils via MCP
- Generate API client code in JavaScript, Python, Go, or curl
- Understand the protocol, rate limits, or error codes
- Test or debug endpoint calls

---

## Endpoints at a Glance

| Surface | URL | Auth |
|---|---|---|
| Tool API (REST) | `https://api.findutils.com/api` | None |
| MCP Server | `https://mcp.findutils.com/` | None |
| OpenAPI Spec | `https://api.findutils.com/api/openapi.json` | None |
| Health Check | `https://mcp.findutils.com/health` | None |

No API keys. No signup. Free to use.

---

## MCP Server Setup

### Claude Desktop

Add to `~/.claude/claude_desktop_config.json` (macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "findutils": {
      "url": "https://mcp.findutils.com/"
    }
  }
}
```

Restart Claude Desktop. FindUtils tools appear automatically in the tools menu.

### Claude Code CLI

```bash
claude mcp add findutils --transport http https://mcp.findutils.com/
```

Verify it was added:

```bash
claude mcp list
```

### Any MCP Client (Generic)

Transport: Streamable HTTP (POST to root URL)
Protocol: JSON-RPC 2.0

---

## REST API Usage

### List All Tools

```bash
curl https://api.findutils.com/api/tools
```

### Get Tool Schema

```bash
curl https://api.findutils.com/api/tools/hash_generate
```

### Execute a Tool

```bash
# POST /api/tools/:tool_id/execute
curl -X POST https://api.findutils.com/api/tools/hash_generate/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "hello world", "algorithm": "SHA-256"}'
```

### OpenAPI Spec

```bash
curl https://api.findutils.com/api/openapi.json
```

---

## Available Tools (52 total)

### Encoding / Crypto

| Tool ID | Description | Required Params |
|---|---|---|
| `base64_encode` | Encode text to Base64 | `text` |
| `base64_decode` | Decode Base64 to plain text | `text` |
| `url_encode` | Percent-encode for URLs | `text` |
| `url_decode` | Decode percent-encoded string | `text` |
| `hash_generate` | MD5, SHA-1, SHA-256, SHA-512 hash | `text`; opt: `algorithm` |
| `hmac_generate` | HMAC-SHA-256/512 signature | `message`, `secret`; opt: `algorithm` |
| `jwt_decode` | Decode JWT (no verification) | `token` |
| `string_escape` | Escape/unescape JSON, HTML, URL, regex | `text`, `format`; opt: `mode` |

### Generators

| Tool ID | Description | Required Params |
|---|---|---|
| `uuid_generate` | Generate UUID v4 | opt: `count` |
| `password_generate` | Cryptographically secure password | opt: `length`, `uppercase`, `lowercase`, `numbers`, `symbols`, `count` |
| `random_number` | Random integer or float in range | opt: `min`, `max`, `count`, `float`, `decimals` |
| `random_string` | Random string from charset | opt: `length`, `count`, `charset`, `custom` |
| `lorem_ipsum_generate` | Lorem ipsum placeholder text | opt: `type`, `count` |
| `slug_generate` | URL-friendly slug from text | `text`; opt: `separator` |
| `qr_text` | QR code as ASCII art | `text` |

### Text Manipulation

| Tool ID | Description | Required Params |
|---|---|---|
| `case_convert` | camelCase, snake_case, kebab-case, etc. | `text`, `to` |
| `word_count` | Words, chars, sentences, reading time | `text` |
| `text_reverse` | Reverse chars, words, or lines | `text`; opt: `mode` |
| `text_truncate` | Truncate with ellipsis | `text`; opt: `length`, `suffix`, `word_boundary` |
| `text_repeat` | Repeat string N times | `text`; opt: `times`, `separator` |
| `whitespace_clean` | Trim, collapse spaces, normalize newlines | `text`; opt: `trim`, `collapse_spaces`, `remove_blank_lines`, `normalize_newlines` |
| `line_sort` | Sort lines alpha, numeric, or by length | `text`; opt: `order`, `mode`, `case_sensitive` |
| `line_dedupe` | Remove duplicate lines | `text`; opt: `case_sensitive`, `trim_lines` |
| `regex_test` | Test regex, return all matches + groups | `pattern`, `input`; opt: `flags` |

### Data Conversion

| Tool ID | Description | Required Params |
|---|---|---|
| `csv_to_json` | CSV text to JSON array | `csv`; opt: `delimiter` |
| `json_to_csv` | JSON array to CSV text | `json`; opt: `delimiter` |
| `markdown_to_html` | Markdown to HTML | `markdown` |
| `html_strip` | Strip HTML tags to plain text | `html` |
| `xml_to_json` | XML document to JSON | `xml` |
| `yaml_to_json` | YAML to JSON | `yaml` |
| `json_format` | Pretty-print JSON | `json`; opt: `indent` |
| `json_validate` | Validate JSON and report errors | `json` |
| `json_flatten` | Nested JSON to dot-notation flat object | `json`; opt: `separator` |
| `json_unflatten` | Flat dot-notation object to nested JSON | `json`; opt: `separator` |
| `json_query` | Query JSON with dot-notation path | `json`, `path` |

### Number / Unit Conversion

| Tool ID | Description | Required Params |
|---|---|---|
| `unit_convert` | Length, weight, temp, volume, area, speed | `value`, `from`, `to` |
| `color_convert` | HEX, RGB, HSL, HSV conversion | `color`, `from`, `to` |
| `number_base_convert` | Binary, octal, decimal, hex | `value`, `from`, `to` |
| `percentage_calculate` | X% of Y, X is what % of Y, % change | `mode`, `a`, `b` |
| `morse_code` | Text to/from Morse code | `text`; opt: `mode` |
| `roman_numeral` | Arabic integers to/from Roman numerals | `input`; opt: `mode` |

### Date / Time

| Tool ID | Description | Required Params |
|---|---|---|
| `unix_timestamp_convert` | Unix timestamp to/from date | `mode`; opt: `value`, `timezone` |
| `date_difference` | Difference between two dates | `start`; opt: `end` |
| `cron_describe` | Cron expression to plain English | `expression` |

### Validation

| Tool ID | Description | Required Params |
|---|---|---|
| `ip_validate` | Validate IPv4/IPv6 address | `ip` |
| `email_validate` | Validate email format | `email` |
| `credit_card_validate` | Luhn check + card type detection | `number` |

### Developer / Networking

| Tool ID | Description | Required Params |
|---|---|---|
| `chmod_calculate` | Octal <-> symbolic chmod notation | `input` |
| `cidr_calculate` | CIDR block details (range, hosts, broadcast) | `cidr` |

### Calculators

| Tool ID | Description | Required Params |
|---|---|---|
| `bmi_calculate` | BMI from height and weight | `weight`, `height`; opt: `unit` |
| `tip_calculate` | Tip, total, and per-person split | `bill`; opt: `tip_percent`, `people` |
| `aspect_ratio` | Aspect ratio or scaled dimensions | `width`, `height`; opt: `new_width`, `new_height` |

---

## Code Generation Templates

### JavaScript / TypeScript (fetch)

```typescript
const API_BASE = 'https://api.findutils.com/api';

async function executeTool<T = unknown>(toolId: string, params: Record<string, unknown>): Promise<T> {
  const res = await fetch(`${API_BASE}/tools/${toolId}/execute`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(params),
  });

  if (!res.ok) {
    const err = await res.json().catch(() => ({}));
    throw new Error(`FindUtils API error ${res.status}: ${JSON.stringify(err)}`);
  }

  return res.json() as Promise<T>;
}

// Usage examples
const hash = await executeTool('hash_generate', { text: 'hello', algorithm: 'SHA-256' });
const uuid = await executeTool('uuid_generate', { count: 5 });
const slug = await executeTool('slug_generate', { text: 'Hello World!' });
const caseResult = await executeTool('case_convert', { text: 'hello world', to: 'camel' });
```

### Python (requests)

```python
import requests
from typing import Any

API_BASE = 'https://api.findutils.com/api'

def execute_tool(tool_id: str, params: dict) -> Any:
    resp = requests.post(
        f'{API_BASE}/tools/{tool_id}/execute',
        json=params,
        timeout=30
    )
    resp.raise_for_status()
    return resp.json()

# Usage examples
result = execute_tool('hash_generate', {'text': 'hello', 'algorithm': 'SHA-256'})
print(result)

uuids = execute_tool('uuid_generate', {'count': 5})
print(uuids)

converted = execute_tool('unit_convert', {'value': 100, 'from': 'km', 'to': 'miles'})
print(converted)
```

### Go (net/http)

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io"
    "net/http"
)

const apiBase = "https://api.findutils.com/api"

func executeTool(toolID string, params map[string]any) (map[string]any, error) {
    body, err := json.Marshal(params)
    if err != nil {
        return nil, err
    }

    resp, err := http.Post(
        fmt.Sprintf("%s/tools/%s/execute", apiBase, toolID),
        "application/json",
        bytes.NewReader(body),
    )
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()

    data, err := io.ReadAll(resp.Body)
    if err != nil {
        return nil, err
    }

    if resp.StatusCode != 200 {
        return nil, fmt.Errorf("API error %d: %s", resp.StatusCode, data)
    }

    var result map[string]any
    if err := json.Unmarshal(data, &result); err != nil {
        return nil, err
    }
    return result, nil
}

func main() {
    result, err := executeTool("hash_generate", map[string]any{
        "text":      "hello world",
        "algorithm": "SHA-256",
    })
    if err != nil {
        panic(err)
    }
    fmt.Println(result)
}
```

### curl

```bash
# Base64 encode
curl -s -X POST https://api.findutils.com/api/tools/base64_encode/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello, World!"}'

# Hash
curl -s -X POST https://api.findutils.com/api/tools/hash_generate/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "hello", "algorithm": "SHA-256"}'

# UUID
curl -s -X POST https://api.findutils.com/api/tools/uuid_generate/execute \
  -H "Content-Type: application/json" \
  -d '{"count": 3}'

# Unit convert
curl -s -X POST https://api.findutils.com/api/tools/unit_convert/execute \
  -H "Content-Type: application/json" \
  -d '{"value": 100, "from": "km", "to": "miles"}'

# Case convert
curl -s -X POST https://api.findutils.com/api/tools/case_convert/execute \
  -H "Content-Type: application/json" \
  -d '{"text": "hello world from api", "to": "camel"}'

# List all tools (pretty print)
curl -s https://api.findutils.com/api/tools | jq .
```

---

## MCP Protocol Details

Transport: Streamable HTTP (POST to root URL with JSON-RPC 2.0 body)

### Method: initialize

Required first call. Returns server capabilities.

```bash
curl -s -X POST https://mcp.findutils.com/ \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "initialize",
    "params": {
      "protocolVersion": "2024-11-05",
      "capabilities": {},
      "clientInfo": {"name": "my-client", "version": "1.0"}
    }
  }'
```

Response:
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "protocolVersion": "2024-11-05",
    "capabilities": {"tools": {}},
    "serverInfo": {
      "name": "findutils-mcp",
      "version": "1.0.0"
    }
  }
}
```

### Method: tools/list

Returns the full tool catalog with JSON Schema for each tool.

```bash
curl -s -X POST https://mcp.findutils.com/ \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc": "2.0", "id": 2, "method": "tools/list", "params": {}}'
```

### Method: tools/call

Execute a tool. Returns MCP content object.

```bash
curl -s -X POST https://mcp.findutils.com/ \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 3,
    "method": "tools/call",
    "params": {
      "name": "hash_generate",
      "arguments": {"text": "hello", "algorithm": "SHA-256"}
    }
  }'
```

Response:
```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "result": {
    "content": [{"type": "text", "text": "{\"hash\":\"2cf24d...\",\"algorithm\":\"SHA-256\"}"}]
  }
}
```

### Batch Requests (MCP)

Send up to 50 JSON-RPC calls in a single request:

```bash
curl -s -X POST https://mcp.findutils.com/ \
  -H "Content-Type: application/json" \
  -d '[
    {"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"uuid_generate","arguments":{}}},
    {"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"uuid_generate","arguments":{}}}
  ]'
```

---

## Rate Limits

| Limit | Value |
|---|---|
| Per minute per IP | 60 requests (Tool API) / 120 requests (MCP) |
| Daily per IP | 500 requests (Tool API) / 1,000 requests (MCP) |
| Global daily | 50,000 requests (Tool API) / 100,000 requests (MCP) |

No API keys needed. Rate limiting is in-memory and resets on cold starts.

When a limit is hit, the API returns HTTP 429 with an error message.

---

## Error Handling

### REST API Error Format

```json
{
  "error": "Tool not found",
  "code": "NOT_FOUND"
}
```

### MCP Error Format (JSON-RPC 2.0)

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "error": {
    "code": -32601,
    "message": "Tool \"bad_tool\" not found."
  }
}
```

### JSON-RPC Error Codes

| Code | Name | When |
|---|---|---|
| -32700 | Parse Error | Request body is not valid JSON |
| -32600 | Invalid Request | Missing `jsonrpc` field or malformed envelope |
| -32601 | Method Not Found | Unknown method or tool name |
| -32602 | Invalid Params | Missing required parameter or wrong type |
| -32603 | Internal Error | Unexpected server error |

### HTTP Status Codes

| Status | Meaning |
|---|---|
| 200 | Success |
| 400 | Bad request (invalid JSON, missing params) |
| 404 | Tool not found |
| 405 | Method not allowed (MCP requires POST) |
| 413 | Payload too large (max 1MB) |
| 429 | Rate limit exceeded |
| 500 | Internal server error |

---

## Tool Parameter Reference

### `case_convert` — `to` values

`camel`, `pascal`, `snake`, `kebab`, `screaming_snake`, `title`, `sentence`, `lower`, `upper`

### `hash_generate` — `algorithm` values

`MD5`, `SHA-1`, `SHA-256`, `SHA-512`

### `hmac_generate` — `algorithm` values

`SHA-256`, `SHA-512`

### `color_convert` — `from`/`to` values

`hex`, `rgb`, `hsl`, `hsv`

### `unit_convert` — common `from`/`to` values

Length: `km`, `m`, `cm`, `mm`, `miles`, `yards`, `feet`, `inches`
Weight: `kg`, `g`, `mg`, `lbs`, `oz`, `ton`
Temperature: `C`, `F`, `K`
Volume: `L`, `mL`, `gal`, `fl_oz`, `cup`, `pint`, `quart`
Speed: `km/h`, `mph`, `m/s`, `knots`
Area: `m2`, `km2`, `ft2`, `acres`, `hectares`

### `unix_timestamp_convert` — `mode` values

`to_date` (timestamp to human date), `to_timestamp` (date string to timestamp), `now` (current timestamp)

### `percentage_calculate` — `mode` values

`percent_of` (X% of Y), `what_percent` (X is what % of Y), `percent_change` (% change from X to Y)

### `random_string` — `charset` values

`alphanumeric`, `alphabetic`, `numeric`, `hex`, `custom` (use `custom` field for character set)

### `text_reverse` — `mode` values

`chars` (default), `words`, `lines`

### `morse_code` / `roman_numeral` / `string_escape` — `mode` values

morse: `encode`, `decode`
roman: `to_roman`, `to_arabic`, `auto`
escape: `escape`, `unescape`

### `line_sort` — `mode` values

`alpha` (default), `numeric`, `length`

