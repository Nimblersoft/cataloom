# cataloom — Agent Guide

Conversational Generative UI framework scaffold. Read [README.md](README.md),
[architecture](docs/ARCHITECTURE.md), and [contribution guidance](CONTRIBUTING.md) before changes.
Distinguish proposed architecture from implemented behavior.

## Documentation lifecycle

Keep specs and non-ADR docs current-state only, except `CHANGELOG.md`, the release-history SSOT.
Collect pending changes under `[Unreleased]`, preserve published release entries, and group them
by actual version and release date; never invent prior releases. ADRs own decision rationale:
before release they may be edited, merged, or squashed; after release preserve published ADRs
and record later decisions in a new ADR with `supersedes`. Apply `context-hygiene` before
documentation or spec writes; link to the owning SSOT rather than duplicating it. Git and Plane
own commit and work-item detail.
