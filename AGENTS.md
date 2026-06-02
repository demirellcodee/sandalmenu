# AGENTS.md

## Cursor Cloud specific instructions

### Product overview

Static single-page marketing site for **Sandal Kafe** (Turkish café). No backend, database, build step, or package manager. Primary entry point: `index.html` at repo root. A duplicate draft copy lives in `site--taslak/` (not required for dev).

### Services

| Service | Required | How to run |
|---------|----------|------------|
| Static HTTP server | Yes | From repo root: `python3 -m http.server 8080 --bind 127.0.0.1` then open `http://127.0.0.1:8080/` |

Use a tmux session for long-running servers (see Cloud Agent shell docs). No Docker, Node, or npm.

### Lint / test / build

There is no project-defined lint, test, or build pipeline. Optional sanity checks:

- `python3 -m http.server` + `curl http://127.0.0.1:8080/` (expect `200`)
- Parse `index.html` with Python's `html.parser` for basic well-formedness

### External dependencies (browser)

AOS animations and Google Fonts load from CDNs at runtime. Offline or blocked CDN only affects animations/fonts; navigation and menu content still work.

### Hello-world verification

1. Serve from `/workspace` (not `site--taslak/` unless testing the draft).
2. Confirm hero "SANDAL KAFE" and **Menüyü Gör**.
3. Open a menu category (e.g. **yemekler**) and verify priced items.
4. At mobile width, open the hamburger and use nav links (**Hakkımızda**, **İletişim**).

### Gotchas

- One menu card references `images/hamburger.jpg`, which is not in the repo; that card may show without a background image.
- Hash anchors use Turkish characters (e.g. `#hakkımızda`, `#sıcakiçecek`); match exact IDs in `index.html`.
