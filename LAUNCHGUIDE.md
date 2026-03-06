# HopGraph

## Tagline
Verify ANZ businesses against government registers. Surfaces cross-jurisdictional findings.

## Description
HopGraph verifies Australian and New Zealand businesses against government registers via MCP. It returns registration status, directors, licences, trading names, and a three-tier risk assessment (CLEAR / ADVISORY / FLAGS_FOUND) that surfaces regulatory findings across jurisdictions — including bans, disqualifications, and insolvencies that may not appear in any single register. Each verification produces an immutable compliance record with a unique audit UID. Built for compliance professionals, accountants, lawyers, and AI agents performing due diligence on ANZ entities.

## Setup Requirements
- `AUTH_HEADER` (required): API key for authentication. Free tier available (5 verifications/month). Get one at https://hopgraph.com/signup

## Category
Finance

## Use Cases
Business verification, Due diligence, AML compliance, KYC checks, Adviser screening, Regulatory risk assessment, Entity research, Cross-jurisdictional screening, Licence verification, Company status checks

## Features
- Verify any Australian or New Zealand business by ABN, ACN, NZBN, or company name
- Three-tier risk assessment: CLEAR, ADVISORY, or FLAGS_FOUND
- Cross-references regulatory bans and disqualifications across jurisdictions
- Returns directors, officers, and shareholders with role details
- AFS and credit licence verification with licence holder details
- Financial adviser registration screening against banned persons registers
- Cross-jurisdictional screening of NZ directors against Australian regulatory registers
- Trading name and business name history
- Insolvency status detection
- Industry classification data
- Immutable compliance record with unique audit UID for every verification
- Verification history tracking over time (Professional tier)
- Search across 2.3M+ Australian companies and 3.2M+ business names
- Live NZBN API integration for New Zealand entities
- Sub-100ms response times on cached data
- Data sourced from 9 government registers across two countries

## Getting Started
- "Verify business ABN 35002976294"
- "Check if Capstone Financial Planning has any regulatory flags"
- "Search for insurance companies in New Zealand"
- "Look up NZBN 9429033177502 and check for cross-jurisdictional findings"
- Tool: verify_business — Verify any ANZ business and get a risk assessment with compliance record
- Tool: search_business — Search entities by name to find the correct identifier
- Tool: get_verification — Retrieve a past compliance record by its audit UID
- Tool: get_verification_history — View how an entity's compliance status has changed over time (Professional tier)

## Tags
compliance, verification, government-data, australia, new-zealand, aml, due-diligence, regulatory, finance, business-verification, kyc, asic, nzbn, adviser-screening, risk-assessment, audit-trail, mcp

## Documentation URL
https://hopgraph.com/docs

## Health Check URL
https://hopgraph.com/health
