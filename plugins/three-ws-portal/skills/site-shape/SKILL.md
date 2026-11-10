---
name: site-shape
description: Inspect a website's structure with Portal: the cheap heading outline, or a full 3D world with doors, billboards, a GLB and a walkable link. Use when you need a page's shape rather than its text, or want to turn a site into a 3D scene.
---

# Portal: read a site's shape

Portal reads a public page's structure (headings, section weight, links, images) and lays it out deterministically as a 3D world: sections become buildings, links doors, images billboards. No key or account. Respects robots.txt, identifies as `ThreeWSPortalBot/1.0`, caches a page for an hour, caps HTML at 3 MB with a 12 second deadline.

## MCP tools (registered by this plugin's `.mcp.json`)

- `site_shape` `{ url }`: the cheap read. Title, description, word count, and per section: `heading`, `level`, `words`, `paragraphs`, `code_blocks`, `links`, `images`, `summary`. Use it to compare pages, find thin sections, or decide what to read in full.
- `walk_site` `{ url, include_links? }`: districts, doors (label, href, internal), billboards, a link a human can walk and a GLB URL. `include_links` defaults to true.

Launch by hand: `npx -y -p @three-ws/portal portal-mcp`. Override the API with `PORTAL_API` or `PORTAL_PAGE`.

## CLI

```bash
npx @three-ws/portal three.ws                    # summarize the world
npx @three-ws/portal three.ws --glb site.glb     # save a glTF binary
npx @three-ws/portal three.ws --json world.json  # save the world document
npx @three-ws/portal three.ws --open             # print the walkable link
```

## Library

```js
import { fetchWorld, fetchOutline, fetchWorldGlb, describeWorld, mountPortal, embedSnippet } from '@three-ws/portal';
import { buildWorld, collidersFor } from '@three-ws/portal/layout';

const { world, cached } = await fetchWorld('example.com');
console.log(describeWorld(world)); // { host, sections, doors, tallest }
mountPortal(document.querySelector('#stage'), { url: 'example.com', height: 560 });
```

`buildWorld(outline)` is pure (no network, DOM or three.js); the same URL always builds the same city. Options: `endpoint` (default `https://three.ws/api/portal`), `fetch`, `signal`.

Embed without JS: `<iframe src="https://three.ws/portal?url=example.com&embed=1" width="100%" height="520" style="border:0" loading="lazy" title="Walk example.com in 3D"></iframe>`.

## Errors

`PortalError` carries the API `code`: `invalid_url`, `robots_disallowed`, `blocked_host`, `not_html`, `no_structure`, `too_large`, `unreachable`, `upstream_status`, `rate_limited`. On `robots_disallowed` do not retry or work around it: the site asked crawlers to stay out.
