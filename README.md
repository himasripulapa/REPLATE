# 🌿 Replate: Rescue Food. Feed People.

Replate is a front-end web app that connects **people with surplus food** (event hosts, restaurants, temples, passersby) to **nearby NGOs** and **volunteers** who can pick it up and deliver it before it expires.

> **Event / Reporter → NGO → Volunteer**

Built with plain HTML, CSS and JavaScript. No framework, no build step, no backend.

---

## ✨ Features

| Page | File | What it does |
|------|------|--------------|
| **Home** | `index.html` | Landing page with a hero section, live impact stats, a "How it works" walkthrough and calls to action |
| **Report Food** | `report.html` | Form to report leftover food: reporter info, food type, quantity, pickup and expiry time, location (with "use my current location"), notes and a volunteer-request toggle |
| **Live Listings** | `listings.html` | Real-time feed of all reports with filter tabs (All / Available / Active / Delivered / Expired) and live expiry countdowns |
| **NGO Dashboard** | `ngo.html` | Pick an NGO and see requests within 20 km (distance computed with the Haversine formula). Accept or decline, with KPI cards and expiry progress bars |
| **Volunteer** | `volunteer.html` | Pick a volunteer profile, view their stats and take available deliveries |
| **Impact** | `impact.html` | Impact dashboard with meals rescued, people fed, waste reduced, a weekly bar chart, monthly goals and a leaderboard |
| **Shared styles** | `replate-shared.css` | Design tokens (colors, radius, shadows), navbar, buttons, badges, forms, cards and animations used by every page |

### Highlights

- ⏰ **Live expiry countdowns** that tick every second and change color as time runs low
- 📍 **Distance-based NGO matching** using latitude/longitude and the Haversine formula
- 🔄 **Cross-page shared state** through `localStorage`, so a report submitted on one page shows up on the others
- 📊 **Auto-updating impact stats** (meals, people fed, kg of waste reduced, rescues)
- 📱 **Responsive layout** with a compact navbar on small screens
- 🎨 **Consistent design system** driven by CSS variables in a single shared stylesheet

---

## 🚀 Getting Started

No installation is needed.

### Option 1: Open directly
Clone the repo and open `index.html` in your browser.

```bash
git clone https://github.com/<your-username>/replate.git
cd replate
open index.html        # macOS
# start index.html     # Windows
# xdg-open index.html  # Linux
```

### Option 2: Run a local server (recommended)
A local server makes sure `localStorage` and cross-page behavior work consistently.

```bash
# Python
python3 -m http.server 8000

# or Node
npx serve .
```

Then visit **http://localhost:8000**.

---

## 🧭 How It Works

1. **Report** – A host or passerby fills out the form on **Report Food**. The report is saved to `localStorage` under `replate_reports`, and the global stats under `replate_stats` are updated.
2. **Notify** – The report appears on **Live Listings** and on the **NGO Dashboard** of any NGO within 20 km of the pickup location.
3. **Accept** – An NGO accepts or declines the request. Choices are stored in `ngo_accepted` and `ngo_declined`.
4. **Deliver** – A volunteer takes the delivery on the **Volunteer** page. This is stored in `vol_taken`.
5. **Measure** – The **Impact** and **Home** pages read the shared stats and show the totals.

### Impact estimates
When a report is submitted, these values are derived from the quantity entered:

- **People fed** ≈ `quantity × 0.95`
- **Waste reduced (kg)** ≈ `quantity × 0.35`

---

## 🗂️ Project Structure

```
replate/
├── index.html            # Landing page
├── report.html           # Report leftover food
├── listings.html         # Live listings feed
├── ngo.html              # NGO dashboard
├── volunteer.html        # Volunteer dashboard
├── impact.html           # Impact & leaderboard
└── replate-shared.css    # Shared design system
```

---

## 💾 Data & Storage

All data lives in the browser's `localStorage`:

| Key | Purpose |
|-----|---------|
| `replate_reports` | Array of submitted food reports |
| `replate_stats` | Aggregate meals, people, kg and rescues |
| `ngo_accepted` | IDs of reports accepted by NGOs |
| `ngo_declined` | IDs of reports declined by NGOs |
| `vol_taken` | IDs of deliveries taken by volunteers |

Each page also includes two **seed reports** (a Bengaluru wedding and a Vijayawada community lunch) so the UI isn't empty on first load.

To reset the app, clear site data in your browser or run this in the console:

```js
localStorage.clear();
```

---

## 🛠️ Tech Stack

- **HTML5**, **CSS3** (custom properties, grid, flexbox, keyframe animations)
- **Vanilla JavaScript** (ES6+)
- **[Inter](https://fonts.google.com/specimen/Inter)** via Google Fonts
- **Browser Geolocation API** for "use my current location"
- **Unsplash** image on the home page, with an emoji fallback if it fails to load

---

## ⚠️ Current Limitations

This is a front-end prototype, so a few things are simulated:

- **No backend or database.** Data is stored per browser, so reports aren't shared between devices or users.
- **No real notifications.** "Notify Nearby NGOs" saves the report locally; no SMS, email or push alert is sent.
- **No automatic volunteer matching.** Volunteers pick deliveries manually; nearest-volunteer assignment is not implemented yet.
- **Fixed NGO and volunteer lists.** NGO locations and volunteer profiles are hard-coded.
- **Fixed 20 km radius on the NGO dashboard.** The "Search Radius" field on the report form is saved with the report but not used for matching yet.
- **Fallback coordinates.** If latitude and longitude are left blank, a random point near Hyderabad is used.
- **Illustrative numbers.** Some impact figures (partner NGOs, volunteers, weekly chart, leaderboard) are static sample data.

---

## 🗺️ Roadmap

- [ ] Backend and database (Firebase, Supabase or Node + PostgreSQL)
- [ ] User authentication with roles (reporter, NGO, volunteer)
- [ ] Real-time notifications (SMS, WhatsApp, push)
- [ ] Automatic nearest-volunteer assignment
- [ ] Map view with live pickup and NGO markers
- [ ] Address autocomplete and geocoding
- [ ] Use the reporter's chosen search radius for NGO matching
- [ ] Delivery status tracking (Accepted → In transit → Delivered)
- [ ] Photo upload for food reports
- [ ] Multi-language support

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for details.

---

<p align="center">Made with 🌿 to fight food waste, one plate at a time.</p>
