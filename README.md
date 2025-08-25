# RAG Stack (Qwen + Qdrant) on Ubuntu

End-to-end pipeline:
File Share -> Crawler -> Text Extractor -> Embeddings (bge-m3) -> Qdrant -> RAG API -> llama.cpp (Qwen 7B/14B)

## Components
- Ingestion worker (Python): crawls SMB/FS, extracts text with `unstructured`, chunks, embeds via `BAAI/bge-m3`, upserts into Qdrant.
- Vector DB: Qdrant (Docker).
- RAG API (FastAPI): retrieves from Qdrant and calls llama.cpp (`/completion`) on 7B (8080) or 14B (8081).
- Systemd services: `qwen3-7b`, `qwen3-14b`, `rag-app`, plus nightly `rag-ingest.timer`.

See `config/settings.yaml` for paths and knobs.
EOF
