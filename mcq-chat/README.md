# MCQ Studio

A responsive image-to-chat study assistant. Upload a question photo to the selected chat, then use MCQ Tutor, Explain Concept, or Read Text mode.

## Open the live website

**https://mcq-photo-chat-api.shachindeury24.workers.dev/**

The website and API are served by a Cloudflare Worker. The source code is also stored in this GitHub folder.

## First-time setup

The Worker needs two encrypted secrets:

1. `OPENAI_API_KEY`: your OpenAI API key. The Worker uses this key server-side; it is never sent to the browser or stored in GitHub.
2. `APP_ACCESS_TOKEN`: the private app access code. This is separate from your OpenAI key. Paste the access code provided by the site owner into Settings & connection in the website.

To add the OpenAI secret, open Cloudflare → Workers & Pages → `mcq-photo-chat-api` → Settings → Variables and Secrets → Add → Secret. Name it `OPENAI_API_KEY`, paste the key, and save.

Keep both secrets private. Never commit them to this repository. API usage is billed through the OpenAI API account, separately from a ChatGPT subscription; have a parent or guardian manage the API key and billing.

## Features

- Separate saved chat threads in the sidebar.
- Image upload by file picker or drag and drop.
- MCQ Tutor, Explain Concept, and Read Text modes.
- Model selection: GPT-6 Luna, GPT-6.1 Terra, and GPT-6.2 Sol.
- Chat text is saved in this browser. Image files are sent with the current request and are not retained in saved chat history.
- Mobile and desktop layouts. No local build tool or installation required.

## Notes

- This is its own chat app powered by the OpenAI API. It cannot insert a photo into an existing conversation on chatgpt.com.
- AI can misread blurry photos, so check the explanation.
