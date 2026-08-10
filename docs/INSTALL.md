# Installing Verbative Memory

Verbative Memory is a local MCP server. It runs entirely on your machine; the first launch
downloads the on-device engine and models once, then works offline.

The canonical, always-current guide lives at
[verbative.de/docs/memory](https://verbative.de/docs/memory) — this file is a quick mirror.

## Requirements

- **macOS (Apple silicon) or Windows 10/11 (x64).** Linux is on the roadmap.
- **Node.js ≥ 18** (for the `npx` launcher) or **Python ≥ 3.10** (for `pip`).
- A **Verbative account**. Memory is part of the **Code Advanced** plan and starts with a
  **14-day free trial**; see [verbative.de/pricing](https://verbative.de/pricing).
- ~4 GB of disk for the on-device models (downloaded once). An optional **on-device reader
  model** (it powers `ask`) — sized to your machine's RAM, from a few GB up to ~19 GB on
  high-RAM machines — downloads on first use, or up front via `verbative-memory setup`.

## Option A — Claude Code CLI (recommended)

Automatic capture and recall, wired into your sessions:

```bash
claude mcp add verbative-memory -- npx -y verbative-memory
```

Then sign in when prompted (or run `npx verbative-memory login`).

## Option B — pip

```bash
pip install verbative-memory
verbative-memory login        # sign in with your Verbative account
verbative-memory setup        # (optional) download the models up front
```

The `verbative-memory` (or `vbm`) command runs the MCP server for any client configured to
launch it.

## Option C — any MCP client

The tools work in any Model Context Protocol client. Point it at the launcher:

```json
{
  "mcpServers": {
    "verbative-memory": { "command": "npx", "args": ["-y", "verbative-memory"] }
  }
}
```

Automatic capture and injection are built for the **Claude Code CLI** and **Codex**. Other MCP
clients can call the tools manually (`remember`, `recall`, `search`, and the rest).

## First run

The first launch downloads the engine and models (one time, ~4 GB): the sealed engine core and
the local model runtime from the official
[release repository](https://github.com/verbative/verbative-dist), plus the on-device
embedding, reranker, and extractor models from their official Hugging Face repos. The engine
core, runtime, and these three models are each verified against a pinned SHA-256 before they
are used. After that, recall runs with zero network calls. If you are offline on first run,
the download is deferred until you have a connection.

The optional **on-device reader model** (used by `ask`) is separate: it downloads on first
use (or with `verbative-memory setup`), and its size depends on your RAM — the largest tier
is ~19 GB, so fetch it on a connection you trust to stay up.

## Verifying it works

- `verbative-memory login` should report your plan (Code Advanced, or an active trial).
- In your MCP client, calling `remember` then `search` should round-trip a fact.

## Troubleshooting

- **"Models ✓" but search returns nothing** — the local model runtime may not be on the path
  yet; re-run `verbative-memory setup` to fetch it, then restart the server.
- **"no reader model" after a long download** — the reader download does not resume yet, so an
  interrupted transfer starts over. Re-run `verbative-memory setup` on a stable connection; the
  reader is optional — only `ask` needs it, everything else works without it.
- **Install fails with "no matching distribution" (pip)** — the package ships as sealed,
  per-version platform wheels (macOS Apple silicon and Windows x64). Confirm you are on a
  supported platform with a supported Python (3.10–3.14).
- **Anything account- or billing-related** — email info@verbative.de.

Full docs and current benchmarks: [verbative.de/docs/memory](https://verbative.de/docs/memory).
