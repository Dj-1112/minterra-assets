# minterra-assets

Image and media asset repository for [minterra.in](https://minterra.in).  
This repo is served via GitHub Pages so images are accessible by URL from the main website.

---

## Why a Separate Repo?

- Keeps `minterra-web` (code) lightweight and fast to clone/work with
- Images can be added or replaced without touching any HTML or CSS
- Clear separation: code changes in one repo, content/images in the other
- Each repo has its own commit history — code fixes don't get mixed with "added project photo"

---

## GitHub Pages Setup (one-time)

This repo must have GitHub Pages enabled for images to be accessible via URL.

1. Create GitHub repo named exactly: `minterra-assets` (visibility: **Public**)
2. Push all files to the `main` branch
3. Go to repo **Settings → Pages**
4. Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → Save

Once enabled, all files are accessible at:
```
https://YOUR-GITHUB-USERNAME.github.io/minterra-assets/[folder]/[filename]
```

Then in `minterra-web`, do a **Find & Replace** across all `.html` files:
- Find: `YOUR-GITHUB-USERNAME`
- Replace: your actual GitHub username

---

## Folder Structure

```
minterra-assets/
│
├── site/
│   ├── logo.png              ← Main brand logo (used in email signatures, social)
│   ├── logo-white.png        ← White variant for dark backgrounds
│   ├── og-image.jpg          ← Social share preview image (1200×630px recommended)
│   └── hero-bg.jpg           ← Homepage hero background image
│
├── team/
│   ├── founder.jpg           ← Founder photo
│   ├── co-founder.jpg        ← Co-founder photo
│   └── head-of-design.jpg    ← Head of design photo
│
├── services/
│   ├── architecture.jpg      ← Services page image for Architecture card
│   ├── construction.jpg      ← Services page image for Construction card
│   ├── interior.jpg          ← Interior design service image
│   ├── renovation.jpg        ← Renovation service image
│   └── landscaping.jpg       ← Landscaping service image
│
└── projects/
    ├── project-001-river-edge-villa/
    │   ├── cover.jpg         ← Card thumbnail (ALWAYS this name)
    │   ├── gallery-01.jpg
    │   ├── gallery-02.jpg
    │   └── gallery-03.jpg
    │
    ├── project-002-prestige-office-park/
    │   ├── cover.jpg
    │   ├── gallery-01.jpg
    │   └── gallery-02.jpg
    │
    ├── project-003-heritage-home-revival/
    │   ├── cover.jpg
    │   ├── gallery-01.jpg
    │   └── gallery-02.jpg
    │
    └── project-004-next-project-name/   ← Add new projects here
        ├── cover.jpg
        └── gallery-01.jpg
```

---

## Naming Rules — Read Before Adding Files

These rules are what allow images to be swapped without touching any HTML.
**Do not break them.**

### Project Folders

```
project-[NUMBER]-[slug]/
```

| Part       | Rule                                              | Example                         |
|------------|---------------------------------------------------|---------------------------------|
| `NUMBER`   | Three-digit sequence, always padded               | `001`, `002`, `012`, `099`      |
| `slug`     | Short hyphenated name, lowercase, no spaces       | `river-edge-villa`              |

Full example: `project-004-lakefront-residence/`

### Files Inside a Project Folder

| Filename         | Purpose                                     | Rules                                  |
|------------------|---------------------------------------------|----------------------------------------|
| `cover.jpg`      | Card thumbnail on projects page             | **Always exactly this name**           |
| `gallery-01.jpg` | First gallery image                         | Always zero-padded sequential numbers  |
| `gallery-02.jpg` | Second gallery image                        | Add `gallery-03`, `gallery-04` as needed |

### Team Photos

```
team/[role-slug].jpg
```
Example: `team/founder.jpg`, `team/head-of-design.jpg`

Keep the filename stable. To update a team photo, upload a new file with the **same name**.

### Site Assets

| File              | Size / Notes                                      |
|-------------------|---------------------------------------------------|
| `og-image.jpg`    | 1200×630px — used for social media link previews  |
| `hero-bg.jpg`     | At least 1920px wide — used as homepage background|
| `logo.png`        | Transparent background preferred                  |

---

## How to Add a New Project (Step by Step)

### Step 1 — Create the folder in this repo

Name it following the convention:
```
projects/project-00X-project-slug/
```
Where `X` is the next number in sequence (004, 005, etc.)

### Step 2 — Add images

Required:
- `cover.jpg` — the card thumbnail (aim for 800×600px, 4:3 ratio, under 300 KB)

Optional but recommended:
- `gallery-01.jpg`, `gallery-02.jpg`, `gallery-03.jpg` — full-res gallery shots

**Optimise images before uploading.** Large images slow down the website.
Use [Squoosh](https://squoosh.app) (free, in browser) to compress to JPEG quality 80.
Target: under 300 KB per image. Hero/large images: under 500 KB.

### Step 3 — Add the project card in minterra-web

In `minterra-web/projects.html`, copy an existing `<article class="project-card">` block
and update:
- `data-category` attribute (residential / commercial / renovation / interior)
- `src` to point to the new folder's `cover.jpg`
- `alt` text describing the project
- Project number, name, location, year

The project also appears automatically on the homepage "Featured Projects" section
if you add it there too (in `index.html`).

---

## How to Replace an Image Without Touching HTML

Because filenames are always stable (e.g. `cover.jpg`, `hero-bg.jpg`),
you can replace any image by just overwriting the file:

1. Upload the new image to GitHub with the **exact same filename**
2. GitHub overwrites the old file
3. The URL stays identical → the website updates automatically
4. **Zero HTML changes needed**

> Note: GitHub may cache the old image for a few minutes. Hard-refresh
> the browser (Ctrl+Shift+R or Cmd+Shift+R) if you don't see the new image immediately.

---

## Image Format Guidelines

| Type        | Format | Why                                              |
|-------------|--------|--------------------------------------------------|
| Photos      | `.jpg` | Best compression for photographs                 |
| Logos/icons | `.png` | Preserves transparency                           |
| Illustrations | `.svg` | Scales infinitely, tiny file size              |

Avoid `.webp` unless you're sure all your visitors use modern browsers.
`.jpg` at quality 80 is safe, fast, and universally supported.

---

## Commit Message Convention

Keep the asset repo history readable:

```
add: project-004-lakefront-residence cover and gallery images
update: team/founder.jpg — new photo
replace: site/hero-bg.jpg — higher resolution version
add: services/interior.jpg
```

---

## Questions?

Refer to the main `minterra-web` README for full deployment, DNS, and development instructions.
