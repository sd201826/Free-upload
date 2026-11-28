# Free-upload

## MCQ Studio — new MCP server

The new MCQ Studio question-bank website and authenticated MCP endpoint are deployed on Cloudflare:

- **Website:** https://mcq-mcp-server.shachindeury24.workers.dev/
- **MCP endpoint:** https://mcq-mcp-server.shachindeury24.workers.dev/mcp
- **Health:** https://mcq-mcp-server.shachindeury24.workers.dev/health
- **Source and setup:** [mcq-mcp/](./mcq-mcp/)

The new server stores MCQ questions in Cloudflare KV and exposes MCP tools for saving, searching, listing, retrieving, checking, and deleting questions. ChatGPT supplies image reading and reasoning when a compatible ChatGPT MCP connection is available. **The new server does not require an OpenAI API key.**

### One-time Cloudflare setup still required

The Worker needs one encrypted secret before its website login and OAuth consent flow can accept sign-ins:

1. Open Cloudflare Dashboard → Workers & Pages → `mcq-mcp-server`.
2. Open Settings → Variables and Secrets → Add → Secret.
3. Set the variable name to `APP_ACCESS_TOKEN` and choose your own long private access code.
4. Save it as a secret and redeploy if Cloudflare asks.

Do not put this access code in GitHub or share it publicly. This is the password you enter into the MCQ Studio website and OAuth consent page. It is **not** an OpenAI API key.

### Legacy photo-chat app

The older API-based photo-chat demo is still in [mcq-chat/](./mcq-chat/) and uses the separate `mcq-photo-chat-api` Worker. It requires an OpenAI API key and is not the new MCP server. Use the new `mcq-mcp` project for the no-OpenAI-key question-bank/MCP setup.

## GitHub Pages

The source files can also be viewed on GitHub Pages, but the interactive website and authenticated API need the Cloudflare Worker deployment.
