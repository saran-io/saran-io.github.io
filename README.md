# Astro Starter Kit: Minimal

```sh
npm create astro@latest -- --template minimal
```

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## Blog diagrams

Technical posts use **hand-authored SVG** in `public/blog/<slug>/` so figures stay sharp on retina and match site typography (see `building-gpt2-from-scratch`).

Other options worth knowing:

| Tool | Best for |
|------|-----------|
| **[D2](https://d2lang.com/)** (CLI) | Clean architecture diagrams from code; versionable `.d2` files |
| **[Mermaid](https://mermaid.js.org/)** | Quick diagrams in Markdown; Astro can render via `rehype-mermaid` or pre-render with `@mermaid-js/mermaid-cli` |
| **[Excalidraw](https://excalidraw.com/)** | Sketched style, great for talks; export SVG |
| **[Penpot](https://penpot.app/) / Figma** | Full design control; export SVG or PNG |

This repo does not bundle a diagram plugin by default; add one with `astro add` or a Markdown `rehype` plugin if you want Mermaid in `.md` files.

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).
