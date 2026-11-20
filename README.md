# Ng Mei Yee - Portfolio

Static portfolio site converted from the Figma `PORTFOLIO` file. Single page, no build step, deploys as-is to GitHub Pages.

## Status

| Item | Status |
|---|---|
| Page structure, layout, type, colour | sourced (from Figma) |
| All 19 project titles and descriptions | sourced (transcribed from Figma, proofread needed) |
| Nav, modals, scroll animation, mobile layout | sourced (built and verified) |
| Hero collage card text (Experience / Education / Summary) | proposed (my wording, replace with yours) |
| Project images | open (you export them) |
| Case study images for the popups | open (you export them) |
| Resume PDF | open (you add it) |
| Custom domain | open (optional) |

Flagged assumptions, because I could not read them cleanly from the Figma render:

- The five bullets on the yellow "My Experience" note are my wording, not yours.
- The "Summary" card text is my paraphrase of your Figma copy.
- Project descriptions were transcribed visually from the design. Proofread them.

## Deploy

1. Create a public repo named `portfolio` on GitHub.
2. Push `index.html`, `README.md`, `.nojekyll` and the `assets/` folder to `main`.
3. Repo Settings, Pages, Source "Deploy from a branch", branch `main`, folder `/root`.
4. The site goes live at `https://ngmeiyee2005821.github.io/portfolio/` within a minute or two.

```bash
git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/NgMeiYee2005821/portfolio.git
git push -u origin main
```

`.nojekyll` is included so GitHub serves folders beginning with an underscore correctly. Keep it.

## Images to export from Figma

Export at 2x PNG, then convert to WebP if you want smaller files (change the extension in `index.html` to match if you do). Nothing in the layout breaks while these are missing. Each empty slot shows its own filename, so you always know what goes where.

### Hero

```
assets/hero/portrait.jpg
```

### Project thumbnails

```
assets/work/daikin-dtc.png
assets/work/the-daun.png
assets/work/suruhanjaya-tenaga-app.png
assets/work/app-component.png
assets/work/tng-disbursement.png
assets/work/smart-blasting.png
assets/work/suruhanjaya-tenaga-portal.png
assets/work/deloitte.png
assets/work/raya-airways.png
assets/work/apeak-gaming.png
assets/work/dina-travel.png
assets/work/encompass.png
assets/work/beshop-logo.png
assets/work/jaxer-logo.png
assets/work/veecotech-hiring-1.png
assets/work/veecotech-hiring-2.png
assets/work/mynext.png
assets/work/indrive.gif
assets/work/jaxer-brochure.png
```

Export the image area of each card only, not the whole card. The titles and descriptions are real text in the page, which is better for search engines and screen readers than text baked into a picture.

### Case study popups

These come from your popup frames in Figma. Export each inner screen as its own tall image.

```
assets/case/suruhanjaya-tenaga/01-login.png
assets/case/suruhanjaya-tenaga/02-dashboard.png
assets/case/suruhanjaya-tenaga/03-user-management.png
assets/case/suruhanjaya-tenaga/04-add-new-user.png
assets/case/suruhanjaya-tenaga/05-roles.png
assets/case/suruhanjaya-tenaga/06-view-roles.png
assets/case/suruhanjaya-tenaga/07-content-management.png
assets/case/suruhanjaya-tenaga/08-view-content.png

assets/case/raya-airways/01-home.png
assets/case/raya-airways/02-about-us.png
assets/case/raya-airways/03-ground-operations.png
assets/case/raya-airways/04-our-fleet.png
```

### Resume

```
assets/Ng-Mei-Yee-Resume.pdf
```

## Adding a case study to another project

Only Suruhanjaya Tenaga (portal) and Raya Airways open a popup right now, because those are the two you had built in Figma. To add more, find the `CASES` object near the bottom of `index.html` and add an entry whose key matches the card's `data-project` value:

```js
var CASES = {
  'deloitte': {
    images: [
      'assets/case/deloitte/01-dashboard.png',
      'assets/case/deloitte/02-assessment.png'
    ]
  }
};
```

A card with no entry in `CASES` simply does not open a popup, and gets no "View" hover badge. Nothing else to change.

## How the Figma prototype maps to the web

| Figma | Web |
|---|---|
| Prototype navigation between frames | Smooth anchor scrolling plus a sticky nav |
| Popup overlay frames | HTML modal, closes on backdrop click or Esc |
| "Click Background to Close" label | Kept as the modal footer hint |
| Smart animate on entry | `IntersectionObserver` plus CSS transitions |
| Fixed 1440px frames | Fluid layout, single column below 640px |
| Tape label graphics | Drawn in CSS, so they stay sharp at any zoom |

## Notes

- Tailwind loads from its CDN and compiles in the browser. That keeps the file editable by hand with no build step, which is what you asked for. If the page ever feels slow to paint, the fix is a prebuilt Tailwind CSS file, and I can do that conversion later.
- `prefers-reduced-motion` is respected: animations switch off for visitors who have asked their system for less motion.
- The contact button opens the visitor's mail client. GitHub Pages cannot run a server, so a real contact form would need a third-party endpoint such as Formspree.
