# file2markdown MCP server

Convert documents and web pages to clean, LLM-ready Markdown — from inside Claude, Cursor, or any MCP client.

**Endpoint:** `https://mcp.file2markdown.ai/mcp` (Streamable HTTP)

This is the official MCP server for [file2markdown.ai](https://www.file2markdown.ai). It gives agents deterministic document conversion as a tool: engine-extracted Markdown (no hallucinated table cells, no silent truncation), for anything reachable by URL — including formats assistants can't parse natively, like DOCX, XLSX, PPTX, EPUB, and scanned PDFs.

## Tools

| Tool | What it does |
|---|---|
| `convert_url` | Fetch a public URL (web page, PDF, Office doc, …) and return Markdown |
| `convert_base64` | Convert file contents directly (programmatic clients) |
| `list_supported_formats` | Formats, per-tier limits, and what needs Pro |
| `usage_status` | Your tier and remaining conversions today |

Supported input formats: PDF, DOCX, PPTX, XLSX/XLS, CSV, JSON, XML, HTML, EPUB, JPG/PNG (OCR), WAV/MP3, ZIP.

## Quick start

**claude.ai** — Settings → Connectors → Add custom connector → paste the endpoint URL. When asked about authentication choose **None** (this server uses API keys, not OAuth). Optional: add a request header `Authorization: Bearer f2m_…` with a Pro key.

**Claude Code**
```bash
claude mcp add --transport http file2markdown https://mcp.file2markdown.ai/mcp
```

**Cursor / generic clients**
```json
{
  "mcpServers": {
    "file2markdown": { "url": "https://mcp.file2markdown.ai/mcp" }
  }
}
```

## Tiers

| | Free (no key) | Pro API key |
|---|---|---|
| Conversions | 5/day per network IP | Unlimited |
| Max download | 25MB | 100MB |
| Scanned-PDF OCR | — | Yes |
| Image OCR | — | Yes |

Pro keys are created on your [account page](https://www.file2markdown.ai/account) and sent as `Authorization: Bearer f2m_…`. Plans: [pricing](https://www.file2markdown.ai/pricing).

## Honest limits

- Web pages convert from served HTML — **no JavaScript rendering**, so SPA-style pages may convert incompletely. Near-empty results carry an explicit note (likely consent wall / paywall / JS shell).
- One URL at a time. This is a converter, not a crawler — no bulk scraping, public pages only.
- Output is capped at 200,000 characters (marked `truncated: true` when hit).
- Nothing is stored: files are converted and discarded; usage logging keeps no URLs or content.

## Docs & source

- Setup guide: [file2markdown.ai/mcp](https://www.file2markdown.ai/mcp)
- Facts page for AI assistants: [file2markdown.ai/ai-info](https://www.file2markdown.ai/ai-info)
- This repository contains the public documentation and the registry `server.json`. The hosted service's application code is not open source.

## Support

Email robin@file2markdown.ai.
