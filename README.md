# Mike

Open-source release containing the Mike frontend and backend.

## Contents

- `frontend/` - Next.js application
- `backend/` - Express API, Supabase access, document processing, and migrations
- `backend/migrations/000_one_shot_schema.sql` - one-shot Supabase schema for fresh databases

## Setup

Install dependencies:

```bash
npm install --prefix backend
npm install --prefix frontend
```

Create local env files from the examples:

```bash
cp backend/.env.example backend/.env
cp frontend/.env.local.example frontend/.env.local
```

Run `backend/migrations/000_one_shot_schema.sql` in the Supabase SQL editor for a fresh database.

Start the backend:

```bash
npm run dev --prefix backend
```

Start the frontend:

```bash
npm run dev --prefix frontend
```

Open `http://localhost:3000`.

## Required Services

- Supabase Auth and Postgres
- S3-compatible object storage, such as Cloudflare R2
- At least one supported model provider key, depending on which models you enable
- LibreOffice for DOC/DOCX to PDF conversion

## Environment Variables

### Backend (`backend/.env`)

| Variable | Description |
|----------|-------------|
| `SUPABASE_URL` | Supabase project URL |
| `SUPABASE_SECRET_KEY` | Supabase service-role key |
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase public URL (used by workflow helpers) |
| `R2_ENDPOINT_URL` | Cloudflare R2 S3-compatible endpoint |
| `R2_ACCESS_KEY_ID` | R2 API token Access Key ID |
| `R2_SECRET_ACCESS_KEY` | R2 API token Secret Access Key |
| `R2_BUCKET_NAME` | R2 bucket name (default: `mike`) |
| `DOWNLOAD_SIGNING_SECRET` | Secret for signing download tokens (falls back to `SUPABASE_SECRET_KEY`) |
| `ANTHROPIC_API_KEY` | Anthropic (Claude) API key |
| `GEMINI_API_KEY` | Google Gemini API key |
| `PORT` | Server port (default: `3001`) |
| `FRONTEND_URL` | Allowed CORS origin (default: `http://localhost:3000`) |

### Frontend (`frontend/.env.local`)

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL (client-side) |
| `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_DEFAULT_KEY` | Supabase anon/public key |
| `SUPABASE_SECRET_KEY` | Supabase service-role key (server-side) |
| `NEXT_PUBLIC_API_BASE_URL` | Backend API base URL (default: `http://localhost:3001`) |
| `R2_ENDPOINT_URL` | Cloudflare R2 endpoint (server-side) |
| `R2_ACCESS_KEY_ID` | R2 Access Key ID (server-side) |
| `R2_SECRET_ACCESS_KEY` | R2 Secret Access Key (server-side) |
| `R2_BUCKET_NAME` | R2 bucket name (default: `mike`) |

## Checks

```bash
npm run build --prefix backend
npm run build --prefix frontend
npm run lint --prefix frontend
```

## License

AGPL-3.0-only. See `LICENSE`.
