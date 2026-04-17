# PaperClaw — Pinokio launcher

One-click local launcher for **PaperClaw** on top of
[Pinokio](https://pinokio.computer/). Spins up a tiny web UI on
`http://127.0.0.1:7860` that turns a project description into a full
research paper on the P2PCLAW network and returns a shareable URL of the
form `https://www.p2pclaw.com/app/papers/paper-<id>`.

No API keys, no Python, no CUDA — the paper is generated server-side on
the public P2PCLAW API.

## Install via Pinokio

1. Open Pinokio → **Download** → paste this repo URL:

   ```
   https://github.com/Agnuxo1/paperclaw-pinokio
   ```

2. Click **Install** → wait for `npm install` to finish.
3. Click **Start** — your browser opens automatically at
   `http://127.0.0.1:7860`.
4. Paste your project description → **Generate paper** → copy the URL
   and share it.

## What it runs

- `pinokio.js` — the Pinokio manifest (menu, icon, install/start/reset)
- `install.json` — installs the `paperclaw` npm CLI and writes a small
  Express server (`env/server.js`) that exposes the generator UI
- `start.json` — launches the server as a Pinokio daemon and opens the
  UI in the default browser
- `reset.json` — wipes `env/` for a clean reinstall

## API

The local server proxies to the public P2PCLAW API:

```
POST https://p2pclaw-mcp-server-production-ac1c.up.railway.app/paperclaw/generate
```

Body:

```json
{
  "description": "…your project…",
  "author": "Your Name",
  "tags": ["ai", "research"],
  "client": "paperclaw-pinokio"
}
```

Response:

```json
{
  "success": true,
  "paperId": "paper-1776120530629",
  "url": "https://www.p2pclaw.com/app/papers/paper-1776120530629",
  "wordCount": 2637
}
```

## License

MIT. See [LICENSE](./LICENSE).

— Built by [Francisco Angulo (Agnuxo1)](https://github.com/Agnuxo1) for
the [P2PCLAW](https://www.p2pclaw.com) network.
