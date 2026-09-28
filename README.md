# Verifluence

**Check how trustworthy an influencer campaign really is.**

Verifluence analyzes an influencer's post and produces a transparent trust report. It checks whether the post is sponsored and properly disclosed, whether the creator's numbers look unusual, and whether the claims made in the caption or video are backed by real evidence from the web, news, and scholarly sources.

> Built for the SerpApi India Hackathon 2026.

---

## What it does

| Area | What we check |
|------|---------------|
| **Sponsored detection** | `#ad`, promo codes, affiliate links, and whether disclosure is found, missing, or unclear |
| **Creator signals** | Engagement anomalies, growth anomalies, repetitive or similar comments, audience fit |
| **Claim verification** | Extracts atomic claims, searches for evidence, and marks each as supported, contradicted, or not found |
| **Evidence explorer** | Clickable sources per claim, classified as research, government, news, influencer, and so on |
| **Risk report** | Combined review level with confidence, with a stricter mode for health and finance claims |

**Principle:** "not found" is not the same as "unqualified". The report always includes a limitations note.

---

## Tech stack

- **Backend:** FastAPI, PostgreSQL, SQLAlchemy
- **Frontend:** React, Vite, Tailwind CSS
- **Evidence search:** SerpApi (web, news, Scholar)
- **AI:** LLM for claim extraction, query generation, and claim-vs-evidence comparison

---

## How it works

```
URL / caption  ->  extraction  ->  creator intel + sponsored detection
                                        |
                                        v
                          claims  ->  evidence (SerpApi)
                                        |
                                        v
                                   risk  ->  report
```

---

## Project structure

```
Verifluence/
├── backend/     # FastAPI app: api, extraction, claims, evidence, risk, report
└── frontend/    # React app: Home, Analyzing, Report pages
```

Each folder has its own detailed structure once its branch is merged.

---

## API endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/analyze` | POST | Start analysis, returns `report_id` |
| `/reports/{id}/status` | GET | Progress of each pipeline step |
| `/reports/{id}` | GET | Full report JSON |
| `/claims/{id}/evidence` | GET | Sources for one claim |
| `/health` | GET | Server check |

---

## Getting started

### Backend
```bash
cd backend
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env            # add your keys
uvicorn app.main:app --reload
```
API docs: http://localhost:8000/docs

### Frontend
```bash
cd frontend
npm install
npm run dev
```
App: http://localhost:5173

### Environment variables

| Variable | Used for |
|----------|----------|
| `DB_URL` | PostgreSQL connection string |
| `SERPAPI_KEY` | Evidence search |
| `LLM_KEY` | Claim extraction and comparison |
| `VITE_API_URL` | Frontend, backend base URL |

---

## Git workflow

```
main       stable, final release only
 └── default    integration branch
      ├── backend    API, SerpApi, claims, risk engine
      └── frontend   UI, report, components
```

Short feature branches are created from `backend` or `frontend`, merged upward, and `default` is merged into `main` only for the final release.

---

## Build status

- [ ] Backend setup (FastAPI, DB, `/health`, `/analyze` stub)
- [ ] Claim extraction
- [ ] SerpApi client and caching
- [ ] Evidence classifier and verdicts
- [ ] Sponsored and disclosure detection
- [ ] Risk engine and report
- [ ] Creator intel
- [ ] Advanced (escalation, timeline, health mode)
- [ ] Frontend pages

---

## Limitations

Verifluence is a review aid, not a final judgment. Results depend on available public data and search coverage. A missing source does not prove a claim is false, and a flagged signal does not prove wrongdoing. Always read the evidence yourself.

---

## License

To be decided.
