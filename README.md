# come-unity.productions

Static website for **come-unity** — Edmonton's home for house and deep house.
Hosted on GitHub Pages with a custom domain via Namecheap.

**Live site:** https://come-unity.productions

---

## Site structure

```
come-unity.productions/
├── index.html                      ← homepage
├── CNAME                           ← custom domain (do not delete or edit)
├── README.md                       ← this file
│
├── artists/
│   ├── index.html                  ← artist roster page
│   └── poloismz/
│       └── index.html              ← Poloismz full profile page
│
├── events/
│   ├── index.html                  ← all events listing
│   └── elevate/
│       └── index.html              ← Elevate Saturdays dedicated page
│
└── assets/
    ├── css/
    │   └── style.css               ← shared styles for all pages
    ├── logo.png                    ← come-unity circular logo
    ├── hero.jpg                    ← homepage hero background (Cask & Barrel interior)
    ├── elevate-cask.jpg            ← venue photo used on Poloismz profile
    ├── rane-1.jpg                  ← gear banner photo (Rane One / Serato)
    ├── poloismz-profile.jpg        ← Poloismz profile square photo
    ├── elevate/
    │   ├── Elevate_Banner.jpg      ← Elevate hero background (DJ booth shot)
    │   ├── Elevate_LOGO_00.png     ← Elevate Saturdays logo (red E + SATURDAYS)
    │   └── Elevate_Arrow.png       ← Elevate arrow mark (watermark + section icon)
    └── events/
        ├── polar-patio-solstice.jpg     ← Polar Patio Club Summer Solstice flyer
        ├── polar-patio-march-2024.png   ← Polar Patio Club First Days of Spring flyer
        └── winterruption_cover_photo.png ← Winterruption YEG festival flyer
```

---

## Pages overview

| Page | URL | Description |
|---|---|---|
| Homepage | `/` | Hero with venue photo, who we are / story, upcoming events teaser |
| Artists roster | `/artists/` | Grid of artist cards with profile, promo mix, Instagram, and EPK links |
| Poloismz profile | `/artists/poloismz/` | Full bio, genre tags, gear banner, mixes (SoundCloud embed), listening (Spotify embed), residency card, past gigs with filter tabs |
| All events | `/events/` | Upcoming and past events — auto-split by status field in JS array |
| Elevate Saturdays | `/events/elevate/` | Dedicated page with Elevate branding, upcoming dates, residents section |

---

## How to update content

All content is controlled by JavaScript arrays near the bottom of each HTML file.
Edit directly in GitHub (open file → pencil icon → edit → commit) — the site updates within ~60 seconds.

---

### Add an event to the events page

Open `events/index.html` → find `const events = [` → add a new entry:

```js
{
  title:   "elevate saturdays",
  date:    "9 August 2026",
  venue:   "The Cask & Barrel",
  lineup:  "poloismz<br>sotero",
  image:   "assets/elevate/Elevate_Banner.jpg",
  status:  "upcoming",   // or "past"
  tickets: "",           // ticket URL or "" for free entry
  slug:    "elevate/"
},
```

---

### Add an Elevate date with ticket info

Open `events/elevate/index.html` → find `const dates = [` → add:

```js
{
  date:    "9 August 2026",
  note:    "elevate saturdays",
  tickets: "",           // ticket URL or "" for free entry
  price:   ""            // e.g. "$10 adv / $15 door" or "" for no cover
},
```

---

### Add a mix to the Poloismz page

Open `artists/poloismz/index.html` → find `const mixes = [` → add:

```js
{
  title:  "your mix title",
  detail: "house / deep house · 60 min",
  src:    "https://w.soundcloud.com/player/?url=...&auto_play=false...",
  url:    ""
},
```

To get the `src` URL: SoundCloud → open track or playlist → Share → Embed → copy the `src="..."` value from the iframe code → change `auto_play=true` to `auto_play=false`.

---

### Add a listening embed (Spotify or Tidal)

Open `artists/poloismz/index.html` → find `const listening = [` → add:

```js
// Spotify
{
  type:     "embed",
  platform: "Spotify",
  src:      "https://open.spotify.com/embed/playlist/YOUR_ID?utm_source=generator",
  height:   352,
  label:    "house rotation",
  note:     "what's on while I'm working"
},

// Tidal
{
  type:     "embed",
  platform: "tidal",
  src:      "https://embed.tidal.com/playlists/YOUR_PLAYLIST_ID",
  height:   275,
  label:    "deep house favorites",
  note:     "tracks I keep coming back to"
},

// Simple link card (no embed)
{
  type:     "link",
  platform: "spotify",
  title:    "Larry Heard",
  url:      "https://open.spotify.com/artist/...",
  label:    "artist",
  note:     "the blueprint for deep house"
},
```

---

### Add a past gig to the Poloismz page

Open `artists/poloismz/index.html` → find `const pastGigs = [` → add:

```js
{
  title:     "event name",
  date:      "Month DD, YYYY",
  venue:     "Venue Name",
  image:     "../../assets/events/your-flyer.jpg",   // or "" for placeholder
  tags:      ["poloismz", "sotero"],
  type:      "elevate",   // "elevate" or "other"
  landscape: false        // true if flyer is wide (16:9), false for tall poster (3:4)
},
```

Set `type: "elevate"` for Elevate Saturdays nights. Set `type: "other"` for any other gig (Polar Patio Club, festivals, etc.). The filter tabs on the page handle the rest automatically.

---

### Add a photo to the Poloismz profile

1. Upload the photo to `assets/` — use a lowercase filename with hyphens, no spaces (e.g. `poloismz-profile.jpg`)
2. In `artists/poloismz/index.html` find:
   ```html
   <div class="profile-photo" style="background-image:url('../../assets/elevate-cask.jpg');">
   ```
3. Change the filename to your new photo:
   ```html
   <div class="profile-photo" style="background-image:url('../../assets/poloismz-profile.jpg');">
   ```

---

### Add a photo to an artist card (roster page)

1. Upload photo to `assets/` (lowercase, hyphens, no spaces)
2. In `artists/index.html` find the artist's card and change:
   ```html
   <div class="photo" style="background: linear-gradient(...);">
   ```
   to:
   ```html
   <div class="photo" style="background-image:url('../assets/artist-name.jpg');">
   ```

---

### Add an artist to the roster

1. Duplicate the Poloismz card block in `artists/index.html` — copy everything between `<!-- POLOISMZ -->` and `<!-- END POLOISMZ -->`
2. Update the name, role, bio, photo, and all link URLs
3. If the artist has their own profile page, create a folder e.g. `artists/sotero/` and add an `index.html` inside it (copy from `artists/poloismz/index.html` and edit)
4. Update the `profile →` button href to point to the new folder

---

### Add a gallery photo to the scrolling strip

The gallery strip is referenced in `index.html` (homepage) and `events/elevate/index.html`.

1. Upload photos to `assets/gallery/` (create this folder if it doesn't exist)
2. In the HTML find the gallery block and replace a placeholder `<div class="gal-item">`:
   ```html
   <!-- BEFORE (placeholder) -->
   <div class="gal-item gal-sq">
     <div class="gal-placeholder">...</div>
   </div>

   <!-- AFTER (real photo) -->
   <div class="gal-item gal-sq">
     <img src="assets/gallery/photo.jpg" alt="Elevate Saturdays">
   </div>
   ```
   Use `gal-sq` for square crops and `gal-ls` for landscape.
3. Also replace the matching slot in **Copy 2** (the duplicate set below the first) so the loop stays seamless.

---

### Update the Elevate hero background

Replace `assets/elevate/Elevate_Banner.jpg` with a new file of the same name, or change the reference in `events/elevate/index.html`:

```css
background-image: url('../../assets/elevate/your-new-banner.jpg');
```

---

## Naming rules for files

GitHub Pages is case-sensitive. Always use:
- **lowercase** filenames: `poloismz-profile.jpg` not `Poloismz-Profile.jpg`
- **hyphens** instead of spaces: `elevate-banner.jpg` not `elevate banner.jpg`
- Common formats: `.jpg`, `.png`, `.webp`

---

## Deploying changes

**Via GitHub.com (easiest — no terminal needed):**
1. Open the file in your repo
2. Click the pencil icon (Edit)
3. Make your changes
4. Click **Commit changes**
5. The site updates automatically within ~60 seconds

**Via terminal (git):**
```bash
git add .
git commit -m "describe what you changed"
git push
```

---

## GitHub Pages + Namecheap DNS

| Setting | Value |
|---|---|
| GitHub username | poloisaradiobot |
| Repo name | come-unity.productions |
| Repo URL | github.com/poloisaradiobot/come-unity.productions |
| Pages source | main branch / root |
| Custom domain | come-unity.productions |
| HTTPS | enforced |

**Namecheap Advanced DNS records:**

| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | poloisaradiobot.github.io |

---

## Tech stack

- Plain HTML, CSS, vanilla JavaScript — no frameworks, no build tools
- Hosted on GitHub Pages (free)
- Custom domain via Namecheap
- Fonts: Oswald + Space Mono via Google Fonts
- Embeds: SoundCloud (mixes), Spotify and Tidal (listening section)
- EPK / asset links: Google Drive (public share links)

---

*come-unity productions · Edmonton, AB · est. 2026*
