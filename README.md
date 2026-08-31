# Pol del Castillo — portfolio

Static site, no build step, no dependencies. Designed to be edited by hand
(or with Claude) and hosted free on GitHub Pages.

Layout modeled on the sites Pol picked as references: alexanderelias.com and
cheng-chi.github.io (project rows with a media thumbnail left / text right,
per-entry link rows) plus v1ktornikolov.com (hero with Download Resume /
Contact buttons, categorized skill chips, a dedicated athletics section).

```
portfolio/
├── index.html                       the whole front page
├── css/style.css                    shared styles (palette, type, components)
├── projects/
│   └── _template.html               copy this to add a project case study
├── assets/
│   ├── Pol_del_Castillo_Resume.pdf  served by the "Download resume" buttons
│   └── img/                         thumbnails, headshot, photos, og image
└── _archive/
    └── index-v1-editorial.html      earlier text-only version, self-contained
```

The visual identity comes from the LaTeX resume: `#00235A` is the resume's
link blue, and EB Garamond is the resume's typeface — so the site and the
PDF read as one identity. Light and dark themes both work; the page follows
the visitor's system setting.

## The two highest-value things still missing

1. **Thumbnails** — every project row has a labeled placeholder saying what
   to drop in (GIF of the arm, bench photo, plot…). A short looping GIF or
   muted video per robotics project is what makes this format work — it's
   exactly what cheng-chi.github.io does.
2. **Headshot** — the hero has a portrait slot; swap the placeholder for
   `assets/img/headshot.jpg`.

## Filling a thumbnail

Replace the `<span class="placeholder">…</span>` inside an entry's
`<div class="thumb">` with either:

```html
<img src="assets/img/so101.gif" alt="SO-101 arm running a learned policy">
```

or a muted looping video (smaller files than GIF for the same clip):

```html
<video src="assets/img/so101.mp4" autoplay muted loop playsinline></video>
```

Keep clips short (5–15 s), around 640 px wide, a few MB at most. Convert a
screen recording with: `ffmpeg -i in.mp4 -vf scale=640:-2 -an out.mp4`

## Adding a project

1. Copy an existing `<div class="entry">` block in `index.html` into the
   right section and edit it. Story shape: outcome-first paragraph, 2–4
   bullets with real numbers, chips, links row.
2. For a deep dive, copy `projects/_template.html` →
   `projects/your-project.html`, fill the `[BRACKETED]` placeholders
   (problem → approach → results → what's next), and link it from the
   entry's `entry-links` row:
   ```html
   <a href="projects/your-project.html">Case study &rarr;</a>
   ```
3. Per-entry links follow the academic-site convention:
   `Case study → · Code ↗ · Video ↗ · Paper ↗` — commented stubs are
   already in place.

## Updating the resume PDF

`assets/Pol_del_Castillo_Resume.pdf` was compiled from the LaTeX source in
`Downloads/RESUME.zip` (MiKTeX is installed — `pdflatex main.tex` works).
When the resume changes, re-export from Overleaf (or recompile) and replace
this one file; both buttons point at it.

## What this design is optimized for (the research, in short)

- **Case studies over lists** — 3–6 well-documented projects beat twenty
  shallow ones.
- **Outcome first, numbers everywhere** — "0.001 in under $1,500" is
  remembered; "worked on automation" is not.
- **A 30–60 s demo video per robotics project** is the single
  highest-value asset; embed via YouTube on case-study pages, loop a
  silent clip in the thumbnail.
- **Contact findable in under 10 seconds** — buttons in the hero and the
  footer. Phone number deliberately left off the public site; email is
  enough and scrapes less.
- **Mobile matters** — a majority of recruiters open portfolios on a
  phone; the layout collapses to one column, verified at 375 px.

## Previewing locally

Just double-click `index.html` — everything works from the filesystem.

## Publishing on GitHub Pages

1. Create a repo named exactly **`pd05849.github.io`** on GitHub.
2. Push this folder to it:

```bash
git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/pd05849/pd05849.github.io.git
git push -u origin main
```

3. GitHub Pages turns on automatically for a `<username>.github.io` repo.
   The site appears at **https://pd05849.github.io** within a minute or two.

To use a different repo name instead, push there and enable Pages under
Settings → Pages → Source: `main` / root. The URL becomes
`https://pd05849.github.io/<repo-name>`.

After it's live: add a 1200×630 social-preview image at `assets/img/og.png`
and uncomment the `og:image` tag in `index.html`, so links shared on
LinkedIn show a proper card. (You may want to exclude `_archive/` from the
repo — add a `.gitignore` line — or keep it; it's harmless either way.)

## Custom domain, later

Buy a domain, add a file named `CNAME` here containing just the domain
(e.g. `poldelcastillo.com`), point the domain's DNS at GitHub Pages, then
set it under Settings → Pages.
