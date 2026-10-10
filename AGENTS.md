# AGENTS.md

Instructions for AI coding agents working in or with `@three-ws/portal`.

## What this is

Turn any website into a walkable 3D world. Reads a page's real structure and lays out a city from it: sections become buildings, links become doors, images become billboards. Pure layout in JS, a client for the three.ws Portal API, a CLI, and an MCP server.

## Use it

```bash
npm install @three-ws/portal
```

Full API reference: [README.md](README.md). Machine-readable summary: [llms.txt](llms.txt). Full text: [llms-full.txt](llms-full.txt).

## Work on it

- Node 20 or newer, ESM only.
- Run the tests with `npm test` before proposing a change.
- Keep runtime dependencies at their current count. Prefer a well-maintained library over new hand-rolled code, and say why in the pull request.
- No mocks, placeholders or TODO comments in committed code.
- Do not use em-dashes or en-dashes in code, comments or docs.

## Source of truth

This repository is exported from https://github.com/nirholas/three.ws/tree/main/packages/portal. Bug reports belong here; larger changes should be proposed against the monorepo path.
