# momv-conceptual

The conceptual / explanatory companion to **Mountain of Many Voices**
([`ZZYW/momv`](https://github.com/ZZYW/momv)). Right now it holds a single
printable letter-sized flyer that explains how MoMV works.

## Layout

```
flyer/
  index.html   # the page (HTML + inline CSS + a small content loader)
  content.md   # the copy — sections in [SECTION NAME] blocks
```

`index.html` fetches `content.md` at runtime and populates the masthead,
intro paragraphs, section heading, footer, and the eight numbered callouts
around the ring diagram. To change wording, edit `content.md`; to change
layout, edit `index.html`.

Hidden authoring helper: **Shift+D+A** toggles a drag/resize mode on the
live page that lets you reposition the eight callout blocks and copies
the new CSS to your clipboard.

## How this is deployed

This repo is **not standalone in production** — it is served as a static
slice of `momv.zzyw.org` via nginx:

- Live URL: <https://momv.zzyw.org/conceptual/flyer/>
- VPS path: `/var/www/momv-conceptual` (served by nginx `alias`)
- Auto-deploy: push to `main` → GitHub webhook
  (`momv.zzyw.org/conceptual/flyer-webhook`) →
  `momv-conceptual-webhook.service` runs `webhook.cjs`, which `git pull`s
  this directory. No build step, no service restart.

Full deploy topology (including the game app and its separate webhook) is
documented in the main repo's README under **Production Deployment**:
<https://github.com/ZZYW/momv#production-deployment-momvzzyworg>

## Cross-links

The flyer's top-left "← return to game" button uses `history.back()`, so
visitors who clicked through from a station return to their exact
passage. The matching "What is this? How does it work?" chip on the
stations lives in the main `momv` repo.
