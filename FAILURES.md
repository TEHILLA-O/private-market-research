# Failure modes, fixes, and results

Honest engineering notes for this project. Nothing here is invented for polish.

## What can go wrong

- **Supabase / DB unavailable on Vercel.** Impact: settings and dashboard errors. Mitigation: JSON store fallback locally; harden settings when Supabase is down; skip noisy `DATABASE_URL` hints when REST works.
- **News hub timeouts / upstream rate limits.** Impact: empty news panels. Mitigation: multi-provider free path (Hear API + RSS); cache news; fix timeout handling on Vercel (commits).
- **Duplicated API keys in headers** when env values are pasted twice. Impact: auth failures to Supabase. Mitigation: commit that de-duplicates key headers.
- **Treating free delayed data as live trading signal.** Impact: bad personal decisions. Mitigation: README disclaimer; not financial advice; free data called out as delayed/rate-limited.

## What went wrong

Commit evidence (real serverless/product fixes):

1. News hub timeouts and server errors on Vercel (`9dcfdd0`).
2. Settings page brittle when Supabase unavailable (`2dd64f2`).
3. Duplicate Supabase key in headers from pasted env (`8ee9fa3`).
4. Slow navigation without DB-first pages / skeletons (`e2ae831`).

## How it was resolved

- Supabase REST path, NGX features, and Vercel serverless fixes landed together (`d66a2b9`), then follow-up hardening commits above.
- Mock financials/news and deterministic DeepSeek mock when keys are missing so the UI stays explorable offline.

## Results

- Successful demo: `npm install`, `.env.local` optional keys, `npm run dev`, watchlist + score breakdown.
- Live Vercel app referenced in repo metadata. No claimed alpha/returns metrics.
