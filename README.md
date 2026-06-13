# Drum Collection Website

A personal archive and showcase website for a vintage and collectible drum collection. Built as a single self-contained HTML file — no build tools, no dependencies, no server required.

## Features

- **Brand-tabbed navigation** — Browse drums by manufacturer (Ludwig, Gretsch, Slingerland, Rogers, and a catch-all Other tab)
- **Drum cards** — Grid layout with photo, name, decade/material/size tags, short description, and approximate year
- **Detail modal** — Click any drum to open a full-screen overlay with a specs table and personal notes
- **Vintage dark theme** — Deep brown/black palette with gold accents, serif typography
- **Responsive layout** — Adapts to mobile and tablet viewports
- **Zero dependencies** — Pure HTML, CSS, and vanilla JavaScript; works by opening the file in any browser

## Project Structure

```
drum-collection/
└── index.html        # The entire site — markup, styles, and scripts in one file
```

> **Note:** The file may be named `drum-collection.html` locally. Rename it to `index.html` before deploying so it is served as the homepage.

## Adding a Drum

### 1. Add the card (HTML)

Find the correct brand `<section>` in `index.html` and copy an existing drum card block (marked `<!-- DRUM CARD START -->` / `<!-- DRUM CARD END -->`). Update the `onclick` with a unique key and fill in the card content:

```html
<!-- DRUM CARD START -->
<div class="drum-card" onclick="openModal('ludwig-supraphonic')">
  <!-- Replace the placeholder div below with a real <img> once you have a photo -->
  <div class="card-img-placeholder">...</div>
  <div class="card-body">
    <div class="card-name">Ludwig Supraphonic</div>
    <div class="card-meta">
      <span class="tag gold">1970s</span>
      <span class="tag">Chrome over Brass</span>
      <span class="tag">14×5</span>
    </div>
    <div class="card-desc">Short description of the drum.</div>
  </div>
  <div class="card-footer">
    <span class="card-year">c. 1974</span>
    <span class="card-view">View Details →</span>
  </div>
</div>
<!-- DRUM CARD END -->
```

### 2. Add the data (JavaScript)

Scroll to the `const drums = { ... }` block near the bottom of the file. Add a matching entry using the same key you used in `onclick`:

```js
'ludwig-supraphonic': {
  title: 'Ludwig Supraphonic Snare Drum',
  tags: [
    { label: '1970s', gold: true },
    { label: 'Chrome over Brass' },
    { label: '14×5' },
  ],
  specs: [
    ['Brand',     'Ludwig'],
    ['Model',     'Supraphonic'],
    ['Era',       'Early 1970s'],
    ['Shell',     'Chrome over brass, seamless'],
    ['Diameter',  '14"'],
    ['Depth',     '5"'],
    ['Hoops',     'Triple-flanged'],
    ['Strainer',  'P-85 throw-off'],
    ['Finish',    'Chrome'],
    ['Condition', 'Excellent — all original'],
  ],
  notes: 'Your personal notes about this drum.',
},
```

### 3. Add a photo

Replace the `<div class="card-img-placeholder">` with an `<img>` tag:

```html
<img
  class="card-img"
  src="photos/ludwig-supraphonic.jpg"
  alt="Ludwig Supraphonic"
/>
```

Keep your photos in a `photos/` subfolder alongside `index.html`. The modal image uses `id="modal-img"` — to add a photo there, replace its placeholder div with an `<img class="modal-img">` and set the `src` dynamically in `openModal()` if desired.

## Adding or Renaming a Brand

1. Add a nav button:
   ```html
   <button class="nav-btn" onclick="showBrand('premier')">Premier</button>
   ```
2. Add a matching section:
   ```html
   <section class="brand-section" id="brand-premier">
     <div class="brand-header">
       <div>
         <h2>Premier</h2>
         <p>Leicester, England · Est. 1922</p>
       </div>
       <span class="drum-count">0 drums</span>
     </div>
     <div class="drum-grid">
       <!-- drum cards go here -->
     </div>
   </section>
   ```

## Customization

| What to change               | Where to find it                                        |
| ---------------------------- | ------------------------------------------------------- |
| Site name & tagline          | `<h1>` and `<p>` inside `.site-title` in the header     |
| Hero intro text              | `.hero` section                                         |
| Brand names / history blurbs | `<div class="brand-header">` in each section            |
| Color theme                  | CSS variables at the top of `<style>` (`:root { ... }`) |
| Footer copyright name        | `<footer>` at the bottom of the file                    |

## Deployment

### Azure Static Web Apps (recommended)

1. Rename `drum-collection.html` → `index.html`
2. Push to a GitHub repository
3. In the Azure Portal, create a **Static Web App**, connect it to your repo, set build preset to **Custom** with all build paths left blank
4. Azure auto-deploys on every push; your site gets a free `*.azurestaticapps.net` URL and SSL certificate

### SWA CLI (no GitHub required)

```bash
npm install -g @azure/static-web-apps-cli
az login
swa deploy . --deployment-token <your-deployment-token>
```

Grab the deployment token from: Azure Portal → your Static Web App → **Manage deployment token**.

### Local preview

Just open `index.html` in any browser — no local server needed.
