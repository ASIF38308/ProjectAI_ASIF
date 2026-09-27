# AsifAI

**A local-first personal AI assistant designed to run on modest hardware.**

AsifAI explores how much useful intelligence can be created by combining a relatively small local language model with **memory, retrieval, tools, and orchestration** rather than relying only on model size.

> Built by Mohd Asif
> Status: Architecture & Planning

---

## Why I Built AsifAI

I started building AsifAI because I wanted to understand what it would take to build a personal AI system that actually belongs to the person using it.

Modern AI assistants are powerful, but much of their intelligence depends on cloud infrastructure, external services, and models that users do not control. I wanted to explore a different approach:

**What can I build locally, on the hardware I already have, if I combine a smaller language model with memory, retrieval, tools, and good system design?**

My goal is not to build a model that competes with the largest AI systems. It is to understand the engineering behind a useful personal AI assistant — how it remembers context, works with personal knowledge, uses tools, handles failures, adapts to limited hardware, and becomes more useful over time.

**AsifAI is my experiment in building AI as a system, not just calling an AI model.**

---

## The Problem

Current AI assistants can be extremely capable, but several challenges remain:

* Dependence on cloud infrastructure
* Personal information being processed by external services
* Limited control over how memory is stored and used
* Model capabilities being treated as the primary source of intelligence
* Difficulty running capable AI systems on modest hardware
* Limited transparency into why an assistant retrieved information or performed an action

AsifAI explores whether some of these challenges can be addressed through **local execution, modular architecture, persistent memory, retrieval, tools, and orchestration.**

---

## The Approach

Instead of expecting one large model to handle everything, AsifAI treats the AI assistant as a system made of multiple components:

```text
             ┌──────────────────┐
             │      User        │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │  User Interface  │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │   Orchestrator   │
             └────────┬─────────┘
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
    ┌───────┐     ┌────────┐     ┌────────┐
    │  LLM  │     │ Memory │     │  RAG   │
    └───────┘     └────────┘     └────────┘
       │              │              │
       └──────────────┼──────────────┘
                      │
                      ▼
               ┌────────────┐
               │   Tools    │
               └────────────┘
```

The central idea is:

**Model + Memory + Retrieval + Tools + Orchestration = System Intelligence**

---

## Core Capabilities

| Capability               | Description                                                     | Status     |
| ------------------------ | --------------------------------------------------------------- | ---------- |
| Local LLM                | Run language models locally                                     | 🔄 Planned |
| Conversational Interface | Interact with the assistant                                     | 🔄 Planned |
| Long-Term Memory         | Store and retrieve useful context                               | 🔄 Planned |
| Document Intelligence    | Search and reason over local documents                          | 🔄 Planned |
| RAG                      | Ground responses using retrieved information                    | 🔄 Planned |
| Tool Calling             | Allow the assistant to perform actions                          | 🔄 Planned |
| Model Routing            | Select models based on task and hardware                        | 💡 Planned |
| Agent Workflows          | Coordinate multi-step tasks                                     | 💡 Planned |
| Voice Interface          | Speech input and output                                         | 💡 Planned |
| Observability            | Monitor reasoning-related system activity, latency and failures | 💡 Planned |

---

# Design Principles

## 1. Local First

AsifAI should work locally whenever practical.

Personal conversations, memories, and documents should not need to leave the user's machine for core functionality.

Internet access may be introduced for tasks that explicitly require external information.

---

## 2. Model Agnostic

AsifAI should not depend on one specific LLM.

Different models may be selected based on:

* Hardware
* Task complexity
* Context requirements
* Speed
* Quality
* Resource availability

The model should be replaceable without rebuilding the entire application.

---

## 3. System Intelligence

A language model does not need to perform every task itself.

AsifAI aims to extend a model using:

```text
Memory
+
Retrieval
+
Tools
+
Context
+
Orchestration
```

The goal is to make the overall system more capable than the model operating in isolation.

---

## 4. Hardware Adaptive

The system should degrade gracefully on weaker hardware instead of requiring a high-end GPU.

The project will investigate:

* Smaller models
* Quantization
* Context management
* Model routing
* Resource-aware configuration
* CPU/GPU utilization

---

## 5. Observable

AI systems can fail in ways that are difficult to understand.

AsifAI should eventually make important system activity observable, including:

* Model used
* Response latency
* Retrieved memories
* Retrieved documents
* Tool calls
* Tool failures
* Resource usage
* Workflow state

This is intended to make the system easier to debug, evaluate, and improve.

---

# High-Level Architecture

```text
                         ┌──────────────────┐
                         │      User        │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │   User Interface │
                         │ Streamlit / Web  │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │   API / Backend  │
                         │     FastAPI      │
                         └────────┬─────────┘
                                  │
                                  ▼
                       ┌─────────────────────┐
                       │    Orchestrator     │
                       │                     │
                       │ Context Management  │
                       │ Model Routing       │
                       │ Tool Selection      │
                       │ Workflow Control    │
                       └───────┬─────────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌────────────┐   ┌────────────┐   ┌────────────┐
       │    LLM     │   │   Memory   │   │    RAG     │
       │  Ollama    │   │   SQLite   │   │  ChromaDB  │
       └────────────┘   └────────────┘   └────────────┘
              │                │                │
              └────────────────┼────────────────┘
                               │
                               ▼
                       ┌─────────────────┐
                       │      Tools      │
                       │ Files / Python  │
                       │ Web / APIs      │
                       └─────────────────┘
```

---

# Tech Stack

| Layer             | Technology                  | Purpose                     |
| ----------------- | --------------------------- | --------------------------- |
| Language          | Python                      | Core development            |
| API               | FastAPI                     | Backend/API layer           |
| Initial UI        | Streamlit                   | Rapid prototyping           |
| Future UI         | React                       | Production interface        |
| LLM Runtime       | Ollama                      | Local model execution       |
| Models            | Qwen / Phi / Gemma / others | Language generation         |
| Structured Memory | SQLite                      | Persistent application data |
| Vector Store      | ChromaDB                    | Semantic retrieval          |
| Orchestration     | LangGraph                   | Stateful workflows          |
| Version Control   | Git                         | Source control              |

> Technologies may change as the architecture evolves. Components should remain modular wherever practical.

---

# Target Hardware

The first development target is a **MacBook Air 2015 with 8 GB RAM**.

The system should also be tested on stronger hardware where available.

| Hardware Class | Example          | Goal                       |
| -------------- | ---------------- | -------------------------- |
| Low End        | MacBook Air 2015 | Core functionality         |
| Mid Range      | M1 MacBook Air   | Faster local inference     |
| GPU Laptop     | RTX 4060 Laptop  | Larger/faster models       |
| Workstation    | RTX 4090         | High-performance workloads |

Hardware compatibility does not mean every model will perform equally well on every device.

The project will focus on **adaptive model selection and resource-aware configuration**.

---

# Initial Model Strategy

Initial models under consideration:

| Model Family | Approx. Size | Intended Use                            |
| ------------ | -----------: | --------------------------------------- |
| TinyLlama    |         1.1B | Lightweight experiments                 |
| Gemma        |           2B | Lightweight assistant tasks             |
| Qwen         |           3B | General-purpose local assistant         |
| Phi          |         3–4B | General-purpose / reasoning experiments |
| DeepSeek     |           7B | Higher-quality workloads                |

Actual performance will depend on:

* Quantization
* Context length
* CPU/GPU
* Available RAM/VRAM
* Prompt size
* Runtime configuration

Performance numbers will be benchmarked on actual hardware rather than assumed from model size alone.

---

# Development Roadmap

## Phase 0 — Foundation

**Goal:** Establish the smallest working local AI system.

### Build

* Project structure
* Ollama integration
* Local model execution
* FastAPI backend
* Basic chat interface
* Configuration management
* Logging

### Target

```text
User
 ↓
UI
 ↓
API
 ↓
Ollama
 ↓
Local LLM
 ↓
Response
```

### Success Criteria

* Local model responds successfully
* Chat history works within a session
* API and UI communicate correctly
* System runs on the target MacBook

---

## Phase 1 — Persistent Memory

**Goal:** Give AsifAI persistent context beyond a single conversation.

### Build

* Conversation storage
* Memory extraction
* Memory storage
* Memory retrieval
* Relevance filtering
* SQLite persistence

### Target Architecture

```text
Conversation
     ↓
Memory Extraction
     ↓
Memory Store
     ↓
Relevant Memory Retrieval
     ↓
LLM Context
```

The system should distinguish between:

* Current conversation context
* Short-term memory
* Long-term memory
* User-provided knowledge

---

## Phase 2 — Document Intelligence / RAG

**Goal:** Allow AsifAI to work with local documents and knowledge.

### Build

* Document ingestion
* Text extraction
* Chunking
* Embeddings
* Vector storage
* Semantic retrieval
* Context injection
* Source attribution
* Retrieval evaluation

### Target Flow

```text
Document
   ↓
Parse
   ↓
Chunk
   ↓
Embed
   ↓
Vector Store
   ↓
Retrieve
   ↓
LLM
   ↓
Grounded Response
```

---

## Phase 3 — Tool Usage

**Goal:** Allow the assistant to perform useful actions instead of only generating text.

Potential tools include:

* File operations
* Python execution
* Local database queries
* Calculator
* System information
* Web search
* External APIs

Tool execution should be:

* Explicit
* Permission-controlled
* Logged
* Validated where appropriate
* Recoverable when possible

---

## Phase 4 — Orchestration

**Goal:** Move from simple chat toward task-oriented workflows.

Example:

```text
User Request
     ↓
Task Classification
     ↓
Planning
     ↓
Memory / RAG / Tool Selection
     ↓
Execution
     ↓
Verification
     ↓
Final Response
```

LangGraph may be used where stateful workflows provide meaningful value.

The goal is not to create multiple agents simply for the sake of having multiple agents.

---

## Phase 5 — Voice Interface

Potential capabilities:

* Speech-to-text
* Voice activity detection
* Text-to-speech
* Streaming responses
* Wake-word experiments

Voice will remain an interface layer rather than being tightly coupled to the core AI architecture.

---

# Phase 6 — Long-Term Vision

## Personal AI System

The long-term direction is to explore whether a local AI assistant can become a broader **personal computing layer** capable of:

* Understanding user context
* Managing personal knowledge
* Working with files
* Executing workflows
* Connecting to external services
* Maintaining persistent memory
* Selecting appropriate models
* Selecting appropriate tools
* Verifying task results

This is a **long-term research direction**, not a promise that every capability will be implemented.

---

# Evaluation

AsifAI should not be evaluated only by whether it produces convincing text.

The system should eventually be measured using practical engineering metrics.

| Area        | Example Metric                              |
| ----------- | ------------------------------------------- |
| Latency     | Time to first token / total response time   |
| Memory      | Retrieval relevance                         |
| RAG         | Retrieval accuracy / grounded response rate |
| Tools       | Successful tool execution rate              |
| Reliability | Failure and recovery rate                   |
| Resources   | RAM / CPU / GPU usage                       |
| Models      | Quality vs. latency trade-off               |
| Privacy     | Data leaving the local environment          |
| Usability   | Task completion rate                        |

The evaluation framework will evolve as the system develops.

---

# Project Structure

```text
AsifAI/
│
├── app/
│   ├── api/
│   ├── core/
│   ├── memory/
│   ├── rag/
│   ├── models/
│   ├── tools/
│   └── orchestration/
│
├── ui/
│
├── tests/
│
├── scripts/
│
├── data/
│
├── docs/
│   ├── vision.md
│   ├── architecture.md
│   ├── roadmap.md
│   ├── hardware-guide.md
│   ├── model-strategy.md
│   ├── performance-tuning.md
│   ├── troubleshooting.md
│   └── model-registry.md
│
├── .env.example
├── requirements.txt
├── README.md
└── LICENSE
```

---

# Documentation

* [Vision](docs/vision.md)
* [Architecture](docs/architecture.md)
* [Roadmap](docs/roadmap.md)
* [Hardware Guide](docs/hardware-guide.md)
* [Model Strategy](docs/model-strategy.md)
* [Performance Tuning](docs/performance-tuning.md)
* [Troubleshooting](docs/troubleshooting.md)
* [Model Registry](docs/model-registry.md)

---

# Current Status

🟡 **Planning & Architecture**

### Currently working on

* Defining system architecture
* Evaluating local model options
* Designing memory architecture
* Defining component interfaces
* Establishing evaluation criteria
* Planning the first working prototype

### Current milestone

> **Local Model → API → Chat UI**

No production code has been implemented yet.

Everything beyond the first milestone will be built incrementally and evaluated before expanding the system.

---

# Project Philosophy

> **Don't make the model do everything. Build a system around the model.**

AsifAI is an experiment in combining:

**Local Models**

* **Memory**
* **Retrieval**
* **Tools**
* **Orchestration**
* **Evaluation**

to explore how a useful personal AI system can be built within the constraints of modest hardware.

The objective is not simply to build a chatbot.

**The objective is to understand and build the system behind a capable personal AI.**

---

# License

MIT License
