# Environment Configuration

Document required environment variables and secret scopes.

Core variables:
- `DATABASE_URL`
- `OPENAI_API_KEY`

Knowledge bank integrations:
- `ZOTERO_API_KEY`
- `ZOTERO_USER_ID`
- `OSF_API_TOKEN`
- `OSF_PROJECT_ALLOWLIST` (comma-separated project IDs to sync)

Research scout integrations:
- `SEMANTIC_SCHOLAR_API_KEY`
- `PUBMED_EMAIL`

Guidance:
- keep secrets in local `.env` and GitHub Actions secrets
- use allowlists to avoid accidental sync of private OSF projects