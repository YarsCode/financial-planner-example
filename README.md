# Financial Products Planning Dashboard

> A drag-and-drop tool for financial planners to build tailored service packages for their clients — and export the result as a polished Word document, ready to send.

[**Live Demo →**](https://yarson-ai.github.io/financial-planner-example/)

> **Note:** This is a public demo replica of a real product I built for a private client. The original is in active use behind closed doors, so I rebuilt a representative version here for portfolio purposes. Branding, product data, and copy have been generalized.

---

## Table of Contents

- [Overview](#overview)
- [Who it's for](#who-its-for)
- [How it works](#how-it-works)
- [The user flow](#the-user-flow)
- [Tech stack](#tech-stack)
- [Getting started](#getting-started)
- [Project structure](#project-structure)
- [Deployment](#deployment)
- [About the author](#about-the-author)
- [License](#license)

---

## Overview

The Financial Products Planning Dashboard helps a financial planner sit down with a client and visually assemble the exact mix of services that fits the client's situation — basic guidance, quarterly check-ins, semi-annual reviews, or full annual planning. Instead of juggling spreadsheets or static price lists, the planner drags products from a categorized catalog into the client's plan, sees pricing update live, and exports the finished proposal as a branded Word document in one click.

The interface is in **Hebrew (RTL)**, matching the original client's market.

## Who it's for

- **Business owners** evaluating whether this kind of tool fits their advisory workflow
- **Financial planners and consultants** who want a faster, more visual way to scope client engagements
- **Developers and recruiters** browsing my work to see how I build production React applications

## How it works

At the highest level, the app is a single-page React application with three concerns:

1. **A categorized product catalog** rendered on the left side of the screen
2. **A live "chosen products" board** on the right that the planner builds up via drag-and-drop
3. **A Word document generator** that merges the chosen plan into a pre-designed `.docx` template

There is no backend. Everything runs in the browser, which keeps the tool fast, cheap to host, and trivially deployable. Client data never leaves the planner's device.

### The user flow

1. **Authentication** — A lightweight password gate keeps the tool private to the planner.
2. **Browse products** — Products are grouped by category. Each card shows a name, short description (expandable), and price.
3. **Build the plan** — The planner drags products onto the client's board. The board calculates a running monthly total and a grand total automatically.
4. **Enter client details** — Name and phone number are captured and validated (Israeli phone format).
5. **Export** — One click generates a Word document from `planningTemplate.docx`, populated with the client's name, the selected products, and the calculated totals. The file downloads instantly.
6. **Reset** — A reset action clears the board for the next client.

### Why drag-and-drop?

Selecting from a long list with checkboxes works, but it doesn't *feel* like planning. Dragging a service into a client's plan mirrors the conversational nature of the meeting — "let's add this, drop that, swap these two" — and makes the resulting plan feel earned rather than configured.

## Tech stack

| Layer | Tool | Why |
|---|---|---|
| **Framework** | [React 18](https://react.dev/) | Component model fits the catalog/board split cleanly |
| **Build tool** | [Vite](https://vitejs.dev/) | Fast dev server, tiny production bundles |
| **Language** | TypeScript | Type safety on product/plan shapes |
| **Drag & drop** | [@dnd-kit](https://dndkit.com/) | Accessible, modern DnD with great touch support |
| **Document generation** | [docxtemplater](https://docxtemplater.com/) + [PizZip](https://github.com/Stuk/jszip) | Merge plan data into a real `.docx` template, in-browser |
| **Linting** | ESLint + `@typescript-eslint` | Standard quality gates |
| **Hosting** | GitHub Pages | Free, fast, and good enough for a static SPA |

**No backend, no database, no analytics, no tracking.** The entire app is static files served from a CDN.

## Getting started

### Prerequisites

- **Node.js** ≥ 18
- **npm** (or `pnpm` / `yarn` if you prefer)

### Install and run locally

```bash
# 1. Clone the repository
git clone https://github.com/YarsCode/financial-planner-example.git
cd financial-planner-example

# 2. Install dependencies
npm install

# 3. Start the dev server
npm run dev
```

The dev server runs at `http://localhost:5173/financial-planner-example/`.

### Available scripts

| Command | What it does |
|---|---|
| `npm run dev` | Start the Vite dev server with hot reload |
| `npm run build` | Type-check and produce a production build in `dist/` |
| `npm run lint` | Run ESLint across the project |
| `npm run preview` | Serve the production build locally for a final check |

### Customizing the Word template

The export feature is driven by `planningTemplate.docx` in the repo root. Open it in Microsoft Word or any compatible editor and edit freely — just preserve the `{placeholder}` tokens (e.g. `{customerName}`, `{products}`, `{totalSum}`). Docxtemplater fills these in at export time.

## Project structure

```
financial-planner-example/
├── assets/                  # Built JS/CSS bundles (output of `npm run build`)
├── index.html               # SPA entry point
├── planningTemplate.docx    # Word template merged with client data at export
├── background.png           # Login screen background
├── vite.svg                 # Favicon
├── .eslintrc.cjs            # ESLint configuration
└── .gitignore
```

## Deployment

The demo is hosted on **GitHub Pages**, configured via Vite's `base` option (`/financial-planner-example/`). The build output in `dist/` is published to the `gh-pages` branch (or the `/docs` folder, depending on your preference). Any static host — Netlify, Vercel, Cloudflare Pages, S3 — works equally well; just adjust the `base` path in `vite.config.ts` to match your hosting setup.

## About the author

Built by **Yarson** — a full-stack web developer who builds custom React and TypeScript applications for businesses that have outgrown off-the-shelf tools.

- 🌐 Portfolio: [yarson.dev](https://yarson.dev)
- 💼 LinkedIn: [linkedin.com/in/yarson](https://www.linkedin.com/in/yarson/)
- 💻 GitHub: [@YarsCode](https://github.com/YarsCode)

If you're a business owner with a workflow that doesn't fit any existing tool, I'd love to hear about it.

## License

Released under the [MIT License](LICENSE). Use it, fork it, learn from it — attribution appreciated but not required.
