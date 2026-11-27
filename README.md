# Free-upload

## MCQ Studio

The MCQ Studio photo-to-chat website is live:

**https://mcq-photo-chat-api.shachindeury24.workers.dev/**

Source code is in [mcq-chat/](./mcq-chat/).

- Website source: [mcq-chat/index.html](./mcq-chat/index.html)
- Setup guide: [mcq-chat/README.md](./mcq-chat/README.md)
- Cloudflare API Worker source: [mcq-chat/worker/worker.js](./mcq-chat/worker/worker.js)

To activate AI replies, add an encrypted Cloudflare Worker secret named `OPENAI_API_KEY` to the `mcq-photo-chat-api` Worker. The app also requires a private access code, which is not stored in this repository. Never commit secrets to GitHub.

API usage is billed separately from ChatGPT; have a parent or guardian manage the API key and billing.

GitHub Pages can optionally be enabled under Settings → Pages (main branch, root folder) to serve the source website at:
https://sd201826.github.io/Free-upload/mcq-chat/
