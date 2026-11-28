# Free-upload

## MCQ Studio — Cloudflare MCP server

The MCQ Studio Worker has been uploaded to Cloudflare and its `workers.dev` hostname is enabled.

- Website: https://mcq-mcp-server.shachindeury24.workers.dev/
- MCP endpoint: https://mcq-mcp-server.shachindeury24.workers.dev/mcp
- Health endpoint: https://mcq-mcp-server.shachindeury24.workers.dev/health
- Source: [mcq-mcp/](./mcq-mcp/)

### Setup still required

The deployed Worker currently has **no `APP_ACCESS_TOKEN` secret configured**. As a result, its website login and OAuth sign-in cannot be used yet.

In Cloudflare Dashboard:

1. Open **Workers & Pages** → **mcq-mcp-server**.
2. Open **Settings** → **Variables and Secrets** → **Add** → **Secret**.
3. Set the name to `APP_ACCESS_TOKEN`.
4. Choose a long private access code and save it as a secret.
5. Redeploy if Cloudflare asks.

Use that same code to sign in to the MCQ Studio website and its OAuth consent page. Do not add the code to GitHub or share it publicly. It is a login code, not an OpenAI API key.

### Photo upload status

The latest GitHub source in [mcq-mcp/](./mcq-mcp/) now includes a private photo-upload interface and MCP image tools (`list_mcq_images`, `read_mcq_image`, and `delete_mcq_image`). **That newer image update has not been deployed to Cloudflare** because the update request was blocked. The live Worker is still the earlier question-bank version.

When the updated source is deployed, ChatGPT can retrieve an uploaded image through `read_mcq_image` and inspect it in the connected conversation. The website cannot directly inject an image into an already-open ChatGPT chat.

### No OpenAI API key

The new MCP server does not call an AI API. ChatGPT supplies image interpretation and reasoning when a compatible account can connect to the custom MCP server. Custom MCP access depends on ChatGPT plan/workspace availability.

## Legacy photo-chat demo

The older API-based website remains in [mcq-chat/](./mcq-chat/) and runs separately at https://mcq-photo-chat-api.shachindeury24.workers.dev/. It requires an OpenAI API key and is not the no-key MCP server.
