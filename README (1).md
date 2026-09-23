# E-Album

**Every Memory. One Beautiful Place.**

A premium, Apple-inspired digital photo album web app — built as a single self-contained HTML file with vanilla HTML, CSS, and JavaScript. No frameworks, no build step, no backend.

![E-Album](https://img.shields.io/badge/stack-HTML%20%7C%20CSS%20%7C%20JS-0071e3?style=flat-square)
![No dependencies](https://img.shields.io/badge/dependencies-none-30d158?style=flat-square)

---

## Features

- **Cinematic landing page** — floating glassmorphic nav, full-screen hero, an interactive 3D album (CSS `perspective`/`transform-style: preserve-3d`) that tilts on mouse move and opens on click, plus scroll-reveal feature cards
- **Authentication (demo)** — sign up / log in / log out backed by `localStorage`, live password-strength meter, real-time form validation, show/hide password toggle
- **Dashboard** — animated stat counters, time-of-day greeting, recent albums
- **Album management** — create, search, sort (newest / oldest / A–Z / most memories), favorite
- **Album view** — photo grid, drag-and-drop / file-picker upload with live `FileReader` previews, share modal with a generated demo link and working "Copy Link"
- **Lightbox** — fullscreen photo view with previous/next, favorite, download and share actions, full keyboard support (`Esc`, `←`, `→`)
- **Memories & Favorites** — unified views across all albums
- **Profile & Settings** — editable name/bio, light / dark / system theme (persisted), notification and privacy toggles
- **Responsive** — sidebar collapses to a bottom nav on mobile; tested down to 320px
- **Accessible & performant** — semantic HTML, visible focus states, `prefers-reduced-motion` respected, animations run on CSS transforms only

## Tech stack

- HTML5
- CSS3 (custom properties, glassmorphism, 3D transforms, `IntersectionObserver`-driven reveals)
- Vanilla JavaScript (hash-based router, no framework)
- `localStorage` for demo data persistence (users, albums, photos metadata, theme, preferences)

No React, Vue, Angular, Bootstrap, or jQuery.

## Getting started

This is a single static file — there's nothing to install or build.

```bash
git clone https://github.com/<your-username>/e-album.git
cd e-album
open index.html   # or just double-click the file / drag it into a browser
```

Optionally serve it locally so routing behaves exactly like a deployed site:

```bash
npx serve .
# or
python3 -m http.server 8000
```

On first load, six sample albums are seeded automatically so the app doesn't look empty. Sign up with any name, email, and a 6+ character password to create a demo account — everything is stored only in your browser's `localStorage`.

## Project structure

```text
e-album/
├── index.html      # the entire app: markup, styles, and script in one file
└── README.md
```

The file is organized internally the way a multi-file project would be, with clearly commented sections standing in for what would normally be separate modules:

```text
storage.js   → DB get/set helpers, demo data seeding
auth.js      → registerUser / loginUser / logoutUser / getCurrentUser
app.js       → hash router, theme handling, shared UI helpers
dashboard.js → stats + recent albums
albums.js    → album CRUD, search, sort
gallery.js   → album view, memories, favorites, lightbox
profile.js   → profile editing
```

## Routes

| Hash | View |
|---|---|
| `#/` | Landing page |
| `#/login` | Log in |
| `#/signup` | Create account |
| `#/dashboard` | Dashboard (requires login) |
| `#/albums` | All albums |
| `#/album/:id` | Single album |
| `#/memories` | All photos across albums |
| `#/favorites` | Favorited photos |
| `#/profile` | Profile |
| `#/settings` | Settings |

Visiting an app route while signed out redirects to `#/login`; visiting `#/login` or `#/signup` while signed in redirects to `#/dashboard`.

## Known limitations (demo scope)

- **Photos are placeholders.** Since this is a frontend demo with no backend, gallery "photos" are rendered as gradient tiles rather than real images.
- **Uploads don't persist across reloads.** The upload flow (drag-and-drop, file picker, live previews via `FileReader`) works, but uploaded images aren't written to storage — only demo metadata is. Swap in IndexedDB if you want uploaded images to survive a refresh.
- **Auth is for demonstration only.** Passwords are stored in plain text in `localStorage`. Do not reuse this pattern, or real credentials, in production — pair this frontend with a real backend and proper password hashing before handling actual user data.

## License

Free to use and adapt for personal or portfolio projects.
