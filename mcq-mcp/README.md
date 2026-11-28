# MCQ Studio MCP

A Cloudflare Worker that serves a question-bank website and an authenticated Streamable HTTP MCP server. It does not call an AI API and does not require an OpenAI API key.

## Deployed endpoints

- Website: https://mcq-mcp-server.shachindeury24.workers.dev/
- Health: https://mcq-mcp-server.shachindeury24.workers.dev/health
- MCP: https://mcq-mcp-server.shachindeury24.workers.dev/mcp
- OAuth authorization-server metadata: https://mcq-mcp-server.shachindeury24.workers.dev/.well-known/oauth-authorization-server
- OAuth protected-resource metadata: https://mcq-mcp-server.shachindeury24.workers.dev/.well-known/oauth-protected-resource/mcp

## MCP tools

- `save_mcq`
- `search_mcqs`
- `list_mcqs`
- `get_mcq`
- `check_mcq_answer`
- `delete_mcq`
- `mcq_stats`
- `list_mcq_images`
- `read_mcq_image`
- `delete_mcq_image`

ChatGPT can read a photo in the conversation, extract the MCQ text and choices, reason about the answer, then call these tools to save or retrieve the question bank. The server stores structured data and private uploaded question photos. The website uploads images to Cloudflare KV. ChatGPT can call `list_mcq_images` followed by `read_mcq_image`; the MCP server returns the photo as MCP image content so ChatGPT can visually inspect it. The server does not perform OCR or host a language model.

## Authentication

The Worker implements OAuth authorization-code flow with PKCE (S256), dynamic client registration, ChatGPT Client ID Metadata Documents, a consent screen, bearer-token validation, access-token expiry, and refresh-token rotation.

ChatGPT is a public OAuth client and can identify itself using a client ID metadata document or dynamic registration. A client secret is not needed for the public-client PKCE flow. The user signs in on the MCQ Studio consent page using the Worker secret `APP_ACCESS_TOKEN`.

## Required one-time Cloudflare setup

The Worker has been deployed and its `workers.dev` subdomain is enabled. The encrypted login secret has not been added yet.

1. Open Cloudflare Dashboard → Workers & Pages → `mcq-mcp-server`.
2. Open Settings → Variables and Secrets → Add → Secret.
3. Name: `APP_ACCESS_TOKEN`.
4. Value: choose a long, private access code of your own.
5. Save the secret. If Cloudflare asks, deploy the Worker again.

Never commit the access code to GitHub. Use the same code on the website's login page and on the OAuth consent page.

## Cloudflare KV

The `MCQ_STORE` binding is configured and points to the Cloudflare KV namespace created for this project. MCQ records, OAuth clients, short-lived authorization codes, access tokens and refresh tokens are stored there with expiry settings where applicable.

## Deploy from source

This folder includes `worker.js`, `index.html`, and `wrangler.jsonc`. Deploy with Wrangler after installing its dependencies in a normal Cloudflare Workers environment. The current live Worker was uploaded directly through the Cloudflare API.

## Important plan limitation

The server can be hosted independently, but ChatGPT custom MCP connection availability depends on the ChatGPT plan and workspace permissions. The website can be used as a question-bank manager and private photo uploader after the access secret is configured. In ChatGPT, the user must explicitly invoke the connected MCQ Studio app to fetch and inspect an uploaded image; the website cannot inject a file into an already-open ChatGPT conversation.

No OpenAI API key is used or stored by this project.
