# MCQ Studio MCP

A Cloudflare Worker project for a question-bank website and authenticated Streamable HTTP MCP server. It does not call an AI API and does not require an OpenAI API key.

## Cloudflare deployment

- Website: https://mcq-mcp-server.shachindeury24.workers.dev/
- MCP endpoint: https://mcq-mcp-server.shachindeury24.workers.dev/mcp
- Health: https://mcq-mcp-server.shachindeury24.workers.dev/health
- OAuth authorization-server metadata: https://mcq-mcp-server.shachindeury24.workers.dev/.well-known/oauth-authorization-server
- OAuth protected-resource metadata: https://mcq-mcp-server.shachindeury24.workers.dev/.well-known/oauth-protected-resource/mcp

Cloudflare confirms that the Worker deployment exists and the `workers.dev` subdomain is enabled. The live Worker currently contains the initial MCQ question-bank version.

## Required Cloudflare secret

The Worker currently has no secrets configured, so sign-in is not usable yet.

1. Open Cloudflare Dashboard → Workers & Pages → `mcq-mcp-server`.
2. Open Settings → Variables and Secrets → Add → Secret.
3. Set the name to `APP_ACCESS_TOKEN`.
4. Choose a long private access code of your own and save it.
5. Redeploy if Cloudflare asks.

Never commit this code to GitHub. It is used to sign in on the website and the OAuth consent page. It is not a client secret or OpenAI API key.

## MCP tools in the deployed initial version

- `save_mcq`
- `search_mcqs`
- `list_mcqs`
- `get_mcq`
- `check_mcq_answer`
- `delete_mcq`
- `mcq_stats`

## Photo bridge source status

The latest `worker.js` and `index.html` in this folder contain an additional photo-upload bridge:

- The website accepts JPG, PNG, and WEBP photos and stores them in the private `MCQ_STORE` KV namespace.
- `list_mcq_images` lists uploaded photos.
- `read_mcq_image` returns the selected photo as MCP image content so ChatGPT can inspect it.
- `delete_mcq_image` removes an uploaded photo.

**Important:** this photo-bridge source update is in GitHub but has not been deployed to Cloudflare. The live Worker is still on the initial release until that updated source is deployed.

## Authentication design

The source implements OAuth authorization code + PKCE (S256), dynamic client registration, ChatGPT Client ID Metadata Documents, and a consent page.

ChatGPT can use a public OAuth client with PKCE; a static client secret is not required for that flow. The user authenticates at the MCQ Studio consent page using the `APP_ACCESS_TOKEN` secret.

## KV binding

The Worker uses the `MCQ_STORE` KV binding. The Cloudflare namespace has already been created and bound to the Worker.

## AI behavior

The MCP server stores and returns questions and (in the newer source) images. ChatGPT reads uploaded photos, transcribes questions, explains choices, and calls the MCP tools. The website does not itself run OCR or an AI model.

## ChatGPT plan note

Hosting an MCP server does not automatically make it selectable in ChatGPT. Custom MCP connection support depends on the ChatGPT plan and workspace permissions.
