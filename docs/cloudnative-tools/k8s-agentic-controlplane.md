# Sympozium: Kubernetes-Native Agentic Control Plane

## Overview
Sympozium is an open-source, Kubernetes-native platform for running fleets of AI agents to orchestrate workflows and administer clusters agentically. Every agent runs as an ephemeral Pod (via Jobs), policies as Custom Resource Definitions (CRDs), and executions as Jobs, ensuring isolation, scalability, and security. It supports multi-agent collaboration, model-agnostic AI providers (e.g., OpenAI, Anthropic, Ollama), and integrations with messaging channels like Slack, Telegram, Discord, and WhatsApp. Built by the creator of k8sgpt, it's designed for DevOps and SRE teams to automate cluster ops with declarative, GitOps-friendly resources.

## Key Features
- **Ephemeral Agents**: Isolated Pods/Jobs with resource limits and auto-cleanup.
- **PersonaPacks**: Pre-bundled agent configurations (e.g., SRE On-Call, Security Auditor) with prompts, skills, schedules, and memory.
- **Skill Sidecars**: Tools like kubectl, Helm in separate containers with ephemeral, least-privilege RBAC.
- **Multi-Channel Support**: Dedicated pods for Slack, Telegram, etc., using NATS JetStream.
- **Persistent Memory**: ConfigMap-backed for context across runs.
- **Scheduling**: CRD-based cron tasks for recurring ops.
- **Observability**: TUI (k9s-style), web dashboard, kubectl logs/events.
- **Security**: NetworkPolicies, non-root containers, admission webhooks, multi-tenancy.

## Architecture
- **Control Plane**: Stateless controller, NATS event bus, API server, admission webhook.
- **Execution Flow**: Message → Channel Pod → NATS → AgentRun Job → LLM call → Results.
- **CRDs**: SympoziumInstance, AgentRun, Policy, SkillPack, Schedule, PersonaPack.
- **Design Principles**: Kubernetes-native, declarative, scalable (HPA), safe (isolation, ephemeral RBAC).

## Use Cases
- **Cluster Administration**: Diagnose pod failures, scale deployments, triage alerts, remediate issues (e.g., "Why is a service crash-looping?").
- **Automation Workflows**: Scheduled security audits, resource optimization, incident response, cost analysis.
- **External Tasks**: Customer support agents, code reviews, data pipelines.
- **Agentic Ops**: Overnight alert reviews, manifest reviews, health checks in production clusters.

## Benefits
- **Safety & Isolation**: No shared state, blast-radius containment.
- **Scalability**: Horizontal scaling for high-volume ops.
- **Flexibility**: Any AI model, custom packs, GitOps integration.
- **Ease of Use**: Quick install via CLI, intuitive TUI/dashboard.

## Installation
1. Install CLI: `curl -fsSL https://deploy.sympozium.ai/install.sh | sh` (or Homebrew).
2. Deploy: `sympozium install` (CRDs, controller, NATS).
3. Activate: Use TUI to select PersonaPacks and configure.

## Comparison Table
| Tool          | Open Source | License     | GitHub Stars | Forks | Contributors | CNCF? | GitHub Repo Link | Notes on Activity/Maintenance |
|---------------|-------------|-------------|--------------|-------|--------------|-------|------------------|-------------------------------|
| **Sympozium** | Yes        | Apache 2.0 | 84          | 16   | 5           | No   | [github.com/AlexsJones/sympozium](https://github.com/AlexsJones/sympozium) | Extremely active (commits today, v0.0.65 release, UI/dashboard work) |
| **Kagent**    | Yes        | Apache 2.0 | ~2.3k       | ~416 | ~113        | Yes (contributed) | [github.com/kagent-dev/kagent](https://github.com/kagent-dev/kagent) | Mature, steady growth |
| **K8sGPT**    | Yes        | Apache 2.0 | ~7.5k       | ~950 | ~114        | No   | [github.com/k8sgpt-ai/k8sgpt](https://github.com/k8sgpt-ai/k8sgpt) | Very popular, established (frequent updates from core contributors) |
| **kubectl-ai**| Yes        | Apache 2.0 | ~7.3k       | ~680 | ~53         | No   | [github.com/GoogleCloudPlatform/kubectl-ai](https://github.com/GoogleCloudPlatform/kubectl-ai) | Strong adoption (Google-backed, active issues/PRs) |


**K8sGPT** and **Sympozium** are both open-source AI-powered tools for Kubernetes, created by the same developer (Alex Jones). K8sGPT focuses on diagnostics and troubleshooting, while Sympozium builds on similar ideas to create a full **agentic control plane** for running fleets of AI agents — including those that administer Kubernetes clusters.

### Key Differences

- **Core Purpose and Scope**  
  - **K8sGPT**: Primarily a diagnostic and triage tool. It scans your Kubernetes cluster (pods, events, deployments, etc.), identifies issues using codified SRE knowledge (analyzers), and uses LLMs to explain problems in plain English with remediation suggestions. It can run as a CLI (`k8sgpt analyze --explain`), in-cluster operator for continuous monitoring, or via MCP server for integration with AI assistants like Claude.  
  - **Sympozium**: A Kubernetes-native platform for orchestrating **multi-agent fleets** that can diagnose, scale, remediate, and perform arbitrary workflows. It treats agents as ephemeral Pods/Jobs, policies as CRDs, and supports proactive/scheduled execution. It can point agents inward (cluster ops) or outward (e.g., customer support, code review, data pipelines).

- **Execution Model**  
  - **K8sGPT**: Analyzer-based scanning + LLM explanation. No native agent runtime; remediation is suggested (some auto-remediation in operator mode with risk controls), but not executed via agents.  
  - **Sympozium**: Full agent lifecycle — messages → NATS → ephemeral AgentRun Job → LLM call + skill sidecars → results. Agents have persistent memory (ConfigMaps), isolated skill execution (kubectl, helm in sidecars with ephemeral RBAC), and garbage collection.

- **Agentic Capabilities**  
  - **K8sGPT**: Supports agent-like interaction via MCP (Model Context Protocol) for tools like Claude, but it's more "consultant" than autonomous actor. No multi-agent collaboration or scheduling built-in.  
  - **Sympozium**: True multi-agent orchestration, bidirectional channels (Slack, Telegram, Discord, WhatsApp), scheduled tasks (SympoziumSchedule CRD), PersonaPacks (pre-bundled agents like "SRE Watchdog" or "Security Guardian").

- **Security & Isolation**  
  - Both emphasize safety, but **Sympozium** goes further with per-run ephemeral RBAC, NetworkPolicy isolation, non-root containers, and sidecar-based tool execution.

- **Maturity & Community**  
  - **K8sGPT**: Mature (CNCF Sandbox project), ~7.5k GitHub stars, very popular for quick troubleshooting.  
  - **Sympozium**: Newer (early 2026 public release), ~84 stars, extremely active development (daily commits/releases), positioned as the "spiritual successor" to K8sGPT.

### Comparison Table

| Aspect                  | K8sGPT                                      | Sympozium                                           |
|-------------------------|---------------------------------------------|-----------------------------------------------------|
| Primary Focus           | Diagnostics, triage, explanations           | Agentic orchestration & execution                   |
| Execution               | Scan + explain (CLI / operator / MCP)       | Ephemeral Pods/Jobs per agent run                   |
| Agent Model             | Analyzer + LLM enrichment                   | Full agents with tools, memory, multi-agent         |
| Remediation             | Suggestions + limited auto (operator)       | Agents can execute (via skills like kubectl)        |
| Scheduling / Proactive  | Limited (operator monitoring)               | Built-in CRD-based scheduling                       |
| Integrations            | Many LLM backends, Prometheus, etc.         | Messaging channels + any OpenAI-compatible LLM      |
| Use Case Fit            | "What’s wrong? Why? How to fix?"            | "Fix it autonomously", scheduled ops, workflows     |
| GitHub Stars (Feb 2026) | ~7.5k                                       | ~84                                                 |
| CNCF Status             | Sandbox project                             | No (yet)                                            |

### Which One Is Better?

- **Choose K8sGPT if** you want a lightweight, battle-tested tool for fast troubleshooting and explanations. It's excellent for:  
  - On-call engineers needing quick insights  
  - Beginners learning Kubernetes issues  
  - Integrating diagnostics into existing workflows (CLI, operator, AI assistants)  
  - Production stability (mature, widely adopted)

- **Choose Sympozium if** you want proactive, autonomous, or multi-agent Kubernetes administration. It's better for:  
  - Automating remediation, scaling, audits, or sweeps  
  - Running scheduled agents (e.g., nightly health checks)  
  - Building custom agent fleets with persistent memory and channels  
  - Future-proofing with full agentic orchestration in a Kubernetes-native way

In short: **K8sGPT** is the established "AI doctor" for your cluster — great at telling you what's wrong. **Sympozium** is the evolving "AI SRE team" living inside your cluster — capable of actually doing the work. Many users will benefit from both: use K8sGPT for rapid diagnosis today, and Sympozium for agent-driven automation as it matures.