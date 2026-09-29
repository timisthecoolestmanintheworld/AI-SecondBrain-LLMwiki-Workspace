---
title: "How to Build a Semantic Memory System for AI Agents Without Hermes Agent"
source: "https://www.mindstudio.ai/blog/build-semantic-memory-system-ai-agents-without-hermes"
author:
  - "[[MindStudio Team]]"
published: 2026-07-11
created: 2026-07-14
description: "Hermes Agent proved memory matters, but you can build better recall inside Claude Code. Learn storage, injection, and semantic search using local vector DBs."
tags:
  - "clippings"
---
## Why AI Agents Keep Forgetting (And How to Fix It)

Memory is the difference between an AI agent that’s genuinely useful and one you have to re-explain everything to every single session. If you’ve spent any time building agents, you’ve hit this wall. The model reasons well. The tool calls work. But the moment context resets, it’s back to square one.

This is exactly what made the Hermes Agent experiment interesting. It showed — clearly, repeatedly — that when you give an AI agent a structured semantic memory system, its performance on complex, multi-step tasks improves substantially. Agents stopped repeating themselves. They built on prior reasoning. They started feeling less like stateless APIs and more like persistent collaborators.

The good news: you don’t need Hermes Agent to get that. You can build a **semantic memory system for AI agents** from scratch using local vector databases, embedding pipelines, and smart injection logic. This guide walks through exactly how to do that inside environments like Claude Code or any custom agent framework.

---

## What Hermes Agent Actually Demonstrated

Hermes Agent — built on top of Ollama and local models — gained attention for its emphasis on persistent, context-aware memory. The core insight wasn’t revolutionary in theory, but it was compelling in practice: agents that could recall relevant past interactions performed better on reasoning tasks than those operating from scratch.

What it specifically demonstrated:

- **Retrieval-augmented context** matters more than raw model size in long-horizon tasks
- Storing memories as vector embeddings, rather than raw text logs, allows for *semantic* retrieval — not just keyword matching
- Agents with memory made fewer contradictory decisions across sessions
- The retrieval step itself could be lightweight enough to run locally without meaningful latency
![Learn Hermes. Free. 1 hour.](https://i.mscdn.ai/1b7301c0-de42-4e46-b110-e9c55396e7ca/generated-images/fb67e638-9ac3-4c24-9136-cb4191563d07.png?fm=auto&w=1200)

The limitation of Hermes Agent was mostly about portability and flexibility. It worked within its own ecosystem. If you’re building on Claude Code, LangChain, CrewAI, or a custom Python agent, you need the same capability without the lock-in.

---

## The Anatomy of a Semantic Memory System

Before writing any code, it’s worth understanding the three functional layers of a semantic memory system.

### Layer 1: Storage

Where memories live. In a semantic system, this is a vector database — a store that holds numerical representations of text (embeddings) alongside the original content and metadata.

### Layer 2: The Embedding Pipeline

The process of converting text (agent observations, user inputs, decisions, outcomes) into vector embeddings. This is what enables semantic search rather than keyword matching. Two sentences that mean the same thing but use different words will have similar vectors.

### Layer 3: Retrieval and Injection

When the agent needs to act, it queries the memory store using the current context as a search key. The most semantically relevant memories are retrieved and injected into the agent’s prompt or context window.

These three layers are independent. You can swap out the vector DB, change embedding models, or redesign the injection logic without touching the others. That modularity is intentional — your memory system should be infrastructure, not a bottleneck.

---

## Choosing a Local Vector Database

Running memory locally matters for several reasons: latency, privacy, cost, and control. Here are the main options worth considering.

### ChromaDB

[ChromaDB](https://www.trychroma.com/) is probably the most accessible starting point. It runs in-process (no separate server needed for small deployments), has a clean Python API, and integrates natively with LangChain and LlamaIndex.

**Good for:** prototyping, local development, small to medium agent deployments  
**Limitations:** not ideal for high-concurrency production workloads

```python
import chromadb

client = chromadb.Client()
collection = client.create_collection("agent_memory")

collection.add(
    documents=["User prefers concise responses", "Project deadline is Friday"],
    ids=["mem_001", "mem_002"]
)

results = collection.query(
    query_texts=["What are the user's preferences?"],
    n_results=3
)
```

### Qdrant

Qdrant is a purpose-built vector search engine with a Rust core, which makes it fast. It supports filtering, named vectors, and payload indexing. You can run it locally via Docker with a single command.

**Good for:** production-grade local deployments, agents that need filtered retrieval  
**Limitations:** requires Docker; slightly more setup than Chroma

### FAISS

Facebook AI Similarity Search (FAISS) is a library rather than a database. It’s extremely fast for pure similarity search but doesn’t handle persistence, metadata, or CRUD operations natively. You’d wrap it yourself or use it through a higher-level library.

**Good for:** high-performance similarity search when you’re managing storage separately  
**Limitations:** no built-in persistence; you handle serialization

### LanceDB

A newer entrant, LanceDB stores vectors in a columnar format on disk. It’s serverless by design and has good performance for agents that need to scan large memory stores.

**For most builders starting out, ChromaDB gets you running in under 10 minutes. Move to Qdrant when you need more control.**

---

## Building Your Embedding Pipeline

The embedding pipeline converts raw text into vectors. The model you use determines how well your semantic search performs.

### Choosing an Embedding Model

For local use, these are the practical options:

- **`nomic-embed-text`** via Ollama — solid general-purpose embeddings, runs locally, 768 dimensions
- **`mxbai-embed-large`** via Ollama — higher quality, 1024 dimensions, slightly slower
- **`text-embedding-3-small`** via OpenAI API — excellent quality if you’re okay with API calls, cost is minimal
- **`sentence-transformers/all-MiniLM-L6-v2`** via HuggingFace — fast, lightweight, works entirely offline

### Everyone else built a construction worker.We built the contractor.

🦺

CODING AGENT

Types the code you tell it to.  
One file at a time.

🧠

CONTRACTOR · REMY

Runs the entire build.  
UI, API, database, deploy.

For a Claude Code environment where you want full local operation:

```python
import ollama

def embed_text(text: str) -> list[float]:
    response = ollama.embeddings(
        model="nomic-embed-text",
        prompt=text
    )
    return response["embedding"]
```

### What to Embed

This is a design decision that significantly affects memory quality. Don’t just dump raw conversation logs.

**Embed these:**

- Summarized observations (“User confirmed the report format should be CSV, not JSON”)
- Agent decisions with context (“Chose to use the search tool because the query required current data”)
- Task outcomes (“Completed email draft — user approved with minor edits”)
- User preferences revealed during interaction
- Errors and how they were resolved

**Avoid embedding:**

- Raw, unprocessed transcripts (too noisy, retrieval quality degrades)
- Ephemeral tool outputs that aren’t meaningful long-term
- Duplicate or near-duplicate entries (use deduplication logic)

### Memory Extraction Step

Before storing, have the agent (or a lightweight summarizer) extract the memory-worthy content from a conversation turn:

```python
def extract_memory(conversation_turn: str, llm) -> str:
    prompt = f"""Extract the key factual information, preferences, or decisions from this interaction that would be useful to remember in future sessions. Be concise — one to three sentences maximum.

Interaction: {conversation_turn}

Memory:"""
    return llm.complete(prompt)
```

This step dramatically improves retrieval quality because you’re storing clean, dense signal rather than raw conversation noise.

---

## Implementing Semantic Search

Once you have stored memories, retrieval needs to be fast and relevant.

### Basic Retrieval Pattern

```python
def retrieve_relevant_memories(
    query: str,
    collection,
    n_results: int = 5,
    min_relevance_threshold: float = 0.7
) -> list[str]:
    
    query_embedding = embed_text(query)
    
    results = collection.query(
        query_embeddings=[query_embedding],
        n_results=n_results,
        include=["documents", "distances"]
    )
    
    # Filter by relevance threshold
    memories = []
    for doc, distance in zip(results["documents"][0], results["distances"][0]):
        # ChromaDB returns L2 distance; lower is more similar
        similarity = 1 - distance
        if similarity >= min_relevance_threshold:
            memories.append(doc)
    
    return memories
```

### Hybrid Search for Better Recall

Pure semantic search sometimes misses exact matches. A hybrid approach combines vector similarity with keyword filtering:

1. Run semantic search to get top-N candidates
2. Apply BM25 or simple keyword scoring as a re-ranking step
3. Return the re-ranked top results

For most agent use cases, pure semantic search with a reasonable threshold (0.65–0.75) is sufficient. Add hybrid search when your agents work with lots of proper nouns, codes, or identifiers that semantic models don’t handle well.

### Temporal Decay

Not all memories are equally current. A preference the user stated six months ago may have changed. Add a recency factor to your scoring:

```python
import math
from datetime import datetime

def score_with_recency(similarity: float, timestamp: datetime, decay_rate: float = 0.01) -> float:
    days_old = (datetime.now() - timestamp).days
    recency_score = math.exp(-decay_rate * days_old)
    return similarity * 0.7 + recency_score * 0.3
```

Tune the weights based on your use case. A coding assistant should weight recency lightly (older patterns are still valid). A customer support agent should weight it heavily (account status changes frequently).

---

## Memory Injection Strategies

Retrieved memories are only useful if you inject them into the agent’s context at the right time, in the right format.

### System Prompt Injection

The simplest approach: prepend retrieved memories to the system prompt before each agent turn.

```python
def build_system_prompt(base_prompt: str, relevant_memories: list[str]) -> str:
    if not relevant_memories:
        return base_prompt
    
    memory_block = "\n".join([f"- {mem}" for mem in relevant_memories])
    
    return f"""{base_prompt}

## Relevant Memory
The following information from previous interactions is relevant to this task:
{memory_block}

Use this context to inform your responses, but don't reference it explicitly unless asked."""
```

### Structured Memory Context

For agents with longer tasks, a more structured format helps the model parse and use memories correctly:

```plaintext
## Long-Term Memory (from previous sessions)
[User Preferences]
- Prefers bullet points over paragraphs in summaries
- Works in EST timezone, availability 9am–5pm

[Project Context]
- Current project: Q3 financial report automation
- Last completed: data ingestion pipeline (completed 2024-11-15)
- Next milestone: visualization layer

[Known Issues]
- API rate limits hit when batch size > 100 records
```

### Episodic vs. Semantic Memory

Borrowing from cognitive science, it helps to separate two memory types:

- **Episodic memory**: Specific events (“On Tuesday, the user rejected the CSV format proposal”)
- **Semantic memory**: General knowledge the agent has built up (“This user prefers JSON output formats”)

Store them in separate collections with different retrieval weights. Episodic memories are useful for continuity; semantic memories are useful for preference and behavioral adaptation.

### Avoiding Context Window Bloat

Memory injection can eat your context window fast. Keep these constraints in mind:

- Set a hard cap on injected memories (5–8 is usually enough)
- Compress older memories with periodic summarization runs
- Use importance scoring to prioritize high-signal memories over low-signal ones
- Consider a two-tier system: hot memory (recent, in-context) and cold memory (older, retrieved on demand)

---

## Managing Memory Over Time

A memory system that only grows will eventually degrade in quality and performance.

### Deduplication

Before storing a new memory, check if a semantically similar one already exists:

```python
def should_store_memory(new_memory: str, collection, threshold: float = 0.92) -> bool:
    results = collection.query(
        query_embeddings=[embed_text(new_memory)],
        n_results=1
    )
    
    if not results["distances"][0]:
        return True
    
    similarity = 1 - results["distances"][0][0]
    return similarity < threshold
```

### Periodic Consolidation

Run a consolidation job (daily or weekly) that:

1. Clusters similar memories together
2. Generates a summary of each cluster
3. Replaces the cluster with the summary
4. Removes memories below an importance threshold

This is the rough equivalent of how sleep consolidates human memory — you’re compressing episodes into denser, more useful representations.

### Memory Importance Scoring

Not all memories are worth keeping. Add an importance score when storing:

- High: User stated explicit preference, agent made a significant decision, error with resolution
- Medium: Useful context, task status
- Low: Routine confirmations, obvious inferences

Drop low-importance memories after 30 days unless they’ve been accessed recently.

---

## How MindStudio Fits Into This Picture

Building and maintaining all of this infrastructure — the vector DB, the embedding pipeline, the injection logic, the consolidation jobs — is real work. It’s manageable, but it adds up fast across a multi-agent system.

This is where MindStudio’s approach to [multi-agent workflows](https://app.mindstudio.ai/) makes a practical difference. Rather than wiring memory infrastructure together yourself for every agent, MindStudio lets you build agents with persistent data access baked into the workflow — using Airtable, Notion, Google Sheets, or custom datastores as structured memory layers, connected through its 1,000+ integrations.

## Plans first. Then code.

PROJECTYOUR APP

SCREENS12

DB TABLES6

BUILT BYREMY

1280 px · TYP.

yourapp.msagent.ai

A · UI · FRONT END

Remy writes the spec, manages the build, and ships the app.

For teams building more sophisticated setups, the [Agent Skills Plugin](https://www.mindstudio.ai/blog/introducing-agent-skills) (`@mindstudio-ai/agent`) lets Claude Code agents and other custom agents call MindStudio’s capabilities as simple method calls. You get managed infrastructure for things like `agent.runWorkflow()` without building the orchestration yourself. That means your agent can offload memory consolidation, summarization, or retrieval-augmented lookup to a MindStudio workflow — while your core agent focuses on reasoning.

If you’re earlier in the build process and want to prototype memory-enabled agents without setting up vector DBs locally, [MindStudio’s no-code builder](https://app.mindstudio.ai/) lets you do that in under an hour using its visual workflow tools and built-in data connectors.

You can try it free at [mindstudio.ai](https://www.mindstudio.ai/).

---

## Common Mistakes to Avoid

### Storing Too Much, Too Literally

The most common mistake is treating memory as a log. You don’t want a transcript — you want distilled signal. Always run a summarization/extraction step before storing.

### Ignoring Retrieval Quality

Building storage is the easy part. Retrieval quality determines whether the system actually helps. Test your semantic search with real agent queries. Tune your similarity thresholds. Add hybrid search if pure semantic search underperforms.

### Single Collection for Everything

Separate your memory types. User preferences, project context, error history, and episodic events should live in different collections with different retrieval strategies.

### No Memory Validation

Agents can store incorrect memories. Add a confidence layer: if the memory was derived from an uncertain inference rather than an explicit statement, tag it accordingly and weight it lower during retrieval.

### Forgetting Write Performance

For agents running at high frequency, write performance matters. ChromaDB in-process mode is fine for low-throughput agents. For anything that writes memories at high frequency, benchmark your setup or move to Qdrant with a persistent server.

---

## Frequently Asked Questions

### What is a semantic memory system for AI agents?

A semantic memory system stores agent experiences, observations, and context as vector embeddings and retrieves them using semantic similarity search. Unlike keyword search, it finds relevant memories based on meaning — so a query about “user formatting preferences” will surface memories about layout choices even if those exact words weren’t used.

### How is this different from just using a long context window?

Long context windows include everything — relevant or not. A semantic memory system selectively retrieves only the most relevant information for a given query. This means less noise, lower token costs, and the ability to retain knowledge across sessions without hitting context limits.

### Which vector database should I use for a local agent?

For most builders, ChromaDB is the fastest starting point — it runs in-process with no separate server and has a clean Python API. If you need production-grade performance, filtering capabilities, or are deploying at scale, Qdrant running locally via Docker is the better choice.

### How do I prevent my agent from storing bad memories?

Use an extraction step that filters raw interactions down to high-confidence, factual statements before storing. Add a deduplication check to avoid redundant entries. Tag uncertain inferences separately from explicit statements, and weight them lower during retrieval.

### Can I build a semantic memory system without using OpenAI’s embedding API?

Yes. Ollama supports several strong local embedding models like `nomic-embed-text` and `mxbai-embed-large` that run entirely on your machine. The HuggingFace `sentence-transformers` library also provides high-quality embeddings with no API calls required.

### How many memories should I inject into each agent prompt?

![Wondering what the Hermes hype is about? Free 60-minute primer](https://i.mscdn.ai/1b7301c0-de42-4e46-b110-e9c55396e7ca/generated-images/c8d61682-41d9-44c0-a2fe-5299b2d46f88.png?fm=auto&w=1200)

Typically 3–8 is the right range. More than that and you’re adding noise that can confuse the model and bloat your context window. Use similarity thresholds to ensure only genuinely relevant memories are included rather than injecting a fixed number regardless of relevance.

---

## Key Takeaways

- Semantic memory systems have three layers: storage (vector DB), an embedding pipeline, and retrieval/injection logic — each independently replaceable.
- ChromaDB is the fastest local starting point; Qdrant is better for production workloads.
- Always summarize and extract signal before storing — never log raw conversations.
- Inject 3–8 relevant memories per agent turn using similarity thresholds, not fixed counts.
- Separate episodic memories (events) from semantic memories (preferences and patterns) for better retrieval quality.
- Add temporal decay, deduplication, and periodic consolidation to keep memory quality high over time.

Hermes Agent showed that memory changes what agents can do. Building that capability yourself, with tools you control, puts you in a much better position than depending on a single framework. The infrastructure isn’t complicated — but the design decisions matter.

If you want to skip the infrastructure setup and start with a working agent that has persistent memory and data access, [MindStudio](https://www.mindstudio.ai/) is worth exploring. The average build takes under an hour, and you can connect it to the same datastores your agents already use.