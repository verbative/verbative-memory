# Verbative Memory

On-device memory system for AI coding agents — a **dual-layer engine** (distilled facts + a
lossless event ledger), automatically captured and injected, exposed over **MCP**. Shared
across agents, persistent across sessions; stored as plain, human-readable files in your repo —
no memory cloud, no vendor database.

> This repository is the public home for **docs, install help, and issues**. The engine is
> closed-source and ships as a sealed, compiled package — there is **no source code here**.

## How it works — capture everything, recall selectively

- **Complete capture, in two layers.** Underneath sits a lossless ledger: a mechanical,
  no-model record of every command, edit, and test result, so "what did we run" and "when did
  this test start failing" are exact, replayable facts. On top, an on-device model distills that
  stream into atomic, typed memories — decisions, conventions, and dead ends.
- **Selective recall — the two layers fused.** A single recall surfaces only the handful of
  distilled facts that matter (ranked by semantic search and a reranker) and interleaves them,
  by time, with the exact ledger record around them: what you *decided* next to what you
  *actually did*. One answer, not a dump of the whole history.
- **Self-organizing.** New facts reconcile against old ones, importance decays on per-type
  forgetting curves, frequently-recalled facts strengthen, and recurring specifics distill into
  higher-level insights.
- **Yours, on-device.** Memories live in human-readable files in your project. Recall makes
  zero cloud calls.

## Requirements

- **macOS (Apple silicon) or Windows 10/11 (x64).** (Linux is on the roadmap.)
- A **Verbative account** — Memory is part of the **Code Advanced** plan and starts with a
  **14-day free trial**. See the [plans](https://verbative.de/pricing) and the
  [Terms](https://verbative.de/legal/terms).

## Install

**Claude Code CLI** — automatic capture and recall:

```bash
claude mcp add verbative-memory -- npx -y verbative-memory
```

**pip:**

```bash
pip install verbative-memory
verbative-memory login      # sign in with your Verbative account
```

**Any MCP client** (`mcp.json` / stdio):

```json
{ "mcpServers": { "verbative-memory": { "command": "npx", "args": ["-y", "verbative-memory"] } } }
```

Automatic capture and injection are built for the **Claude Code CLI** and **Codex**; any other
Model Context Protocol client can call the tools manually. The first run downloads the on-device
engine and models once; after that, recall runs fully offline.

More detail in [docs/INSTALL.md](./docs/INSTALL.md) and at
[verbative.de/docs/memory](https://verbative.de/docs/memory).

## Tools

`remember` · `recall` · `search` · `ask` · `list` · `get` · `pin` · `forget` · `revise` ·
`edit_core` · `feedback` · `related` · `history` · `timeline` · `events` — and more. See the
[docs](https://verbative.de/docs/memory).

## Privacy

Capture, embeddings, reranking, and the knowledge graph all run locally. Your code and memories
are not uploaded; the memory files stay in your project and leave your machine only if you
choose to share them.

## Links

- Overview — https://verbative.de/memory
- Docs — https://verbative.de/docs/memory
- Plans — https://verbative.de/pricing
- Terms — https://verbative.de/legal/terms
- Impressum — https://verbative.de/legal/impressum

## Issues

Bug reports and feature requests are welcome in the [issue tracker](../../issues) — the place
for anything about the docs or the tool. For your account, licensing, or a trial, email
info@verbative.de.

---

*Verbative is a product of Cramer Digital. Not affiliated with, or endorsed by, Anthropic.
Verbative works alongside Anthropic's Claude and the Claude Code CLI; those names belong to
Anthropic. See [LICENSE](./LICENSE).*
