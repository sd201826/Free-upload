# MCQ Studio MCP

A Cloudflare Worker project for a question-bank website and authenticated Streamable HTTP MCP server. It does not call an AI API and does not require an OpenAI API key.

## Live deployment

- Website: https://mcq-mcp-server.shachindeury24.workers.dev/
- MCP endpoint: https://mcq-mcp-server.shachindeury24.workers.dev/mcp
- Health: https://mcq-mcp-server.shachindeury24.workers.dev/health
- OAuth authorization-server metadata: https://mcq-mcp-server.shachindeury24.workers.dev/.well-known/oauth-authorization-server
- OAuth protected-resource metadata: https://mcq-mcp-server.shachindeury24.workers.dev/.well-known/oauth-protected-resource/mcp

Cloudflare confirms the photo-bridge Worker deployment and the enabled `workers.dev` subdomain. The live Worker source contains the photo-upload endpoint and image MCP tools.

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

The website accepts JPG, PNG, and WEBP photos and stores them in the private `MCQ_STORE` KV namespace. Use `list_mcq_images` to find an uploaded photo, then `read_mcq_image` to return it as MCP image content. ChatGPT can visually inspect the returned image, transcribe its questions, explain choices, and save MCQs. The server itself does not perform OCR or host a language model.

## Authentication

The Worker uses OAuth authorization code + PKCE (S256), dynamic client registration, ChatGPT Client ID Metadata Documents, a consent page, bearer-token validation, and token expiry/refresh.

The encrypted Worker secret `APP_ACCESS_TOKEN` is configured. Enter the private value chosen for that secret on the website login and OAuth consent form. Cloudflare will not reveal the old secret again; if it is lost, replace it in **Workers & Pages → mcq-mcp-server → Settings → Variables and Secrets**.

ChatGPT uses a public OAuth client with PKCE; a static client secret is not required for this flow. Never put the access code in GitHub.

## KV binding

The Worker uses the configured `MCQ_STORE` KV namespace for saved questions, uploaded photos, and temporary OAuth/token records.

## AI behavior

The MCP server stores and returns questions and images. ChatGPT provides image understanding and reasoning when a compatible ChatGPT app connection is available. The website does not itself run an AI model, and no OpenAI API key is used.

## ChatGPT plan note

Hosting an MCP server does not automatically make it selectable in ChatGPT. Custom MCP connection support depends on the ChatGPT plan and workspace permissions.
