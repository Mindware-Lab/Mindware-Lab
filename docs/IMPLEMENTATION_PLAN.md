# Implementation Plan

This plan assumes Obsidian free tier for graph exploration and VSCode + GitHub as the engineering base.

## Phase 0 (Day 0-2): Platform bootstrap

1. Create `.env` contract for API keys and DB connection strings.
2. Stand up Postgres + pgvector locally.
3. Define initial schema for papers, concepts, links, zotero items, and app events.
4. Add GitHub Actions skeleton for lint, unit tests, and scheduled ingestion jobs.

Exit criteria:
- local stack runs
- DB migrations apply cleanly
- CI workflow triggers on pull requests

## Phase 1 (Week 1): Knowledge bank + Zotero + Obsidian

1. Build Zotero sync job:
- pull collections, items, tags, and attachment metadata
- map into normalized `zotero_item` table
2. Define markdown note template for papers and concepts.
3. Generate/update markdown files from Zotero items.
4. Configure Obsidian vault path to `components/knowledge-bank/obsidian-vault`.
5. Add concept-linking script that injects wiki links with confidence thresholds.

Exit criteria:
- new Zotero item appears in DB and markdown
- Obsidian graph displays linked notes
- link injection runs idempotently

## Phase 2 (Week 2): RAG query layer

1. Implement text chunking for markdown and PDF text.
2. Create embeddings pipeline and vector index updates.
3. Build query API/CLI that returns answer + cited sources.
4. Add citation-first retrieval mode: prioritize your Zotero library before open web sources.

Exit criteria:
- `ask "question"` returns cited answer with source ids
- retrieval logs stored for evaluation

## Phase 3 (Week 3): Cognitive app ingestion and stats pipeline

1. Define event schema for your apps (session, task, response, timing, state labels).
2. Implement ingestion endpoint or batch importer.
3. Add quality checks (missing fields, out-of-range latency, duplicate sessions).
4. Build baseline analysis notebooks (descriptives, reliability, longitudinal trends).

Exit criteria:
- one app exports events into DB
- notebook produces repeatable summary tables and figures

## Phase 4 (Week 4-5): Experiment cloud runtime

1. Build experiment config schema (tasks, randomization, consent, completion rules).
2. Build minimal web runtime to deliver tasks and capture responses.
3. Add participant/session lifecycle and export pipeline.
4. Link each experiment version to Zotero references.

Exit criteria:
- deploy one experiment in cloud
- data lands in DB with version traceability

## Phase 5 (Week 6+): Computational modeling and research agents

1. Implement model-run job system (queued execution, parameter sweeps, artifact tracking).
2. Add paper scout agents for PubMed/arXiv/bioRxiv/Semantic Scholar.
3. Add critique agent that challenges summaries and hypothesis claims.
4. Add human review gate for auto-generated graph links and hypotheses.

Exit criteria:
- reproducible model run from saved config
- nightly scout run opens review-ready updates

## Suggested order for your first 10-hour prototype

1. Zotero sync minimal metadata
2. Paper markdown generation
3. Basic concept linking
4. Embeddings + simple Q/A with citations
5. One app event import + one stats notebook

## Risks to manage early

- data privacy and consent boundaries for participant data
- false confidence from low-quality auto-links
- citation drift when PDFs change or metadata is incomplete
- uncontrolled agent writes without review checkpoints