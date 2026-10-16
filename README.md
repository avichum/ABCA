# ABCA

A "Hello, World!" single-page app built with [Vite](https://vite.dev) and [React](https://react.dev).

## Requirements

- [Node.js](https://nodejs.org) 20.19+ (or 22.12+) and npm

## Getting started

Install dependencies:

```sh
npm install
```

Start the dev server (with hot module replacement) at http://localhost:5173:

```sh
npm run dev
```

## Production build

Build the optimised static bundle into `dist/`:

```sh
npm run build
```

Serve the built bundle locally to check it at http://localhost:4173:

```sh
npm run preview
```

## Project layout

```
index.html        # Vite entry HTML, mounts the app into #root
src/main.jsx      # React entry point
src/App.jsx       # App component (heading + subtitle)
src/index.css     # Global, responsive styling
vite.config.js    # Vite config (React plugin)
```
