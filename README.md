# AI-Powered IT Incident Analyzer

An AI-powered IT Incident Management system built using Java, Spring Boot, Ollama, Semantic RAG, and Docker.

The application analyzes incoming IT incidents using historical incident knowledge. It generates embeddings for historical incidents and the new incident, calculates semantic similarity using cosine similarity, retrieves the most relevant historical incident, and provides the retrieved context to a local Large Language Model (LLM) for AI-powered analysis.

---

## 🚀 Features

- AI-powered IT incident analysis
- Semantic Retrieval-Augmented Generation (RAG)
- Historical incident knowledge retrieval
- Text embeddings using Ollama `nomic-embed-text`
- Local LLM analysis using Ollama `llama3.2`
- Cosine similarity-based semantic search
- In-memory vector store
- Incident categorization
- Incident priority classification
- Root-cause analysis
- Recommended resolution
- RAG explainability
- Similarity score returned in API response
- Input validation
- Global exception handling
- REST API
- Swagger/OpenAPI documentation
- Docker containerization
- No database dependency

---

## 🏗️ Architecture

```text
                    ┌──────────────────────┐
                    │   Swagger / Postman  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ IncidentController   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   IncidentService    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │  IncidentRetriever   │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴───────────┐
                    │                      │
                    ▼                      ▼
          ┌─────────────────┐    ┌─────────────────────┐
          │ EmbeddingService│    │ InMemoryVectorStore │
          └────────┬────────┘    └──────────┬──────────┘
                   │                        │
                   ▼                        ▼
          ┌─────────────────┐     Historical Incidents
          │ Ollama           │              │
          │ nomic-embed-text │              │
          └────────┬────────┘              │
                   │                        │
                   └──────────┬─────────────┘
                              ▼
                   ┌──────────────────────┐
                   │ Cosine Similarity    │
                   └──────────┬───────────┘
                              │
                              ▼
                   ┌──────────────────────┐
                   │ Best Historical      │
                   │ Incident + Score     │
                   └──────────┬───────────┘
                              │
                              ▼
                   ┌──────────────────────┐
                   │     LLMService       │
                   └──────────┬───────────┘
                              │
                              ▼
                   ┌──────────────────────┐
                   │ Ollama llama3.2      │
                   └──────────┬───────────┘
                              │
                              ▼
                   ┌──────────────────────┐
                   │ AIAnalysisResponse   │
                   └──────────────────────┘
