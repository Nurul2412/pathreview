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

---


# Week 8 – Reproduction

## Reproduction summary

I created a new unit test to reproduce Issue #27 by ingesting a document, modifying its contents, and re-ingesting it using the same `source_id`. The expected behavior was that the vector store would replace the old document with the updated one.

## Test performed

1. Created a document with the text:
   - "Original document says Python."
2. Ingested the document into the vector store.
3. Updated the document text to:
   - "Updated document says Rust."
4. Re-ingested the document using the same `source_id`.
5. Queried the stored document from the vector store.

## Result

The test failed because the vector store still returned the original document instead of the updated one.

**Expected:**

```
Updated document says Rust.
```

**Actual:**

```
Original document says Python.
```

This confirms that stale embeddings remain after re-ingesting a document and successfully reproduces Issue #27 in my local environment.

## Files investigated

- `tests/unit/test_batch_processor.py`
- `ingestion/embeddings/batch_processor.py`
- `ingestion/embeddings/provider.py`
- `rag/vector_store.py`