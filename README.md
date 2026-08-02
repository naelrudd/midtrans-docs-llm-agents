# Midtrans Docs for LLM Agents

An unofficial, machine-readable mirror of the official [Midtrans payment gateway documentation](https://docs.midtrans.com/) — all pages converted to plain Markdown so AI coding assistants, LLM agents, RAG pipelines, and vector stores can consume them without scraping or HTML parsing.

Midtrans is the leading payment gateway in Indonesia. This repo lets any agent answer integration questions (Snap Checkout, Core API, payment methods, webhooks, error codes, sandbox testing, and more) from first-party documentation text.

## Why this exists

- Official docs ship an `llms.txt` index but not a plain cloneable corpus.
- Agents often need to read many doc pages during integration work; a local, structured Markdown mirror is faster and more reliable than live-fetching 590 pages.
- Deterministic snapshot: pin a commit and know exactly what docs your agent is reading.

## How to use

Point your agent at this repo (or a subfolder). Suggested flow:

1. **Discover** — read [`llms.txt`](llms.txt) (or `INDEX.md`) for the full page catalog with titles.
2. **Read** — load any page directly, e.g. `docs/snap.md`, `docs/coreapi-card-payment-integration.md`, `reference/backend-integration.md`.
3. **Embed/index** — feed `docs/`, `reference/`, `recipes/`, `changelog/` into your vector store or context window.

For AI agents, also consider Midtrans' own [agent skills.md](https://docs.midtrans.com/docs/building-on-midtrans-with-ai).

### Quick index

| Section | Contents |
|---------|----------|
| [`docs/`](docs/) | Step-by-step integration guides (Snap, Core API, Payment Link, webhooks, sandbox, errors, merchant dashboard, FAQ) — EN + ID |
| [`reference/`](reference/) | API reference pages (Snap API, Core API, Invoicing, GoPay ID, OneKYC, Esign, etc.) |
| [`recipes/`](recipes/) | Copy-paste integration recipes |
| [`changelog/`](changelog/) | Product release notes |
| [`llms.txt`](llms.txt) | Official full page index (markdown + OpenAPI endpoints) |

## RAG Starter Kit

Local semantic search over the docs:

```bash
pip install chromadb
python rag.py build                    # index Markdown pages into ./rag_chroma
python rag.py query "your question"    # retrieve top-k relevant chunks
python rag.py info                     # corpus stats
```

Re-running `build` is idempotent and incremental.

## Updating

Re-mirror from the official index:

```bash
curl -sL -o llms.txt https://docs.midtrans.com/llms.txt
# parse each https://docs.midtrans.com/*.md link in llms.txt and download
```

## License & attribution

- This repository is **not affiliated with, endorsed by, or sponsored by Midtrans / PT Midtrans (GoTo Group)**.
- All documentation content is © Midtrans and belongs to its respective owners.
- It mirrors the official [Midtrans Documentation](https://docs.midtrans.com/), which serves these pages as Markdown via `llms.txt` specifically for AI consumption.
- This repo is provided "as is" for reference/educational purposes. Refer to [docs.midtrans.com](https://docs.midtrans.com/) for authoritative, always-current documentation.
- No API keys, server keys, or secrets are (or should be) stored here.
