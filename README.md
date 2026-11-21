# Gift Benedict Seilane — Portfolio

A software engineering portfolio with project links, a downloadable CV, and Nova, a holographic AI guide. The independent GitHub repository is the source of truth; Cloudflare Workers serves both the site and Nova's `/api` endpoints from one origin.

## Run locally

Open `index.html` for the local portfolio guide. For a Cloudflare-compatible preview, run `npx wrangler dev` from the repository root. Microphone access requires HTTPS or localhost and explicit visitor permission.

## Deploy to Cloudflare

1. Keep the Worker on Cloudflare's **Free** plan and authenticate Wrangler with `npx wrangler login`.
2. From the repository root, deploy the site and Worker together with `npx wrangler deploy`. The root Wrangler config points static assets at the repository root while `.assetsignore` keeps source/configuration files out of the public asset bundle.
3. Connect the independent GitHub repository to Cloudflare Workers Builds and use `npx wrangler deploy` as the deploy command. This deploys future commits from `main` automatically. The `nova-api` setting defaults to `same-origin`, so no API URL or CORS update is needed.
4. To enable internet search, add a Brave Search API key as a Worker secret from the repository root: `npx wrangler secret put BRAVE_SEARCH_API_KEY`. Keep secrets in Cloudflare, never in the repository or website. Search is unavailable until this optional secret is configured.

Workers AI has a free daily allocation of 10,000 Neurons; AI requests stop when the free quota is exhausted. Brave advertises up to $20 in free monthly calls; use only the free allowance and do not add prepaid credits or enable a paid plan.

Nova uses Cloudflare Workers AI (`gpt-oss-20b`) for conversation, Whisper Large v3 Turbo for microphone transcription, and Deepgram Aura-2 for natural English speech. Its tools return allowlisted project, GitHub, LinkedIn, CV, and email links. Voice recordings are sent to the Worker only after the visitor presses the microphone button. Web queries go to Brave only when Nova searches.

The assistant uses transcript module names and topics, not student identifiers or grades. South African language output depends on model coverage and may vary, especially for lower-resource languages. English can use Aura-2's natural voice within the free AI quota. Other spoken languages use voices installed on the visitor's device; availability and quality vary by language and browser.

The supplied CV is included at `assets/Gift-Benedict-Seilane-CV.pdf` for the public download link.
