# Neel Patel — Portfolio with Backend & Admin Dashboard

## What's in this folder

| File | Purpose |
|---|---|
| `neel-patel-portfolio.html` | The portfolio site (works standalone OR with the backend) |
| `server.js` | Express backend — serves the site + API |
| `admin.html` | Admin dashboard (add/delete projects, read messages) |
| `data/db.json` | Your database — projects and contact messages |
| `package.json` | Dependencies (just Express) |

## Run it locally

```bash
npm install
ADMIN_PASSWORD=your-secret-password node server.js
```

Then open:
- **http://localhost:3000** — your portfolio
- **http://localhost:3000/admin** — your dashboard (sign in with the password you set)

On Windows (PowerShell): `$env:ADMIN_PASSWORD="your-secret-password"; node server.js`

⚠️ If you don't set `ADMIN_PASSWORD`, it defaults to `change-me-123`. Never deploy with the default.

## How it works

- **Projects**: The site loads projects from `/api/projects`. Add or delete them in the dashboard — changes appear on the site on next page load. New projects only need a title + short description; empty fields (gallery, before/after, etc.) are hidden automatically.
- **Contact messages**: The contact form and consultation bookings POST to `/api/contact` and appear in the dashboard's Messages tab with unread indicators.
- **Standalone mode**: If you host `neel-patel-portfolio.html` alone (GitHub Pages etc.), it still works — projects fall back to the built-in ones, and the contact form falls back to opening the visitor's email app.

## Deploy for free

**Render.com** (recommended, free tier):
1. Push this folder to a GitHub repo.
2. On render.com: New → Web Service → connect the repo.
3. Build command: `npm install` · Start command: `node server.js`
4. Add environment variable `ADMIN_PASSWORD` = your secret.

Railway.app and Fly.io work the same way. Note: on free tiers the filesystem may reset on redeploy — back up `data/db.json` occasionally (it's just a file you can copy).

## API reference

| Method | Path | Auth | Purpose |
|---|---|---|---|
| POST | `/api/login` | — | `{password}` → `{token}` |
| GET | `/api/projects` | — | List projects |
| POST | `/api/projects` | Bearer | Add project |
| PUT | `/api/projects/:id` | Bearer | Update project |
| DELETE | `/api/projects/:id` | Bearer | Delete project |
| POST | `/api/contact` | — | Submit contact message / booking |
| GET | `/api/contacts` | Bearer | List messages |
| PATCH | `/api/contacts/:id/read` | Bearer | Mark read |
| DELETE | `/api/contacts/:id` | Bearer | Delete message |
