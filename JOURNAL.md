## Week 7 – Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/27

**Issue title:** Vector store returns stale embeddings after a document is re-ingested

**Tier:** [ ] Tier 1 [ ] Tier 2 [x] Tier 3

**Problem summary:**  
When an existing document is re-ingested, the application does not fully replace the document's previous vectors. As a result, the vector store can continue returning outdated chunks and embeddings from the older version of the document. A successful fix would remove or replace the old vectors before storing the newly generated embeddings, ensuring retrieval results always reflect the latest document content.

**Selection notes:**  
I chose this issue because I have previously worked with document ingestion in the Unofficial Guide project, so I already understand the general ingestion workflow. The issue is focused enough to investigate while also helping me improve my understanding of vector stores and RAG systems. I will likely need to trace how document IDs, chunks, and vector-store records are handled during re-ingestion.

**Branch name:** `fix/27-stale-embeddings`

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger