# ABCA

A minimal React "Hello World" website, built with [Vite](https://vite.dev/).

## Files

- `index.html` — HTML entry point (mounts the React app into `#root`)
- `src/main.jsx` — React entry point
- `src/App.jsx` — the `App` component that renders the page
- `src/index.css` — styling (responsive, light/dark aware)
- `vite.config.js` — Vite + React plugin configuration
- `eslint.config.js` — ESLint configuration

## Getting started

Requires Node.js 20+ (Node 24 is pinned in `mise.toml`).

```sh
npm install
npm run dev
# then visit the URL printed by Vite (http://localhost:5173 by default)
```

## Scripts

| Command           | What it does                                   |
| ----------------- | ---------------------------------------------- |
| `npm run dev`     | Start the dev server with hot module reloading |
| `npm run build`   | Build the production bundle into `dist/`       |
| `npm run preview` | Serve the production build locally             |
| `npm run lint`    | Lint the source with ESLint                    |

The equivalent [mise](https://mise.jdx.dev/) tasks are also available:
`mise run install`, `mise run dev`, `mise run build`, `mise run lint`.

`npm run build` emits a static bundle in `dist/` that can be served by any
static host.
