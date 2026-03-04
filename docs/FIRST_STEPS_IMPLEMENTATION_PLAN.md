# First Steps Implementation Plan (v1)

This plan is the execution companion to `docs/IMPLEMENTATION_PLAN.md`.

## Goal for first 14 days

Ship a working foundation with:
1. Zotero + OSF metadata sync into one DB schema.
2. Markdown note generation into the Obsidian vault.
3. Citation-grounded RAG query command.
4. One cognitive app data ingestion path and one baseline analysis notebook.

## Ground rules

1. Canonical metadata lives in Postgres, not in Obsidian.
2. Every generated summary stores provenance (`source`, `date`, `model`, `confidence`).
3. Scheduled jobs are read/sync mode only unless manually approved.
4. No public publish flow (OSF/preprints) in automated jobs during MVP.

## Week 1: Foundations and knowledge sync

### Day 1: Repo and runtime baseline

Tasks:
1. Add `.env.example` with required keys (`DATABASE_URL`, `OPENAI_API_KEY`, `ZOTERO_API_KEY`, `ZOTERO_USER_ID`, `OSF_API_TOKEN`, `OSF_PROJECT_ALLOWLIST`).
2. Choose Python runtime and dependency manager.
3. Add base project structure for scripts and tests.

Deliverables:
- environment contract committed
- local app boots without secrets

### Day 2: Database schema and migrations

Tasks:
1. Create initial migration for:
- `zotero_item`
- `osf_node`
- `osf_file`
- `osf_preprint`
- `paper`
- `concept`
- `concept_link`
- `note`
2. Add unique constraints and sync timestamps.
3. Add minimal seed data command.

Deliverables:
- migration applies cleanly
- schema documented in `infra/db`

### Day 3: Zotero sync MVP

Tasks:
1. Build `zotero-sync` command for metadata pull.
2. Upsert items into `zotero_item`.
3. Log run summary (`items_fetched`, `items_upserted`, `errors`).

Deliverables:
- first successful sync run
- deterministic rerun behavior (idempotent)

### Day 4: OSF sync MVP

Tasks:
1. Build `osf-sync` command for nodes/files/preprints metadata pull.
2. Restrict sync using `OSF_PROJECT_ALLOWLIST`.
3. Upsert `osf_node`, `osf_file`, `osf_preprint` with visibility flags.

Deliverables:
- first successful OSF metadata sync
- private/embargo metadata preserved in DB

### Day 5: Markdown note generation + Obsidian integration

Tasks:
1. Define templates for paper and dataset notes.
2. Generate markdown notes from Zotero + OSF records into `components/knowledge-bank/obsidian-vault`.
3. Add safe overwrite rules (template-managed sections only).

Deliverables:
- note generation command
- Obsidian graph renders generated links

## Week 2: Retrieval and app data baseline

### Day 6: Chunking and embeddings

Tasks:
1. Chunk markdown notes and extracted PDF text.
2. Generate embeddings and store vector references.
3. Track chunk source ids back to Zotero/OSF records.

Deliverables:
- vector index populated for at least one test corpus

### Day 7: Query interface (RAG)

Tasks:
1. Build `ask` command (`ask "question"`).
2. Return answer plus citation list.
3. Add "citation-first" retrieval preference (curated corpus before web).

Deliverables:
- reproducible query responses with source references

### Day 8: Cognitive app event schema

Tasks:
1. Define v1 event schema in `components/data-pipeline/schemas`.
2. Include required fields for sessions, tasks, responses, timing, and state.
3. Add schema validation tests.

Deliverables:
- versioned schema with passing tests

### Day 9: Ingestion path MVP

Tasks:
1. Build one importer for a selected Trident app event export.
2. Load validated rows into DB.
3. Emit run report with reject reasons for invalid rows.

Deliverables:
- ingestion run from sample export to DB

### Day 10: Baseline analysis notebook

Tasks:
1. Create first notebook for descriptive metrics and longitudinal trend preview.
2. Export summary table and one figure.
3. Document notebook inputs/outputs and assumptions.

Deliverables:
- reproducible notebook output committed

### Day 11-14: Hardening buffer

Tasks:
1. Add CI checks (lint + tests + migration checks).
2. Add scheduled workflows for Zotero sync, OSF sync, embedding refresh.
3. Add run logs and basic alerting for failed jobs.
4. Close top reliability issues found during dry runs.

Deliverables:
- automated scheduled runs configured
- minimum reliability checklist complete

## Definition of done (first-steps milestone)

1. You can sync Zotero and OSF into DB on schedule.
2. You can generate linked markdown notes for Obsidian.
3. You can ask a question and get citation-grounded output.
4. You can ingest one app's data and produce a baseline analysis report.

## Immediate next command backlog

1. `bootstrap-env`: validate required environment variables.
2. `migrate-db`: run all pending DB migrations.
3. `sync-zotero`: metadata sync + run logs.
4. `sync-osf`: metadata sync with allowlist.
5. `build-notes`: markdown generation for Obsidian vault.
6. `embed-corpus`: chunk + embed markdown/PDF text.
7. `ask`: citation-grounded RAG query.
8. `import-events`: ingest one cognitive app export.
9. `run-baseline-notebook`: produce table + figure artifacts.

## What to do first today

1. Approve runtime stack (Python + dependency manager + migration tool).
2. Implement `.env.example` and migration skeleton.
3. Build `sync-zotero` before `sync-osf`.
4. Run one end-to-end dry run: sync -> note generation -> one `ask` query.