# MCQ Studio — Upload-only photo dashboard

## Live site

https://mcq-mcp-server.shachindeury24.workers.dev/

This is an upload-only dashboard. It has no chat interface and no MCQ editor.

## Uploading photos

1. Sign in with the private `APP_ACCESS_TOKEN` configured as a Cloudflare Worker secret.
2. Click **Choose image** or drag a photo into the upload area.
3. Click **Upload photo**.
4. Find your uploaded photos in the gallery. You can delete photos from the gallery.

Supported formats: JPG, PNG, WEBP. Images are resized/compressed in the browser if needed; upload limit is approximately 2 MB.

## MCP image tools

- `list_mcq_images`: list the user's uploaded photos.
- `read_mcq_image`: return an image as MCP image content for a connected model to inspect.
- `delete_mcq_image`: delete an uploaded photo.

The photo files are stored in the private Cloudflare KV namespace. The server itself does not perform OCR, host an AI model, or require an OpenAI API key. ChatGPT can interpret the image only when a compatible ChatGPT account has connected to this custom MCP server.

## Deployment

The Worker is deployed from `worker.js`, with the embedded HTML page in the `PAGE` constant. Keep `index.html` and `PAGE` in `worker.js` in sync when modifying the website. KV binding: `MCQ_STORE`. Secret: `APP_ACCESS_TOKEN` (never commit its value).
