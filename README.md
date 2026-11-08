# Mirror Vibes

**Try a dress before you decide.** Mirror Vibes lets a shopper lift a dress from a photo, preview it on their own photo, and keep the pieces and results they want to revisit.

This repository is the Mirror Vibes project copy. The current app is built around the **Try-On Commerce** track: one clear dress try-on flow supported by a personal wardrobe and saved looks.

## What the app does

1. Choose a sample dress or upload a clear garment photo.
2. Review the garment extraction made in the browser.
3. Add a front-facing photo of yourself.
4. Generate a virtual try-on preview with the server-side YouCam AI-Cloth integration.
5. Save a garment or result to your wardrobe, or download the result.

The app also contains other experimental styling pages. They are not part of the main hackathon demonstration because the dress workflow aligns most closely with the commerce challenge.

## API and hackathon fit

The current code integrates Perfect Corp's YouCam AI-Cloth virtual try-on through server routes. The API key stays on the server. The hackathon's Devpost page currently still shows `[YOUR TRY-ON API NAME]` in its requirements, so confirm with the organizers that YouCam is the required or accepted provider before describing this project as compliant with that API requirement.

The project is intended for the **Try-On Commerce** track. Its value is helping shoppers preview a garment before buying and keeping the garments and results they want to revisit.

## Run locally

### Requirements

- Node.js 24.14 or newer
- npm
- A Perfect Corp YouCam API key for live try-on
- Supabase project credentials only if you want cloud storage and cloud try-on history

### Setup

```powershell
git clone https://github.com/Edv6-tech/mirror-vibes.git
cd mirror-vibes
npm ci
Copy-Item .env.example .env.local
```

Set `YOUCAM_API_KEY` in `.env.local` for live try-on. Never put the key in a `NEXT_PUBLIC_` variable or commit it. Start the app with:

```powershell
npm run dev
```

Open `http://localhost:3000`. The app uses SQLite for email and password accounts. By default, the database is created at `data/mirror-moment.sqlite`; set `SQLITE_DB_PATH` to change its location.

### Optional cloud storage

The app can use Supabase for private uploaded assets and saved try-on records. Set `SUPABASE_URL` and the server-only `SUPABASE_SECRET_KEY`, then apply the SQL migrations in `supabase/migrations` to the project. Do not expose the secret key to the browser. A production deployment also needs persistent storage for the SQLite database.

## Images and privacy

Garment extraction runs in the browser. To create a try-on, the person's photo and garment image are sent to the configured try-on provider. If cloud storage is configured, saved assets are stored in private buckets. Only use photos you have permission to process, and do not upload photos of minors.

## Useful routes

- `/` — project landing page
- `/login` and `/signup` — email and password account access
- `/app` — fashion dashboard
- `/app/studio` — dress try-on flow
- `/app/wardrobe` — saved garment collection
- `/app/looks` — saved try-on results
- `/app/settings` — account and privacy controls

## Environment variables

Copy `.env.example` to `.env.local` and fill only the values needed for your setup. Keep all secret values local. `.env.local` is ignored by Git.

## Hackathon submission checklist

- Confirm the exact try-on API required by the organizers.
- Provide judges with a working demo account or another reliable testing path.
- Include screenshots and a public 1 to 3 minute demo video that shows the app running and explains the API integration.
- Explain any significant changes made to the existing project during the submission period.
