# MCQ Studio

A responsive image-to-chat study assistant. Upload a question photo to the selected chat, then use MCQ Tutor, Explain Concept, or Read Text mode.

## Open the website

This app lives in the mcq-chat folder of the Free-upload repository. Enable GitHub Pages:

1. Open Settings → Pages.
2. Under Build and deployment, choose Deploy from a branch.
3. Select branch main and folder /(root), then Save.
4. Open https://sd201826.github.io/Free-upload/mcq-chat/

## Connect the OpenAI API

The front end calls the Cloudflare Worker at:

https://mcq-photo-chat-api.shachindeury24.workers.dev

The Worker is deployed as mcq-photo-chat-api. To activate it:

1. Open the Cloudflare dashboard and select Workers & Pages.
2. Open mcq-photo-chat-api.
3. Go to Settings → Variables and Secrets.
4. Add an encrypted Secret named OPENAI_API_KEY, paste your own OpenAI API key, and save.
5. Return to the website and refresh. The status should change to API connected.

Do not put the API key in this repository, in app.js, or in a public HTML file. The browser never receives the key; the Worker reads it as a secret.

## Features

- Multiple chats in a sidebar. Uploads go to the currently selected chat.
- Photo upload by file picker or drag and drop.
- MCQ Tutor, Explain Concept, and Read Text modes.
- Model selection: GPT-6 Luna, GPT-6.1 Terra, and GPT-6.2 Sol.
- Chat text is saved in this browser. Image files are sent with the current request and are not retained in saved chat history.
- Mobile and desktop layouts. No build tool or local install required.

## Notes

- This is a separate chat app powered by the OpenAI API. It cannot append messages to an existing conversation inside chatgpt.com.
- API requests are billed through your OpenAI API account. A ChatGPT plan and API billing are separate.
- AI can misread unclear photos, so check the reasoning.
- The Worker allows the GitHub Pages origin https://sd201826.github.io and localhost development origins.
