# Website Phrase and Business Model Classifier MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-website-phrase-business-model-classifier)](https://smithery.ai/servers/mambabuilt/mcp-website-phrase-business-model-classifier) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-website-phrase-business-model-classifier/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-website-phrase-business-model-classifier) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-website-phrase-business-model-classifier%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-website-phrase-business-model-classifier&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-website-phrase-business-model-classifier)](https://www.npmjs.com/package/@mambalabsdev/mcp-website-phrase-business-model-classifier) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-website-phrase-business-model-classifier)](https://www.npmjs.com/package/@mambalabsdev/mcp-website-phrase-business-model-classifier) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-website-phrase-business-model-classifier)](https://github.com/mambalabsdev/mcp-website-phrase-business-model-classifier/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-website-phrase-business-model-classifier)

<a href="https://mcprush.com/to/website-phrase-business-model-classifier-mcp?ref=badge"><img width="380" height="200" src="https://mcprush.com/badge/website-phrase-business-model-classifier-mcp/card.svg" alt="Website Phrase Business Model Classifier MCP server" /></a>

An MCP server for the Mamba Labs Website Phrase and Business Model Classifier actor on Apify. Give it company domains. For each one it reads the homepage and up to 5 pages it links to, and returns one row: B2B, B2C, or both; whether the site presents itself as SaaS, an online store, an agency, a manufacturer, a wholesaler, a distributor, or a marketplace; and whether your own phrases appear, with the quoted text and the page as evidence.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

The rules are fixed and written out, not a language model, so the same pages always give the same answer. A site that does not say enough comes back `unknown`. A hit inside a negation ("we are not an agency") never counts. Unreachable, blocked, robots.txt disallowed, and empty sites come back free with a `row_status` saying so. All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-website-phrase-business-model-classifier": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-website-phrase-business-model-classifier"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `classify_website` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Which of these 40 domains are agencies, and which of them say they are a Clay agency?"
- "Split this store list into B2B and B2C and show me the evidence for each."
- "Do any of these suppliers say they do private label?"

## Tool

`classify_website`. One tool. Example arguments:

```json
{
  "domains": ["lodgecastiron.com", "hubspot.com"],
  "phrases": ["cast iron", "private label"]
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers are sent as strings.

| Input | Type | Description |
|---|---|---|
| `domains` | array | Company domains, up to 500 |
| `domain` | string | One domain |
| `phrases` | array | Your buyer phrases, up to 25 |
| `categories` | array | Any of saas, ecommerce, agency, manufacturer, wholesaler, distributor, marketplace; empty means all |
| `max_pages` | string | Pages per site, 1 to 10. Default 6 |
| `max_charge_usd` | string | Optional cost cap for the run |
| `proxy_mode` | string | auto (default) or direct |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `domain-classified`, per domain read and classified | $0.0045 | $0.004275 | $0.00405 | $0.003825 |
| `apify-actor-start`, per run start | $0.0005 | $0.0005 | $0.0005 | $0.0005 |

Unreachable, blocked, robots.txt disallowed, empty, and error rows are free.

## Your keys

The actor needs no key and holds none. It reads the company's own public web pages. Proxy traffic adds nothing to your price: Mamba Labs pays the platform costs of the run.

## Full actor documentation

[apify.com/mambalabs/website-phrase-business-model-classifier](https://apify.com/mambalabs/website-phrase-business-model-classifier)

## License

MIT. See [LICENSE](LICENSE).
