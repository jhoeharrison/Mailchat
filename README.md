# SecurePortal

A deployable public account portal with email/password registration, sign-in, and a separate administrator dashboard. The administrator can view registered email addresses and registration dates. User passwords are hashed with bcrypt and are never displayed to the administrator.

## Important security boundary

This site creates credentials for **SecurePortal only**. It must not be presented as Gmail, Google, or another provider's sign-in page, and it does not collect third-party passwords. The admin dashboard intentionally never reveals users' passwords.

## Run locally

1. Install Node.js 20 or newer.
2. Copy `.env.example` to `.env`.
3. Set `SESSION_SECRET` to a long random value and set `ADMIN_PASSWORD` to the administrator password you want to use. Keep `.env` private; never upload it to a public repository.
4. Run `npm install`.
5. Run `npm start` and open `http://localhost:3000`.

## Deploy publicly

Deploy this folder to a Node.js host (for example, Render, Railway, or a VPS). Set these environment variables in the host's private settings:

- `NODE_ENV=production`
- `SESSION_SECRET` = a long random secret
- `ADMIN_PASSWORD` = your chosen administrator password
- `DB_PATH` = a path on persistent storage, e.g. `/var/data/secureportal.sqlite`

Use a persistent disk mounted at that path so account data survives redeployments. Configure HTTPS and ensure the host supports Node.js 20+. Do not commit `.env`, database files, or session files. For larger deployments, use managed PostgreSQL and a shared persistent session store rather than a single-instance SQLite setup.

## Routes

- `/` — sign-in page
- `/register.html` — account registration
- `/admin.html` — administrator sign-in
- `/admin-dashboard.html` — protected administrator dashboard
- `/health` — health check
