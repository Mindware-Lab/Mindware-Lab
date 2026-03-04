# Architecture

## Product goal

Mindware Lab is a single research workspace with five integrated modules:
1. Knowledge bank (notes, papers, concept graph)
2. Cognitive app data pipeline and statistical analysis
3. Cloud experiment and survey builder
4. Computational modeling environment
5. Agentic research intelligence

## Shared data backbone

Use one canonical storage layer:
- relational store: PostgreSQL
- vector store: pgvector (same Postgres) or dedicated vector DB
- object storage: PDFs, experiment exports, model artifacts

Core entities:
- `paper`
- `concept`
- `concept_link`
- `note`
- `zotero_item`
- `app_event`
- `session`
- `participant`
- `experiment`
- `model_run`
- `agent_run`

## Integration boundaries

- Obsidian free tier reads and edits markdown in `knowledge-bank/obsidian-vault`.
- Zotero sync writes normalized citation metadata to `zotero_item` and a markdown citation index.
- RAG retrieval uses chunks derived from notes and PDFs, joined to citation ids.
- Agent outputs are proposals until they pass review rules.

## Guardrails

- No silent overwrites of manually edited notes.
- Evidence and speculative notes use different templates.
- Participant data workflows require explicit privacy checks and retention policy.