# Free-upload

## MCQ Studio — Cloudflare MCP server

The MCQ Studio Worker and photo bridge are deployed on Cloudflare. Its `workers.dev` hostname is enabled and the live deployment is serving the latest GitHub photo-bridge source.

- Website: https://mcq-mcp-server.shachindeury24.workers.dev/
- MCP endpoint: https://mcq-mcp-server.shachindeury24.workers.dev/mcp
- Health endpoint: https://mcq-mcp-server.shachindeury24.workers.dev/health
- Source: [mcq-mcp/](./mcq-mcp/)

### Sign in

The encrypted Cloudflare Worker secret `APP_ACCESS_TOKEN` is configured. Enter the private code chosen for that secret when signing in to the website or approving its OAuth consent screen. Cloudflare will not display the original secret again. If the code has been lost, replace it with a new private value in **Workers & Pages → mcq-mcp-server → Settings → Variables and Secrets**, then redeploy if requested.

Never commit the access code to GitHub or share it publicly. It is a login code, not an OpenAI API key.

### Photo bridge

The live Worker includes a private photo-upload interface and MCP image tools:

- `list_mcq_images` lists uploaded photos.
- `read_mcq_image` returns a selected photo as MCP image content for ChatGPT to inspect.
- `delete_mcq_image` deletes an uploaded photo.

Image listing and image reading use read access; uploading and deleting photos require write access. The website cannot directly inject an image into an already-open ChatGPT conversation; a connected ChatGPT app must call the MCP image tool.

### No OpenAI API key

The new MCP server does not call an AI API. ChatGPT supplies image interpretation and reasoning when a compatible account can connect to the custom MCP server. Custom MCP access depends on ChatGPT plan/workspace availability.

## Legacy photo-chat demo

The older API-based website remains in [mcq-chat/](./mcq-chat/) and runs separately at https://mcq-photo-chat-api.shachindeury24.workers.dev/. It requires an OpenAI API key and is not the no-key MCP server.
