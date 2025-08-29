# 🌍 TravelMate — Discover & Plan Your Next Journey

A clean, fast, and mobile‑friendly travel web app to explore destinations, build itineraries, and save favorite places. Built with **HTML, CSS, and JavaScript** (no frameworks needed). Perfect for beginners’ portfolios and ready to deploy on Vercel/Netlify.

---

## ✨ Highlights

* ⚡ **Blazing fast** static site (no backend required)
* 📍 **Search destinations** with smart filters (budget, season, interests)
* 🗺️ **Interactive map section** (Leaflet/Mapbox optional)
* 🧭 **Itinerary builder** with drag‑and‑drop days
* 💾 **Local storage** for favorites & saved trips
* 📱 **Responsive** layout (mobile‑first)
* 🎨 **Clean UI** with modern components

---

## 🔗 Demo

* Live Site: `https://your-live-url.com` (add after deploy)
* Screenshots: `assets/screenshots/` (add images)

---

## 🧰 Tech Stack

* **Core:** HTML5, CSS3, JavaScript (ES6+)
* **UI:** CSS Grid/Flexbox, custom components
* **Icons:** Lucide/Font Awesome (optional)
* **Map (optional):** Leaflet.js + OpenStreetMap

---

## 📂 Project Structure

```
travelmate/
├── index.html
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   ├── app.js
│   │   ├── data.js       # destinations, tags, mock data
│   │   └── storage.js    # localStorage helpers
│   ├── img/
│   └── screenshots/
├── .github/
│   └── ISSUE_TEMPLATE.md
├── README.md
└── LICENSE
```

---

## 🚀 Quick Start

### Option 1 — Open with Live Server

1. Clone the repo

   ```bash
   git clone https://github.com/<your-username>/travelmate.git
   cd travelmate
   ```
2. Open `index.html` with **Live Server** (VS Code extension) or double‑click to open in a browser.

### Option 2 — Simple HTTP Server (Node or Python)

```bash
# Node
npx http-server . -p 3000

# Python 3
python -m http.server 3000
```

Visit: `http://localhost:3000`

---

## 🧩 Features In Detail

* **Explore:** Filter by continent, budget, best time to visit, and tags like beaches, mountains, culture.
* **Plan:** Add places to days, reorder using drag‑and‑drop, and export to JSON.
* **Favorites:** Save/unsave destinations; persists via `localStorage`.
* **Map:** Show pins for selected places (Leaflet). Toggle satellite/streets layers.
* **Offline‑friendly:** Core UI works without network after first load.

---

## 🖼️ UI Preview (Placeholders)

```
assets/screenshots/home.png
assets/screenshots/explore.png
assets/screenshots/itinerary.png
```

> Add your own screenshots after building the UI.

---

## 🛠️ Setup Notes & Configuration

* **Leaflet (optional):** add CDN in `index.html` and configure your map container.
* **Mapbox (optional):** set `MAPBOX_TOKEN` in `app.js` (if you use Mapbox tiles).
* **Data source:** edit `assets/js/data.js` to add destinations.

```html
<!-- Leaflet CSS & JS (optional) -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
```

---

## 🧪 Sample Data (starter)

```js
// assets/js/data.js
export const DESTINATIONS = [
  {
    id: "bali",
    name: "Bali, Indonesia",
    country: "Indonesia",
    budget: "$$",
    bestTime: ["Apr", "May", "Jun", "Sep"],
    tags: ["beach", "temples", "surf"],
    coords: [-8.3405, 115.0920],
    image: "assets/img/bali.jpg",
    description: "Lush rice terraces, surf‑ready beaches, and serene temples."
  },
  {
    id: "paris",
    name: "Paris, France",
    country: "France",
    budget: "$$$",
    bestTime: ["Apr", "May", "Sep"],
    tags: ["culture", "museums", "city"],
    coords: [48.8566, 2.3522],
    image: "assets/img/paris.jpg",
    description: "Iconic landmarks, cafés, and world‑class art."
  }
];
```

---

## 🧠 Core Scripts (starter)

```html
<!-- index.html (inside <body>) -->
<header class="nav">
  <h1>TravelMate</h1>
  <input id="search" placeholder="Search destinations..." />
</header>
<main id="app">
  <section id="filters"></section>
  <section id="results" class="grid"></section>
  <section id="planner"></section>
</main>
<script type="module" src="assets/js/app.js"></script>
```

```css
/* assets/css/style.css */
:root { --bg:#0f172a; --card:#111827; --text:#e5e7eb; --muted:#94a3b8; }
*{box-sizing:border-box} body{margin:0;background:var(--bg);color:var(--text);font:16px/1.6 system-ui}
.nav{display:flex;gap:1rem;align-items:center;padding:1rem 1.25rem;border-bottom:1px solid #1f2937;position:sticky;top:0;background:rgba(15,23,42,.8);backdrop-filter:saturate(180%) blur(8px)}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:1rem;padding:1rem}
.card{background:var(--card);border:1px solid #1f2937;border-radius:16px;overflow:hidden}
.card img{width:100%;height:160px;object-fit:cover}
.card .p{padding:12px}
.badge{font-size:.75rem;color:var(--muted);border:1px solid #1f2937;padding:.2rem .5rem;border-radius:999px;margin-right:.35rem}
.button{display:inline-block;padding:.6rem 1rem;border-radius:12px;border:1px solid #1f2937;cursor:pointer}
.button:hover{transform:translateY(-1px)}
```

```js
// assets/js/app.js
import { DESTINATIONS } from "./data.js";

const q = (s, r=document) => r.querySelector(s);
const el = (t, c) => Object.assign(document.createElement(t), c || {});

const results = q('#results');
const search = q('#search');

function renderCards(list){
  results.innerHTML = '';
  list.forEach(d => {
    const card = el('article', { className:'card' });
    card.innerHTML = `
      <img src="${d.image}" alt="${d.name}">
      <div class="p">
        <h3>${d.name}</h3>
        <p>${d.description}</p>
        <div>${d.tags.map(t=>`<span class="badge">${t}</span>`).join('')}</div>
        <div style="margin-top:.5rem">
          <button class="button" data-id="${d.id}">Add to Plan</button>
        </div>
      </div>`
    results.appendChild(card);
  });
}

function filter(){
  const term = (search.value || '').toLowerCase().trim();
  const list = DESTINATIONS.filter(d =>
    d.name.toLowerCase().includes(term) ||
    d.tags.join(' ').toLowerCase().includes(term) ||
    d.country.toLowerCase().includes(term)
  );
  renderCards(list);
}

search.addEventListener('input', filter);
renderCards(DESTINATIONS);
```

---

## 📦 Deployment

### Netlify

* Drag‑and‑drop the project folder into Netlify OR connect via Git.
* Set build command: *none* (static) • Publish directory: `/`.

### Vercel

* Import the repo → Framework = "Other" → Output directory: `/`.

> After deployment, update the **Demo** link above.

---

## 🧭 Roadmap

* [ ] Dark/light theme toggle
* [ ] Map view with clustering
* [ ] Offline export (PDF/PNG of itinerary)
* [ ] Multi‑language support (EN/HI)
* [ ] API integration for real places (later)

---

## 🤝 Contributing

PRs welcome! Please open an issue first to discuss major changes.

1. Fork the project
2. Create feature branch: `git checkout -b feat/awesome`
3. Commit: `git commit -m "feat: add awesome"`
4. Push: `git push origin feat/awesome`
5. Open a Pull Request

See `.github/ISSUE_TEMPLATE.md` for bug/feature template.

---

## 📜 License

Distributed under the **MIT License**. See `LICENSE` for details.

---

## 🙋 FAQ

**Q: Can I use this in my portfolio?**
A: Yes! Add your own UI screenshots and deploy.

**Q: Can I add React later?**
A: Absolutely. Keep the public structure and swap `index.html` for a React build when ready.

**Q: Do I need an API?**
A: No. This starter uses local JSON; you can integrate APIs later.

---

## 👋 Author

**Rohit "Sammy" Mahato**

* GitHub: `@rohitmahato`
* LinkedIn/Portfolio: *add links here*
* Email: *add email here*

---

### 🔖 Badges (optional)

![Static Badge](https://img.shields.io/badge/HTML-CSS-JS-informational)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-success)

---

> Tip: After you create the repo, copy this README.md content, add screenshots, and push. Need a **LICENSE** or **ISSUE\_TEMPLATE.md**? Ping me and I’ll generate them too.


A
C
C
D
E
F
G
H
I
J
K
L
M
N
O
P
Q
R
S
T
U
V
W
X
Y
Z
