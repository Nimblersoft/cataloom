# cataloom

**Turn any catalog into a conversation.**

cataloom is an open-source **Generative UI** framework for building conversational,
agentic-RAG websites. Instead of a search box and a grid of results, visitors describe
what they want in plain language — *"SUV automática, menos de $25k, poco kilometraje"* —
and cataloom retrieves matching items from your content and **renders live, interactive UI
cards** (results, comparisons, quick replies, lead capture) directly in the chat.

It is stack-native to Cloudflare Workers and built around a small, pluggable core so that
each domain — cars, real estate, professional services, anything with a catalog — ships as
its own **vertical plugin**.

> **Status: early / bootstrapping.** This repo is the foundation. The first vertical plugin
> (an automotive "AI Car Finder", available as an optional seed) and the core engine are
> being built out. Contributions and new vertical plugins are welcome — see
> [CONTRIBUTING.md](CONTRIBUTING.md).

## Why

Traditional catalog sites bury intent under filters and forms. A conversational, generative
interface:

- **lifts conversion** — visitors state intent naturally and get an answer, not a filter maze;
- **grounds every answer in your content** (retrieval-augmented) so the UI never invents a
  price or a spec;
- **renders real UI, not just text** — cards, comparisons, and calls-to-action are generated
  per turn from the actual result set.

## How it works

```
User intent (natural language)
        │
        ▼
  Retrieval (Agentic RAG over your catalog content)
        │
        ▼
  Generative UI response  ──►  a validated UI-component message
        │                       (cards · comparisons · quick replies · lead capture)
        ▼
  Rendered live in the chat surface
```

- **Content in, UI out.** Your catalog lives as structured content; retrieval grounds the
  model on it; the model responds with a **UI message** (a declarative component array),
  validated before it ever reaches the browser.
- **Pluggable verticals.** The core knows nothing about cars or houses. A vertical plugin
  supplies its content schema, retrieval mapping, and the cards it wants rendered.
- **Optional seed content.** Ship an empty core, or seed a working demo (e.g. the automotive
  catalog) so newcomers get a running example in one command.

## Tech direction

- **Edge-native**: Cloudflare Workers (frontend + backend), zero-server.
- **Retrieval**: managed hybrid search over the catalog content.
- **Generative UI**: a declarative, validated component protocol (the model returns UI, not HTML).
- **Frontend**: SvelteKit SSR. **Backend**: Hono + TypeScript.

The concrete architecture and the first milestone plan live in
[`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

## Roadmap (short)

1. **Core engine** — content seam, retrieval, generative-UI response + validator, chat surface.
2. **First vertical plugin** — automotive "AI Car Finder" (optional seed content).
3. **Plugin API** — stabilize the contract so the community can add verticals (real estate,
   professional services, …).

## License

[MIT](LICENSE) — © Nimblersoft. Use it, fork it, build on it.
