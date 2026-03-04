# Mindware Lab

A research platform scaffold for:
- knowledge bank and concept graph
- ingestion and analysis of cognitive app data
- cloud experiment and survey delivery
- computational brain-network modeling
- agent-based research scouting and synthesis

This structure is designed to work with:
- VSCode + Codex for build and automation
- GitHub for versioning and workflows
- Obsidian free tier for graph exploration and note navigation
- Zotero as the citation backbone with RAG-ready retrieval

## Directory map

```text
mindware-lab/
  README.md
  docs/
    ARCHITECTURE.md
    IMPLEMENTATION_PLAN.md
  components/
    knowledge-bank/
      README.md
      obsidian-vault/
        README.md
      zotero-sync/
        README.md
      rag/
        README.md
    data-pipeline/
      README.md
      schemas/
        README.md
      notebooks/
        README.md
    experiment-cloud/
      README.md
    computational-modeling/
      README.md
    research-intel-agents/
      README.md
  infra/
    db/
      README.md
    vector/
      README.md
    orchestration/
      README.md
  workflows/
    github-actions/
      README.md
  configs/
    env/
      README.md
```

## Design rules

1. Keep claims and hypotheses separate from evidence-backed notes.
2. Every generated summary must carry provenance (`source`, `date`, `model`, `confidence`).
3. Store public app analytics in structured tables before any modeling.
4. Keep Obsidian as a UI layer over markdown, not the system of record.
5. Prefer human review before auto-merging agent-proposed knowledge links.

## Next action

Start with [docs/IMPLEMENTATION_PLAN.md](./docs/IMPLEMENTATION_PLAN.md).