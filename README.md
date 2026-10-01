# Kshitij Ambilduke — personal academic website

A static site in plain HTML and CSS. There is no build step and no dependencies, so GitHub Pages serves the files exactly as they are.

```
index.html                 About, News, Publications, Projects, Notes
projects/*.html            one page per project (cover, summary, links, PDFs)
assets/css/style.css       all styling; colour tokens are at the top (light + dark)
assets/js/main.js          dark-mode toggle, BibTeX buttons; opens external links in a new tab
assets/img/                profile photo, publication thumbnails, project covers
assets/pdf/<project>/      posters, reports and slides embedded on project pages
404.html, favicon.svg, apple-touch-icon.png, .nojekyll
```

## Deploy to GitHub Pages

This folder is a git clone of [`Kshitij-Ambilduke/Kshitij-Ambilduke.github.io`](https://github.com/Kshitij-Ambilduke/Kshitij-Ambilduke.github.io), and the site is published from the `master` branch.

1. Push your changes: `git push origin master`.
2. The first time only: in the repository, open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, then select `master` and `/ (root)`.
3. After a minute or so the site is live at **https://kshitij-ambilduke.github.io**.

After that, every push to `master` updates the site.

> If you use a different repository name, the site is served at `https://kshitij-ambilduke.github.io/<repo-name>/`. All links are relative, so it still works. The only thing to update is the `og:image` URL in the `<head>` of each page, which controls link previews.

## Preview locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Updating content

- **News:** in `index.html`, add an `<li>` at the top of the first `<ul class="news">`:
  `<li><time datetime="2026-10">Oct. 2026</time><p>…</p></li>`.
  Older items sit in the collapsible `<details class="news-more">` list underneath. To keep the visible list short, move the last visible item into it and update the count in "Show older news (5)".
- **Publication:** copy one `<li class="pub">…</li>` block in `index.html` and put its thumbnail in `assets/img/publications/`.
  - The small label above the title is `<p class="eyebrow">`.
  - Paste the BibTeX entry inside the `<pre>`. For the BibTeX and Copy buttons to work, give the new block its own ids: `bib-<name>` on the box and `bib-<name>-text` on the `<pre>`. They must match the button's `aria-controls` and `data-copy`.
- **Project:**
  1. Copy a file in `projects/` (for example `spire-lm.html`) and edit its title, links, summary and PDF sections.
  2. Put the cover image in `assets/img/projects/` and the PDFs in `assets/pdf/<project>/`.
  3. Add a matching `<li>` card in the `<ul class="projects">` grid in `index.html`.
  4. Update the "Previous / Next" links at the bottom of the neighbouring project pages.
- **Colours and fonts:** change the variables at the top of `assets/css/style.css`. The site always opens in light mode. The dark palette is the `:root[data-theme="dark"]` block, which the moon button switches on, and each visitor's choice is remembered.

Icons are inline SVGs from [Font Awesome Free](https://fontawesome.com) (CC BY 4.0). Text uses each device’s own system font (San Francisco on Apple devices, Segoe UI on Windows, Roboto on Android), so no font is downloaded. To use a web font instead, add its Google Fonts link to each page’s `<head>` and put its name first in the `--font-sans` variable.
