# MOTAZ — Creative Developer Portfolio

An experimental, editorial portfolio for **Motaz**, a creative developer and designer studying
Italian Language. The site pairs large expressive typography with an animated 3D canvas object,
mouse-driven 3D project cards and scroll-triggered motion.

Built with React + Vite. No template, no page builder.

---

## Stack

| Layer      | Choice                                    |
| ---------- | ----------------------------------------- |
| Framework  | React 18                                  |
| Build tool | Vite 6                                    |
| Motion     | GSAP + ScrollTrigger                      |
| Icons      | Lucide React                              |
| Styling    | Hand-written CSS (tokens + section files) |
| 3D         | Canvas 2D with hand-computed 3D projection |

The hero object is not a Three.js scene: it is a torus-knot point cloud rotated and projected with
perspective math in a canvas, which keeps the page light while still being genuinely three-dimensional.

---

## Commands

```bash
npm install      # install dependencies
npm run dev      # local dev server on http://localhost:3000
npm run build    # production build into dist/
npm run preview  # serve the production build
```

---

## Structure

```
index.html                  SEO / Open Graph metadata, fonts
netlify.toml                Netlify build + headers
public/
  favicon.svg
  og-image.jpg              Social share image
src/
  App.jsx                   Page composition
  main.jsx
  components/               Nav, Words, TiltCard, HeroCanvas, ProjectArt, Marquee, SectionHead
  sections/                 Hero, Work, About, Expertise, Journey, Contact, Footer
  data/
    site.js                 Name, email, GitHub, nav, skills, education, about copy
    projects.js             Selected work entries
  hooks/useReducedMotion.js
  lib/gsap.js               GSAP + ScrollTrigger registration
  styles/                   tokens, base, and one stylesheet per section
```

---

## Editing content

Everything personal lives in two files. No copy is hard-coded inside components.

### `src/data/site.js`

- `site.email` — currently `motazsouidi123@gmail.com`
- `site.github` — currently `https://github.com/motazsouidi123-maker`
- `site.linkedin` — `null`. Add a real URL here and expose it in `src/sections/Contact.jsx`
  only when a genuine profile exists.
- `skills` — the five disciplines with short descriptions. No percentages or levels are stored.
- `journey` — education and ongoing practice. **University name and dates are placeholders**
  (`University name — to be added`, `Dates — to be added`). Replace them with real values.
- `about` — paragraphs, traits and the "Right now" list.

### `src/data/projects.js`

Each project entry drives one showcase block:

```js
{
  id: 'slidecraft',
  index: '01',
  name: 'Slidecraft',
  category: 'Personal project',
  stack: [],          // e.g. ['React', 'CSS'] — empty shows "To be documented"
  href: null,         // real project URL — null hides the link entirely
  art: 'slidecraft',  // 'slidecraft' | 'presora'
  summary: '...',     // replace the placeholder with a real description
  year: '',           // optional
}
```

**Honest placeholders:** Slidecraft and Presora are Motaz's projects, but no descriptions, tech
stacks, URLs or statistics were supplied. Nothing about what they do has been invented — the cards
say so until real information is added. The previews are original abstract SVG compositions, and
the caption under each one states that they are not product screenshots.

When real screenshots exist, drop them in `src/assets/` and render an `<img>` inside
`.work__art-frame` instead of `<ProjectArt />`.

---

## Design system

- **Palette** — near-black `#07070b`, warm paper `#f2efe9`, acid lime `#d9ff43`, ember `#ff6a3d`.
- **Typography** — Bricolage Grotesque (display), Instrument Serif (editorial italic accents),
  JetBrains Mono (labels and metadata).
- **Spacing / radii** — sharp editorial edges, hairline rules, no card grids.
- **Motion** — masked word reveals, scroll-triggered section entrances, parallax layers, 3D tilt
  with pointer lighting, an animated marquee. All motion is skipped or reduced under
  `prefers-reduced-motion: reduce`.

Tokens live in `src/styles/tokens.css`. Change the accent in one place and the whole site follows.

---

## Accessibility & performance

- Semantic landmarks (`header`, `nav`, `main`, `section`, `footer`), one `h1`, labelled sections.
- Skip link, visible focus rings, keyboard-operable menu and copy button, `aria-expanded` state.
- The hero canvas is decorative (`aria-hidden`) and pauses when off-screen or when the tab is hidden.
- Fonts preconnected and loaded with `display=swap`; only two image assets ship.
- Production bundle is a single CSS and JS file, both cached aggressively on Netlify.

---

## Deploying to Netlify

`netlify.toml` is configured for a zero-click deploy:

```toml
[build]
  command = "npm run build"
  publish = "dist"
```

Push the repository to GitHub, then in Netlify choose **Add new site → Import an existing project**,
select the repo, and accept the detected settings. No environment variables are required.

---

## Notes / next steps

- Add real project descriptions, stacks and URLs in `src/data/projects.js`.
- Fill in the university name and study dates in `src/data/site.js`.
- Add a LinkedIn URL only when a real profile exists.
- A contact form was intentionally left out: there is no backend or submission service configured,
  so a form would silently fail. Email, GitHub and copy-to-clipboard are the working contact paths.
