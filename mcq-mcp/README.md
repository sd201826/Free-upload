# MCQ Studio MCP

A Cloudflare Worker that exposes an authenticated Streamable HTTP MCP server and a small question-bank website. It does not call an AI API and requires no OpenAI API key.

## Endpoints

- Website: `/`
- Health: `/health`
- MCP: `/mcp`
- OAuth authorization server metadata: `/.well-known/oauth-authorization-server`
- Protected resource metadata: `/.well-known/oauth-protected-resource/mcp`

## MCP tools

- `save_mcq`
- `search_mcqs`
- `list_mcqs`
- `get_mcq`
- `check_mcq_answer`
- `delete_mcq`
- `mcq_stats`

## Authentication

The Worker uses OAuth 2.1 authorization code + PKCE (S256), dynamic client registration, ChatGPT Client ID Metadata Documents, and a branded consent page. The user signs in using the Worker secret `APP_ACCESS_TOKEN`. The MCP client is a public client and does not receive a client secret; it uses PKCE as required for public OAuth clients.

## Deploy

Create a Workers KV namespace, bind it as `MCQ_STORE`, and deploy this folder with Wrangler. Add `APP_ACCESS_TOKEN` as a Worker secret. Do not put the access code in GitHub. The deployed instance uses a private KV namespace.

## AI behavior

The MCP server stores and returns structured MCQ data. ChatGPT or another connected model reads uploaded images, transcribes questions, solves them, and calls the tools. No model is embedded in this Worker. The website is a question-bank manager and does not perform OCR.
