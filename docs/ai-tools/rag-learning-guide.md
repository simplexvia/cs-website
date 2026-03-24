

# RAG Pipeline Learning Guide for DevOps Engineers

**Quick-start guide to Retrieval-Augmented Generation (RAG)** – tailored for DevOps / Platform Engineers with 20+ years of cloud, GitOps, Kubernetes (EKS), Terraform, Helm, ArgoCD, and AWS experience (aligned with SimplexVia-style consulting: enterprise-grade, GitOps-driven, AWS-native AI platforms).

**Current date reference**: March 23, 2026  
RAG remains the dominant production pattern for grounded, hallucination-resistant GenAI applications in regulated industries (finance, healthcare, manufacturing, telecom).

## What is RAG? (30-second version)

RAG = **Retrieval** + **Augmented** + **Generation**  
Instead of pure LLM prompting ("answer from your training data"), RAG first **retrieves** relevant, up-to-date, private documents from your enterprise sources → injects them into the prompt → generates accurate, cited answers.

**Key benefits** (why enterprises love it):
- Zero/few hallucinations when grounded in your data
- Always current (no retraining needed)
- Data privacy & compliance (your data never trains public models)
- Citations / traceability for regulated use cases

## Core RAG Pipeline – Two Phases

### 1. Indexing Pipeline (Offline / Batch – GitOps-triggered)
Goal: Convert your knowledge base into searchable vectors.

Typical steps:
1. Ingest documents (PDFs, Markdown, Confluence, SharePoint, S3, Git repos, databases)
2. Chunk intelligently (semantic, fixed-size with overlap, or hierarchical)
3. Generate embeddings (vector representations) using models like:
   - Amazon Titan Embeddings (Bedrock)
   - text-embedding-3-large (OpenAI)
   - bge-m3 / multilingual models
4. Store in vector database/index:
   - Amazon OpenSearch Serverless (vector engine)
   - PGVector (Aurora PostgreSQL)
   - Pinecone, Weaviate, Chroma

**DevOps view**: This is a scheduled / event-driven ETL pipeline (Argo Workflows, EventBridge + Lambda, GitHub Actions on merge).

### 2. Query Pipeline (Online / Real-time Inference)
Goal: Answer user questions with grounded context.

Typical steps:
1. Embed user query
2. Semantic search: retrieve top-k chunks (cosine similarity / hybrid)
3. Optional: Rerank (Cohere Rerank, cross-encoder models)
4. Build prompt: "Use ONLY the following context: [chunks] Question: ..."
5. Call LLM (Claude 3.5 Sonnet, Llama 3.1, Amazon Titan, etc. via Bedrock)
6. Return answer + sources/citations

**DevOps view**: Low-latency inference service (often FastAPI/Flask + LangChain/LlamaIndex, deployed on EKS with autoscaling).

## Visual Flow (Reference Diagrams)

Here are clean architecture diagrams commonly used to explain RAG:

(First shows end-to-end flow; second highlights offline indexing vs. runtime query separation – perfect for GitOps thinking.)

## Mapping to Your Existing Skills (SimplexVia / Enterprise DevOps Lens)

| Your Skill                          | RAG Equivalent                                      | Tools / AWS Services You Already Use                     |
|-------------------------------------|-----------------------------------------------------|----------------------------------------------------------|
| GitOps (ArgoCD, Flux)               | Index refresh on doc change / schedule              | Argo Workflows + Cron, EventBridge → Lambda → Bedrock embed → upsert vector DB |
| Kubernetes / EKS                    | Deploy vector DB, embedding service, query app      | Helm charts for PGVector / OpenSearch, vLLM/TGI for LLM, LangChain as microservice |
| Terraform / IaC                     | Provision vector store, Bedrock KB, networking      | Terraform modules for OpenSearch Serverless, Bedrock KB, Aurora PGVector |
| CI/CD on merge                      | Re-index on Git push / Confluence update            | GitHub Actions / GitLab CI → trigger indexing pipeline   |
| Monitoring / Observability          | RAG-specific metrics                                | Prometheus + Grafana, LangSmith/Phoenix, CloudWatch (latency, retrieval recall, hallucination score via evals) |
| AWS expertise + Amazon Q            | Fully managed / custom RAG                          | Amazon Q Business (connectors to S3, Confluence, etc.) OR custom on Bedrock + OpenSearch |

**Bottom line**: RAG is **another data + inference pipeline** – just swap traditional ETL/DB for embeddings + vector search. The rest (GitOps, K8s ops, IaC, observability) is your daily work.

## Quick Start Paths (Pick Your Flavor – 2026 Ready)

1. **Fastest / Managed**  
   Amazon Q Business → connect data sources → done (enterprise RAG out-of-box).  
   Great for PoCs / regulated environments.

2. **Custom + GitOps (recommended for control)**  
   - Use Bedrock (Titan Embed + Claude)  
   - Vector store: OpenSearch Serverless or PGVector  
   - Orchestration: LangChain / LlamaIndex  
   - Deploy: Terraform + Helm + ArgoCD on EKS

3. **Reference Repos to Fork & Adapt** (AWS-official, production-grade templates)

   - https://github.com/aws-samples/terraform-rag-template-using-amazon-bedrock  
     (Terraform + Bedrock + Titan Embed + Claude – simple RAG use case)

   - https://github.com/aws-samples/amazon-bedrock-rag  
     (Fully managed Knowledge Bases for Bedrock – ingestion to retrieval)

   - https://github.com/aws-samples/rag-using-langchain-amazon-bedrock-and-opensearch  
     (LangChain + Bedrock Titan Embed + OpenSearch vector search)

   - https://github.com/aws-samples/sample-bedrock-knowledge-base-terraform  
     (Terraform template for Bedrock Knowledge Bases – great for IaC-first)

Start by cloning one of the above, adapt to your EKS cluster / GitOps repo, and trigger indexing via Argo Workflows on doc changes.

You can have a production-grade RAG app running in days – then offer it as "AI Platform Operations" to clients.

