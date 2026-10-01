# Rituals

Mobile-first routine planner PWA MVP. It uses Vite + vanilla TypeScript and localStorage, so it can be deployed as static files on Hostinger.

## Development

```bash
npm install
npm run dev
npm run build
```

Upload the contents of `dist/` to `public_html`. Configure Hostinger rewrite/fallback so `/rutina/<slug>` serves `index.html` (the app uses clean paths such as `/rutina/<slug>`. Add an `.htaccess` fallback in `public_html` so unknown paths serve `index.html` (Apache rewrite).).

### Audio

Sounds use the Web Audio API and are unlocked by tapping **Start**. A short tone plays at activity start, halfway (when enabled), and completion. Mobile browsers may suppress audio until a user gesture.

### Persistence and migration

Routine data is stored in `localStorage` under `routines`. The domain model is isolated in `src/main.ts`; replace the `save`/load calls with Supabase (or Hostinger MySQL API) later, keeping the same Routine/Activity shape.

Example `.htaccess` for Hostinger Apache:

```apache
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```
