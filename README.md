# Patch

A self-hosted changelog for products that ship.

Patch gives your team a polished public release feed and a private editor. Publish versioned updates, organize them by category, let readers subscribe through RSS, and keep the data on infrastructure you control.

## Features
- Responsive public changelog with search and category filters
- Private admin workspace to create, edit, publish, unpublish, and delete releases
- RSS 2.0 feed at `/feed.xml`
- SQLite persistence with no external database service
- Bearer-token protected write API
- Docker and Render deployment examples
- Small dependency footprint; safe, limited Markdown renderer

## Quick start
Requires Node.js 22+.

```bash
git clone https://github.com/Shushirolsh-Dev/Patch.git
cd Patch
cp .env.example .env
npm install
npm run dev
```

Open `http://localhost:3000`. Set a strong `ADMIN_TOKEN` in `.env`, then visit `/admin` to manage releases.

## Configuration

| Variable | Default | Description |
|---|---|---|
| `PORT` | `3000` | HTTP port |
| `HOST` | `0.0.0.0` | Bind address |
| `ADMIN_TOKEN` | — | Required admin secret |
| `SITE_NAME` | `Patch` | Feed and RSS title |
| `SITE_URL` | `http://localhost:3000` | Canonical public URL |
| `DATABASE_PATH` | `./data/patch.db` | SQLite database path |

## API

Write endpoints require `Authorization: Bearer <ADMIN_TOKEN>`.

| Method | Path | Access |
|---|---|---|
| GET | `/api/health` | Public |
| GET | `/api/releases?q=&category=` | Public |
| GET | `/api/releases/:slug` | Public |
| GET | `/feed.xml` | Public |
| GET | `/api/admin/releases` | Admin |
| POST | `/api/admin/releases` | Admin |
| PATCH | `/api/admin/releases/:id` | Admin |
| DELETE | `/api/admin/releases/:id` | Admin |

Categories: `New`, `Improved`, `Fixed`, `Security`.

## Production checklist
- Replace the example admin token with a long random secret.
- Serve the app behind HTTPS.
- Persist the configured database directory and back it up.
- Run one app instance with local SQLite; use shared database infrastructure for horizontal scaling.
- Keep `.env` and database files out of version control.

## Scripts
- `npm run dev` — development server with watch mode
- `npm start` — production server
- `npm test` — Node test suite

## License
MIT.
