# HopGraph MCP Server

Verify Australian and New Zealand businesses against government registers via any MCP-compatible AI agent.

Returns registration status, directors, licences, trading names, and a three-tier risk assessment (CLEAR / ADVISORY / FLAGS_FOUND) that surfaces regulatory findings across jurisdictions — including bans, disqualifications, and insolvencies that may not appear in any single register.

Each verification produces an immutable compliance record with a unique audit UID.

Compatible with Claude, ChatGPT, Cursor, and any MCP-compatible AI client.

<a href="https://glama.ai/mcp/servers/@j-sulliman/hop-graph-mcp">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@j-sulliman/hop-graph-mcp/badge" alt="HopGraph MCP server" />
</a>

## Quick Start

### 1. Get a free API key

Sign up at [hopgraph.com/signup](https://hopgraph.com/signup). No credit card required.

### 2. Add to Claude Desktop

Open your Claude Desktop config file:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Add the following configuration (replace `YOUR_API_KEY` with your actual key):

```json
{
  "mcpServers": {
    "hopgraph": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://hopgraph.com/mcp/",
        "--header",
        "Authorization:${AUTH_HEADER}"
      ],
      "env": {
        "AUTH_HEADER": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### 3. Restart Claude Desktop

After saving the config, restart the app. You'll see the HopGraph tools available in your conversation.

### 4. Test it

Ask your AI assistant:

> Verify business ABN 35002976294

You should see a full verification with company status, licence details, and a risk assessment.

## Tools

### verify_business

Verify any Australian or New Zealand business against government registers. Accepts ABN (11 digits), ACN (9 digits), NZBN (13 digits), or company name.

Returns registration status, directors, licences, trading names, and a three-tier risk assessment (CLEAR / ADVISORY / FLAGS_FOUND) that surfaces regulatory findings across jurisdictions — including bans, disqualifications, and insolvencies that may not appear in any single register.

Each verification produces an immutable compliance record with a unique audit UID.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `identifier` | Yes | ABN, ACN, NZBN, or company name to verify |
| `country` | No | `AU` or `NZ`. Auto-detected from identifier format if omitted |

### search_business

Search Australian and New Zealand business entities by name. Covers 2.3 million+ Australian companies, 3.2 million business names, and New Zealand NZBN-registered entities.

Use this to find the correct identifier before calling `verify_business`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Business name or partial name to search for |
| `limit` | No | Maximum results to return (default 20, max 50) |

### get_verification

Retrieve a previously generated compliance verification record by its unique audit UID. Returns the immutable entity snapshot captured at verification time, data sources consulted with freshness timestamps, and the risk assessment result.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `verification_uid` | Yes | The verification UID (UUID) returned by a previous `verify_business` call |

### get_verification_history <sup>Professional+</sup>

Retrieve the verification history for a specific entity, showing all past compliance checks you have run against it. Returns verification dates, risk assessment results, and audit UIDs. Useful for tracking how an entity's compliance status has changed over time.

Requires a Professional or Business tier API key — [upgrade at hopgraph.com/billing](https://hopgraph.com/billing).

| Parameter | Required | Description |
|-----------|----------|-------------|
| `identifier` | Yes | ABN, ACN, NZBN, or company name used in previous `verify_business` calls |
| `limit` | No | Maximum history records to return (default 20, max 100) |

## Coverage

| Source | Records | Country |
|--------|---------|---------|
| ASIC Companies | 2.3M+ | Australia |
| ASIC Business Names | 3.2M+ | Australia |
| ASIC Financial Advisers | 87K+ | Australia |
| ASIC AFS Licences | 6.5K+ | Australia |
| ASIC Credit Licences | 4.5K+ | Australia |
| ASIC Credit Representatives | 50K+ | Australia |
| ASIC Banned & Disqualified Persons | 7K+ | Australia |
| ASIC Banned Organisations | 15+ | Australia |
| NZBN Register | Live API | New Zealand |

## Pricing

| Tier | Verifications | Rate Limit | Price |
|------|--------------|------------|-------|
| Free | 5/month | 10 req/min | Free |
| Professional | Unlimited | 60 req/min | Coming soon |
| Business | Unlimited | 120 req/min | Coming soon |

## REST API

HopGraph also provides a REST API. See [hopgraph.com/docs](https://hopgraph.com/docs) for full documentation.

## Legal

Findings are factual observations from public government registers, not identity assertions. Professional judgment should be applied to all results. See [Terms of Service](https://hopgraph.com/terms) and [Privacy Policy](https://hopgraph.com/privacy).

Australian data sourced from ASIC under Creative Commons Attribution 3.0 Australia. New Zealand data sourced from the NZBN Register maintained by MBIE.