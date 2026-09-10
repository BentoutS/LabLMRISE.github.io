# MRISE Lab — Site web

Site vitrine du **Laboratory for Multidisciplinary Research and Innovation in Sciences and Engineering (MRISE Lab)**, Université Belhadj Bouchaib de Ain Temouchent.

## Contenu
- `index.html` — page unique (HTML/CSS/JS, sans framework)
- `assets/logo.png` — logo du laboratoire

## Publier sur GitHub Pages
1. Crée un nouveau dépôt GitHub (par ex. `mrise-lab`).
2. Mets ces deux fichiers (`index.html` et le dossier `assets/`) à la racine du dépôt.
3. Sur GitHub : **Settings → Pages → Branch: main → dossier `/root`** puis **Save**.
4. Ton site sera en ligne à `https://<ton-utilisateur>.github.io/mrise-lab/` après 1–2 minutes.

## Modifier le contenu
- Textes des missions : section `<section id="mission">`.
- Équipes : tableau JavaScript `teams` en bas du fichier `index.html` (facile à éditer : nom, chef d'équipe, membres, acronyme, lien).
- Coordonnées et carte : section `<section id="contact">`.
- Couleurs / typographie : variables CSS en haut du fichier (`:root { ... }`).

Aucune dépendance externe hormis les polices Google Fonts (Space Grotesk, Inter, IBM Plex Mono), chargées via CDN.

## Visitor counter setup

The site has two visitor-count options wired in (footer, and in the `<script>` block near the closing `</body>` tag). Both are optional — the site works fine with neither configured.

### Option 1 — Quick badge (no signup)
Uses [visitorbadge.io](https://visitorbadge.io), free, no account needed. It counts a hit per unique page load for the exact URL you give it.

1. Publish the site to GitHub Pages first (see above), so you have a final live URL, e.g. `https://yourname.github.io/mrise-lab/`.
2. In `index.html`, find this line in the footer:
   ```html
   <img id="visitorBadge" src="https://api.visitorbadge.io/api/visitors?path=REPLACE_WITH_YOUR_LIVE_SITE_URL&label=Visitors&countColor=%236F4CE0&style=flat" ...>
   ```
3. Replace `REPLACE_WITH_YOUR_LIVE_SITE_URL` with your URL-encoded live site URL, e.g. `path=https%3A%2F%2Fyourname.github.io%2Fmrise-lab%2F`.

That's it — the badge updates automatically on every visit, no dashboard, just the number.

### Option 2 — GoatCounter (free account, real dashboard + live total on page)
[GoatCounter](https://www.goatcounter.com) is a free, privacy-friendly analytics tool (no cookies, GDPR-friendly) with a public dashboard showing visits over time, referrers, pages, etc.

1. Go to https://www.goatcounter.com/signup and create a free account — pick a site **code** (e.g. `mrise-lab`), giving you `mrise-lab.goatcounter.com`.
2. In `index.html`, find and replace **both** occurrences of `YOUR-CODE` with your chosen code:
   - The tracking script (just before `</body>`):
     ```html
     <script data-goatcounter="https://YOUR-CODE.goatcounter.com/count" async src="//gc.zgo.at/count.js"></script>
     ```
   - The live-total fetch inside the main `<script>` block:
     ```js
     fetch('https://YOUR-CODE.goatcounter.com/counter/TOTAL.json')
     ```
3. In your GoatCounter site settings, make sure **"Public"** is enabled if you want the total-visits number to show on the page itself (otherwise only you can see stats on the dashboard, and the on-page number stays hidden).
4. View full analytics anytime at `https://mrise-lab.goatcounter.com` (or whatever code you chose).

Both options can run at the same time — the badge gives an instant visual counter, GoatCounter gives you the full picture.

## Adding real team & member photos later

Right now every team card shows a themed gradient banner (with a subject icon) and every member shows a colored initials avatar. These are placeholders — swapping in real photos takes no code changes, just editing the `teams` array inside `index.html`'s `<script>` block.

### Team banner photo
Add a `photo` field to any team object, pointing to an image file (recommended: land it in `assets/teams/team-N.jpg`, wide format, ~1200×400px works well):
```js
{
  n: 1,
  icon: "flask",
  photo: "assets/teams/team-1.jpg",   // <-- add this line
  acro: "",
  title: "Chemical and Biological Studies on Nanomaterials Composites",
  ...
}
```
If `photo` is absent, the gradient + icon placeholder shows automatically — no need to touch anything else.

### Member photo
Add a `photo` key inside that member's existing profile object (4th array item), or create one if it doesn't exist yet:
```js
["Soufiane Bentout", "FST, University of Ain Temouchent", "chef", "chef", {
  photo: "assets/people/soufiane-bentout.jpg",   // <-- add this line
  orcid: "https://orcid.org/0000-0002-3699-7346",
  scholar: "https://scholar.google.com/citations?user=mfAJBVcAAAAJ",
  researchgate: "https://www.researchgate.net/profile/Soufiane-Bentout"
}],
```
Square photos (e.g. 200×200px) work best — they're cropped into a circle automatically. If no `photo` is given, the colored initials avatar shows instead.

Create `assets/teams/` and `assets/people/` folders in the repo to hold these images once you have them.

## AI-generated images — where they go

The site is now wired to automatically pick up images the moment you add them — no code edits needed. If a file is missing, the current placeholder (icon or gradient) just stays as-is, so nothing breaks in the meantime.

Color palette to reference in your prompts, so images blend with the site: **violet `#6F4CE0`**, **teal/cyan `#0EA5B7`**, **amber `#C97F12`**, on light backgrounds (`#F6F7FB` / white). Clean, modern, editorial/scientific illustration style works best — avoid busy or dark backgrounds since these sit on a light page.

| Slot | File path | Size / ratio | Suggested prompt direction |
|---|---|---|---|
| Hero background | `assets/hero-illustration.jpg` | 1600×900 (wide), fades out toward the bottom automatically | Abstract, subtle — molecular/network patterns, soft gradients in violet/teal, low detail so it doesn't compete with the text on top |
| Research area — Chemistry | `assets/areas/chemistry.jpg` | 400×400 (square) | Nanomaterials / lab glassware, minimal, violet-teal palette |
| Research area — Physics | `assets/areas/physics.jpg` | 400×400 (square) | Atomic/particle motif, materials science |
| Research area — Biology | `assets/areas/biology.jpg` | 400×400 (square) | DNA helix / biomathematics, organic curves |
| Research area — AI | `assets/areas/ai.jpg` | 400×400 (square) | Circuits, neural network, data visualization |
| Research area — Engineering | `assets/areas/engineering.jpg` | 400×400 (square) | Gears, systems, structural/industrial motif |
| Team banners (8, optional) | `assets/teams/team-1.jpg` … `team-8.jpg` | 1200×400 (wide) | One per team, themed to that team's research focus |
| Director portrait | `assets/director-lamia-bennabi.jpg` | 800×800 (square) | Professional portrait style, or a themed illustration if a real photo isn't available |

Team banners also need one line added per team in the `teams` array (see the section above) — every other slot in this table works automatically just by uploading the file with the exact name and path shown.

Once you have the images, upload them to me and I'll place them directly in the site for you.
