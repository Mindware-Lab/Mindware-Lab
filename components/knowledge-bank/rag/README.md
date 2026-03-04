# RAG Layer

Goal:
- answer research questions grounded in your own notes and citations first

Pipeline:
1. chunk markdown and extracted PDF text
2. embed chunks
3. store embeddings with chunk metadata
4. retrieve top chunks for query
5. generate answer with explicit citations

Quality rule:
- no citation, no claim