# Rodney Maiato — Art Portfolio

Personal art portfolio site showcasing sketches and paintings from Moleskine sketchbooks.

Live at [rodneymaiato.art](http://rodneymaiato.art)

---

## Stack

Pure static HTML — no build step, no framework, no dependencies.

- `index.html` — gallery page
- `about.html` — about page
- `contact.html` — contact form (Netlify Forms)
- `style.css` — all styles
- `favicon.svg` — RM initials favicon
- `static/img/` — all artwork images
- `add-artwork.html` — local helper tool (not in git, see below)

---

## Local Development

Open `index.html` directly in a browser, or run a local server for a more accurate preview:

```bash
npx serve .
```

or

```bash
python3 -m http.server
```

Then open `http://localhost:3000` (or whatever port is shown).

---

## Adding a New Artwork

### Using the local helper tool (recommended)

`add-artwork.html` is a local tool that generates the HTML for you — open it in any browser:

```
open add-artwork.html
```

Fill in the image filename, title, tags, an optional description, and any extra images (process shots, grayscale versions, etc.). Hit **Generate HTML** and you'll get two ready-to-paste code blocks:

1. **Gallery card** — paste inside `<div class="gallery">` in `index.html`
2. **Dialog / lightbox** — paste before `<footer>` in `index.html`

> `add-artwork.html` is excluded from git and stays on your local machine only.

---

### Manually

Adding a new piece takes three steps: add the image, add a gallery card, add a lightbox dialog.

### 1. Add the image

Copy your image file into `static/img/`.

### 2. Add a gallery card

In `index.html`, inside the `<div class="gallery">`, add a new button block:

```html
<button class="gallery-item" onclick="openWork('your-id')">
  <img src="static/img/your-image.jpg" alt="Title of the Work" loading="lazy">
  <div class="item-overlay">
    <span class="item-title">Title of the Work</span>
    <span class="item-tags">medium · style · tag</span>
  </div>
</button>
```

Replace `your-id` with a short unique slug (e.g. `river-sketch`), and update the image filename, alt text, title, and tags.

### 3. Add a lightbox dialog

Below the gallery (before the `<footer>`), add a matching dialog. The `id` must match the slug used in step 2.

**Minimal version (image + title + tags only):**

```html
<dialog id="your-id">
  <div class="dialog-header">
    <button class="dialog-close" aria-label="Close">&#x2715;</button>
  </div>
  <div class="dialog-scroll">
    <img src="static/img/your-image.jpg" alt="Title of the Work" class="dialog-main-img">
    <div class="dialog-meta">
      <h2>Title of the Work</h2>
      <p class="dialog-tags">medium · style · tag</p>
    </div>
  </div>
</dialog>
```

**With description text:**

```html
<dialog id="your-id">
  <div class="dialog-header">
    <button class="dialog-close" aria-label="Close">&#x2715;</button>
  </div>
  <div class="dialog-scroll">
    <img src="static/img/your-image.jpg" alt="Title of the Work" class="dialog-main-img">
    <div class="dialog-meta">
      <h2>Title of the Work</h2>
      <p class="dialog-tags">medium · style · tag</p>
      <div class="dialog-text">
        <p>Write something about this piece here.</p>
      </div>
    </div>
  </div>
</dialog>
```

**With extra images (e.g. process shots, grayscale version):**

```html
<img src="static/img/your-extra-image.jpg" alt="Description" class="dialog-extra-img">
```

Add this after the `dialog-text` div, inside `dialog-scroll`.

---

## Deployment

The site is a static folder — deploy by uploading the project root to any static host. No build command needed.

---

## License

&copy; Rodney Maiato. All artwork is original and all rights are reserved.
