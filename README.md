# AI Market Research GPT — Ready-to-run Repo

This repository contains:
- `server/` — Node/Express server that computes company health metrics (FCF, Gross Profit Margin, Interest Coverage, etc.) using a pluggable data provider adapter.
- `frontend/` — Minimal React UI that calls the server and lets you download XLSX.
- `Dockerfile` & `docker-compose.yml` — Run server + Redis locally.
- `.github/workflows/ci.yml` — CI workflow scaffold.
- `vercel.json` — Example Vercel configuration for serverless deployment.
- `cloudflare/worker.js` — Example Cloudflare Worker proxy.

## Quickstart (local with Docker Compose)
1. Create an environment file `.env` with your API key:
   ```
   FMP_API_KEY=your_fmp_key
   ```
2. Start services:
   ```
   docker-compose up --build
   ```
3. Server will be available at `http://localhost:4000`.
   Use POST `/api/metrics` with JSON `{"tickers":["AAPL","MSFT"]}`.

## Production notes
- Set `DATA_PROVIDER` environment variable to choose provider (e.g., `FMP` or `ALPHAVANTAGE`).
- Provide provider API keys via env vars (`FMP_API_KEY`, `ALPHAVANTAGE_KEY`).
- If you set `REDIS_URL`, the server will use Redis for caching; otherwise it uses in-memory cache.
- For edge/serverless deployments:
  - Vercel: Add `FMP_API_KEY` as a project secret and deploy.
  - Cloudflare Workers: Use the worker as a proxy or repoint the API to a hosted server.

## Files created
- server/index.js
- server/package.json
- frontend/src/App.jsx
- frontend/package.json
- Dockerfile
- docker-compose.yml
- .github/workflows/ci.yml
- vercel.json
- cloudflare/worker.js

## Notes
- This is a production-ready scaffold but you should:
  - Add error handling & retries for provider rate limits.
  - Add authentication and per-user rate limiting.
  - Add tests and monitoring.
  - Replace placeholder frontend build script with a real build (CRA/Vite).
