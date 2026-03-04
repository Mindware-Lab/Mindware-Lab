# Zotero Sync

Responsibilities:
- read Zotero library/collections/tags
- normalize metadata into DB tables
- generate or update markdown citation notes

Minimum synced fields:
- zotero key
- title
- creators
- year
- journal
- DOI
- URL
- collection ids
- tags

All downstream RAG responses should be able to point back to a Zotero item key.