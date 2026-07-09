# Contributing to cataloom

cataloom is built to grow through community contributions — especially **new vertical
plugins**. Whether you're fixing a bug in the core or adding a whole new domain, welcome.

## Ways to contribute

- **Core engine** — retrieval, the generative-UI response/validator, the chat surface,
  developer ergonomics.
- **Vertical plugins** — a new domain (real estate, restaurants, travel, professional
  services, e-commerce, …). A vertical supplies its content schema, its retrieval mapping,
  and the UI cards it renders. The core stays domain-agnostic.
- **Seed content** — optional example catalogs so newcomers get a running demo fast.
- **Docs & examples** — guides, recipes, and reference deployments.

## Ground rules

- **Grounding is non-negotiable.** The interface must never present a value (price, spec,
  availability) that isn't traceable to retrieved content. If retrieval finds nothing, say so
  — don't invent.
- **UI responses are validated.** Every generative-UI message must pass validation before it
  reaches the browser. Don't bypass the validator.
- **Keep the core domain-agnostic.** Domain knowledge belongs in a plugin, never in the core.
- **No secrets in the repo.** Use `.env` / platform secrets; never commit tokens or keys.

## Getting started

1. Fork and clone.
2. Read [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the intended structure and the
   plugin contract.
3. Open an issue describing what you want to build (a new vertical, a fix, an improvement)
   before large changes, so we can align on the plugin API.
4. Send a focused pull request. Small, reviewable PRs merge fastest.

## Adding a vertical plugin (sketch)

A vertical plugin declares:

- a **content schema** (the fields your catalog items carry),
- a **retrieval mapping** (which fields are filterable vs. semantically searched),
- the **UI cards** it renders (result card, comparison, CTA, …).

The stable plugin contract is being defined alongside the first automotive plugin; track
[`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) and the open issues for its shape.

## Code of conduct

Participation is governed by our [Code of Conduct](CODE_OF_CONDUCT.md).
