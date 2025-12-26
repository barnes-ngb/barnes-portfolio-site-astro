# Portfolio Site (Astro starter)

A minimal, content-first portfolio site intended for:
- a flagship demo/project page
- a “Public references” section for employer work (linking out, not copying assets)
- fast deployment (Vercel / Netlify / GitHub Pages)

## Prereqs
- Node.js 18+ recommended
- npm / pnpm / yarn

## Run locally
```bash
npm install
npm run dev
```

## Build
```bash
npm run build
npm run preview
```

## Deploy
- Vercel: import repo → deploy (static output)
- Netlify: build command `npm run build`, publish directory `dist/`
- GitHub Pages: use an Actions workflow (not included here) or deploy from `dist/`

## Where to edit content
- `src/pages/index.md`
- `src/pages/work/*.md`
- `src/pages/about.md`
- `src/pages/contact.md`

## Notes on employer work
This starter is set up to **link out** to public pages rather than re-hosting employer/client imagery.
See `src/pages/work/zahner-labs.md` for the pattern.

---
Astro dependency pinned to: `^5.16.6` (update anytime).
