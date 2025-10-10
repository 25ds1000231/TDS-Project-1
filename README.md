# <PROJECT NAME>

**Live site:** https://OWNER.github.io/REPO/  
**API endpoint (health):** https://YOUR-API/health

## Summary
Briefly explains what the project does (accepts JSON POST, verifies secret, creates a public repo, adds MIT license, deploys GitHub Pages, posts evaluation callback with retries).

## Architecture
- Google Form / Client → **API** (`POST /webhook`)
- Secret verification → Minimal app generator (LLM-friendly hook)
- GitHub REST: create repo, push files, enable Pages via Actions
- Callback: POST to `EVALUATION_URL` with exponential backoff

## Setup
### Environment variables
- `SHARED_SECRET`: shared secret that incoming JSON must match
- `GITHUB_TOKEN`: PAT with `repo` (or `public_repo`) and `workflow`
- `GITHUB_OWNER`: your GitHub username/org
- `EVALUATION_URL`: evaluator callback URL

### Local run
```bash
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8080
