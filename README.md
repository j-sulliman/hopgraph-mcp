# HopGraph MCP Server

Verify Australian and New Zealand businesses against government registers via any MCP-compatible AI agent.

Returns registration status, directors, licences, trading names, and a three-tier risk assessment (CLEAR / ADVISORY / FLAGS_FOUND) that surfaces regulatory findings across jurisdictions — including bans, disqualifications, insolvencies, and disqualified directors that may not appear in any single register.

Each verification produces an immutable compliance record with a unique audit UID.

Compatible with Claude, ChatGPT, Cursor, and any MCP-compatible AI client.

## Quick Start

### 1. Get a free API key

Sign up at [hopgraph.com/signup](https://hopgraph.com/signup). No credit card required.

### 2. Add to Claude Desktop

Open your Claude Desktop config file:

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

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

### `verify_business`

Verify any Australian or New Zealand business against government registers. Accepts ABN (11 digits), ACN (9 digits), NZBN (13 digits), or company name.

Returns registration status, directors, licences, trading names, and a three-tier risk assessment (CLEAR / ADVISORY / FLAGS_FOUND). For Australian entities, cross-references adviser registrations against banned persons registers across entity licence chains. For New Zealand entities, checks every director against the NZ Companies Office Disqualified Directors and Insolvency registers in real time, and screens them against Australian regulatory registers.

Each verification produces an immutable compliance record with a unique audit UID. Findings are labelled as "Exact name match" or "Partial name match" so you can apply the appropriate level of scrutiny.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `identifier` | Yes | ABN, ACN, NZBN, or company name to verify |
| `country` | No | `AU` or `NZ`. Auto-detected from identifier format if omitted |

### `search_business`

Search Australian and New Zealand business entities by name. Covers 2.3 million+ Australian companies, 3.2 million business names, and New Zealand NZBN-registered entities.

Use this to find the correct identifier before calling `verify_business`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Business name or partial name to search for |
| `limit` | No | Maximum results to return (default 20, max 50) |

### `expand_person_network`

Discover all NZ company directorships and shareholdings held by a named person via the NZ Companies Office register. Returns every company where the person holds a role — company name, NZBN, status, role type, and appointment date — plus flags for companies already in the HopGraph database.

Use this to map a person's corporate network beyond what a single entity lookup reveals.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `person_name` | Yes | Full name of the person to search for (e.g. "Stephen Mikkelsen") |
| `role_type` | No | Filter by role type: `DIR` (directors), `SHR` (shareholders), or `ALL` (default) |

### `get_verification`

Retrieve a previously generated compliance verification record by its unique audit UID. Returns the immutable entity snapshot captured at verification time, data sources consulted with freshness timestamps, and the risk assessment result.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `verification_uid` | Yes | The verification UID (UUID) returned by a previous `verify_business` call |

### `get_verification_history` <sup>Professional+</sup>

Retrieve the verification history for a specific entity, showing all past compliance checks you have run against it. Returns verification dates, risk assessment results, and audit UIDs. Useful for tracking how an entity's compliance status has changed over time.

Requires a Professional or Business tier API key — upgrade at [hopgraph.com/billing](https://hopgraph.com/billing).

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
| NZ Companies Office Disqualified Directors | Live API | New Zealand |
| NZ Companies Office Insolvency Register | Live API | New Zealand |

## Chat Interface

A browser-based chat interface is available at [hopgraph.com/chat](https://hopgraph.com/chat) for professionals who prefer to work directly in the browser. Same cross-referencing, same compliance records. Supports all MCP tool capabilities including person network expansion and verification history.

## Pricing

| Tier | Verifications | Rate Limit | Price |
|------|---------------|------------|-------|
| Free | 50/month | 10 req/min | Free |

## REST API

HopGraph also provides a REST API. See [hopgraph.com/docs](https://hopgraph.com/docs) for full documentation.

## Legal

Findings are factual observations from public government registers, not identity assertions. Each match is labelled with its confidence level. Professional judgment should be applied to all results. See [Terms of Service](https://hopgraph.com/terms) and [Privacy Policy](https://hopgraph.com/privacy).

Australian data sourced from ASIC under Creative Commons Attribution 3.0 Australia. New Zealand data sourced from the NZBN Register and NZ Companies Office registers (Disqualified Directors, Insolvency) maintained by MBIE.
