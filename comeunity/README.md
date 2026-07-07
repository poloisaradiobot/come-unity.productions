# come-unity.productions

Static website for come-unity — Edmonton house & deep house events.

## File structure

```
/
├── index.html                   ← home / landing page
├── artists/
│   ├── index.html               ← artist roster
│   └── poloismz/
│       └── index.html           ← PoloIsMZ profile
├── events/
│   ├── index.html               ← all events
│   └── elevate/
│       └── index.html           ← Elevate Saturdays page
├── assets/
│   ├── css/style.css            ← shared styles
│   ├── logo.png                 ← come-unity logo
│   └── hero.jpg                 ← venue background photo
└── CNAME                        ← custom domain (do not delete)
```

---

## GitHub Pages setup

### 1. Create the repo
1. Go to github.com → New repository
2. Name it exactly: `come-unity.productions` (or anything you like)
3. Set visibility to **Public** (required for free GitHub Pages)
4. Click **Create repository**

### 2. Push these files
```bash
git init
git add .
git commit -m "initial site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/come-unity.productions.git
git push -u origin main
```

### 3. Enable GitHub Pages
1. In your repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / root `/`
4. Click **Save**

GitHub will give you a URL like `https://yourusername.github.io/come-unity.productions`

---

## Namecheap DNS setup

### 4. Set up the custom domain in GitHub
1. Still in **Settings → Pages**, under "Custom domain"
2. Type: `come-unity.productions`
3. Click **Save** (this updates the CNAME file automatically)

### 5. Set up DNS on Namecheap
Go to Namecheap → **Domain List** → come-unity.productions → **Manage** → **Advanced DNS**

Add these **A records** (for the apex domain):

| Type | Host | Value            | TTL  |
|------|------|------------------|------|
| A    | @    | 185.199.108.153  | Auto |
| A    | @    | 185.199.109.153  | Auto |
| A    | @    | 185.199.110.153  | Auto |
| A    | @    | 185.199.111.153  | Auto |

Add this **CNAME record** (for www):

| Type  | Host | Value                          | TTL  |
|-------|------|--------------------------------|------|
| CNAME | www  | YOUR_USERNAME.github.io        | Auto |

> Replace `YOUR_USERNAME` with your actual GitHub username.

### 6. Enable HTTPS
Back in GitHub → **Settings → Pages** → tick **Enforce HTTPS** (available after DNS propagates — usually 10–30 min, up to 24h)

---

## Updating content

### Add an event
Open `events/index.html`, find the `const events = [...]` array and add a new object:
```js
{
  title:   "elevate saturdays vol. 2",
  date:    "2 August 2026",
  venue:   "The Cask & Barrel",
  lineup:  "poloismz<br>sotero",
  image:   "",          // or "../assets/events/vol2-flyer.jpg"
  status:  "upcoming",  // or "past"
  tickets: "",          // or "https://eventbrite.ca/..."
  slug:    "elevate/"
},
```
The same pattern works in `events/elevate/index.html` for individual dated shows.

### Add a flyer image
Drop the image into `assets/events/` then set the `image` field to `"../assets/events/yourfile.jpg"`.

### Add an artist
Duplicate the `artists/poloismz/` folder, rename it, edit the HTML inside.
Then add a card in `artists/index.html`.

### Add a mix to PoloIsMZ
Open `artists/poloismz/index.html`, find the `const mixes = [...]` array, add:
```js
{
  title:  "elevate vol. 2",
  detail: "July 2026 · 68 min",
  url:    "https://soundcloud.com/..."
},
```

---

## Deploy updates
```bash
git add .
git commit -m "describe what changed"
git push
```
GitHub Pages redeploys automatically within ~1 minute.
