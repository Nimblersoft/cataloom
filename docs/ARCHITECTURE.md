# cataloom — architecture & vision

> This document captures the intended shape of cataloom. It is a living design doc; the
> concrete milestone plan is tracked in the issue tracker. Nothing here is frozen until the
> plugin API ships with the first vertical.

## The idea

cataloom turns a **catalog** (a set of structured items with descriptive content) into a
**generative, conversational interface**. A visitor expresses intent in natural language; the
system retrieves matching items from the catalog and responds with **live, interactive UI** —
not a wall of text, and not a static results grid, but generated component cards for that turn.

Two invariants define the product:

1. **Grounded** — every rendered value is traceable to retrieved content. No invented prices,
   specs, or availability. Empty retrieval → an honest "no match", never a hallucination.
2. **Validated UI** — the model returns a declarative component message that is validated
   against a known catalog of components before it is rendered.

## The layers

```
┌─────────────────────────────────────────────────────────────┐
│ Frontend (SvelteKit SSR)                                     │
│   chat surface · renders the validated generative-UI message │
└───────────────▲─────────────────────────────────────────────┘
                │  service binding
┌───────────────┴─────────────────────────────────────────────┐
│ Backend (Hono + TypeScript, Cloudflare Worker)               │
│   ┌─────────────┐   ┌───────────────┐   ┌──────────────────┐ │
│   │ Content seam│──►│  Retrieval    │──►│ Generative-UI    │ │
│   │ (catalog)   │   │  (hybrid RAG) │   │ response + valid.│ │
│   └─────────────┘   └───────────────┘   └──────────────────┘ │
│                 lead capture · async side-effects            │
└──────────────────────────────────────────────────────────────┘
        Cloudflare-native storage + managed hybrid search
```

- **Content seam** — the catalog is read through one interface, so the source (files, a CMS,
  a database) is swappable. Verticals declare their content schema here.
- **Retrieval** — managed hybrid (keyword + semantic) search grounds the model on the actual
  catalog. Structured fields become filters; prose becomes semantic recall.
- **Generative-UI response + validator** — the model returns a declarative component array
  (message, result cards, comparison, quick replies, CTAs). A validator enforces the
  component catalog and structural rules before render.
- **Lead capture** — high-intent conversations hand off to a lead/booking flow, with PII
  handled safely (masked before any model call).

## The plugin model

The **core** is domain-agnostic. A **vertical plugin** provides:

| Contribution        | What it declares                                                        |
|---------------------|-------------------------------------------------------------------------|
| Content schema      | The fields a catalog item carries (and which are filterable vs. semantic)|
| Retrieval mapping   | How intent maps onto filters + semantic query                           |
| UI cards            | The components this domain renders (result card, comparison, CTA, …)     |
| Optional seed       | Example catalog content so the plugin runs out of the box               |

Target verticals (community-extensible): **automotive** (first), **real estate**,
**professional services**, and beyond.

## Intended repository structure (provisional)

```
cataloom/
  packages/
    core/            # domain-agnostic engine: content seam, retrieval, gen-UI + validator
  plugins/
    automotive/      # first vertical plugin (AI Car Finder) + optional seed catalog
  apps/
    frontend/        # SvelteKit SSR chat surface
    backend/         # Hono worker wiring core + enabled plugins
  docs/
```

> The exact layout is finalized in the bootstrap milestone plan; this is the direction, not a
> commitment.

## First milestone

1. Stand up the core engine (content seam → retrieval → generative-UI response + validator →
   chat surface) with a minimal built-in demo.
2. Extract the automotive domain into the **first vertical plugin**, with optional seed
   content (the "AI Car Finder").
3. Harden and document the **plugin contract** so the community can add new verticals.
