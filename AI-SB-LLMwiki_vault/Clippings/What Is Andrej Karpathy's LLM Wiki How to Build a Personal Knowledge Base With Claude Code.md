---
title: "What Is Andrej Karpathy's LLM Wiki? How to Build a Personal Knowledge Base With Claude Code"
source: "https://www.mindstudio.ai/blog/andrej-karpathy-llm-wiki-knowledge-base-claude-code"
author:
  - "[[MindStudio Team]]"
published: 2026-04-05
created: 2026-07-13
description: "Karpathy's LLM wiki turns raw documents into a structured markdown knowledge base Claude can query. Here's how to set it up in 5 minutes with Obsidian."
tags:
  - "clippings"
---
## The Idea Behind Karpathy’s LLM Wiki

Andrej Karpathy — co-founder of OpenAI, former Tesla AI director, and one of the clearest explainers of machine learning concepts working today — has talked publicly about a deceptively simple idea: your personal notes and documents, organized in plain markdown, can become a knowledge base that an LLM can actually reason over.

He calls it an LLM wiki. The concept is straightforward. Instead of scattering knowledge across Notion, Google Docs, browser bookmarks, and sticky notes, you keep everything as structured markdown files. Then you point Claude Code (or any capable coding agent) at that folder and ask it questions. The LLM reads your files, finds what’s relevant, and gives you grounded answers drawn from your own knowledge — not the general internet.

This isn’t a product. It’s a workflow pattern. And it’s one of the most practical applications of Claude Code that most people haven’t tried yet.

This guide explains how Karpathy’s LLM wiki works, why markdown is the right format for it, and how to get a working version running with Obsidian in about five minutes.

*Last updated: 2026-05-11 — added related Claude Code workflow links and second-brain comparisons.*

---

## What Makes This Different From a Normal Notes App

Most note-taking apps are built for human reading. You browse, search, click. They’re optimized for you to find things manually.

An LLM wiki is optimized for the model to read on your behalf. That shift changes everything about how you structure information.

## Remy is new. The platform isn't.

Remy

Product Manager Agent

THE PLATFORM

200+ models 1,000+ integrations Managed DB Auth Payments Deploy

▮

BUILT BY MINDSTUDIO

Shipping agent infrastructure since 2021

Remy is the latest expression of years of platform work. Not a hastily wrapped LLM.

Here’s the core distinction:

- **Traditional notes app**: You remember where something is and navigate to it
- **LLM wiki**: You describe what you need in plain language, and Claude finds and synthesizes it across your entire knowledge base

The model doesn’t care about your folder hierarchy or tags. It reads text. So plain markdown — which is just text with minimal syntax — is the ideal format. No proprietary encoding, no locked databases, no export friction.

Claude Code specifically is well-suited to this because it can read files directly from your local filesystem. You don’t need to paste content into a chat window. You just tell it where your notes live and ask your question.

---

## Why Markdown Is the Right Foundation

Before getting into setup, it’s worth understanding why Karpathy’s approach centers on markdown rather than any other format.

### Markdown Is Portable and Future-Proof

A `.md` file is a text file. It opens in any editor, on any operating system, forever. You’re not dependent on a company staying in business or an app maintaining backward compatibility.

### LLMs Read Markdown Natively

Models like Claude are trained on enormous amounts of markdown content — GitHub READMEs, documentation sites, forums. The syntax is part of their understanding. Headers, bullet points, code blocks, bold text — Claude interprets all of it as structure, not noise.

### It Forces Clarity

Writing in markdown discourages the kind of half-finished, poorly organized notes that accumulate in most people’s knowledge systems. Headers require you to name sections. Lists require you to separate items. The format nudges you toward clarity.

### Plain Text Means No Lock-In

You can sync it with git, open it in VS Code, view it in Obsidian, push it to a private GitHub repo, or read it in a terminal. The knowledge is yours in the most literal sense.

---

## How Karpathy’s LLM Wiki Actually Works

The architecture is minimal. There are three components:

**1\. A folder of markdown files** This is your knowledge base. It can contain anything: research notes, meeting summaries, project documentation, book notes, personal reference material, code snippets with explanations.

**2\. A consistent structure within each file** Good LLM wikis use a consistent internal format — a title, a brief summary, tagged topics, and then the content. The model uses this structure to locate relevant information faster.

**3\. Claude Code as the query interface** You open a terminal, navigate to your wiki folder, launch Claude Code, and ask it a question. Claude reads the files it needs, synthesizes an answer, and can even update or add notes when you ask it to.

That’s it. No database. No vector embeddings (though you can add them later). No server. Just files and a capable model.

### The Role of Claude Code

Claude Code is Anthropic’s terminal-based coding agent. Unlike Claude in a browser, Claude Code runs in your local environment and has direct access to your filesystem. It can:

- Read specific files or entire directories
- Search across files for relevant content
- Create new files or update existing ones
- Execute shell commands to search, filter, or organize your notes
![Catch up on Hermes — free 60-minute live workshop](https://i.mscdn.ai/1b7301c0-de42-4e46-b110-e9c55396e7ca/generated-images/2f72d608-9e6a-4ec2-b2f1-5063df20ef36.png?fm=auto&w=1200)

This makes it genuinely useful as a knowledge base interface. You’re not copy-pasting chunks of text into a chat window — the model is working directly with your files. If you want to extend the interaction patterns further, [the Superpowers plugin for Claude Code](https://www.mindstudio.ai/blog/what-is-superpowers-plugin-claude-code) packages reusable skills — including note triage and summarization patterns — that map naturally onto a wiki workflow.

---

## Set Up Your LLM Wiki in Obsidian (Step-by-Step)

Obsidian is the recommended front-end for this workflow. It’s a local-first markdown editor with a strong plugin ecosystem and a clean interface. Your files stay on your disk — Obsidian is just how you read and write them.

### Step 1: Install Obsidian and Create a Vault

Download Obsidian from [the official Obsidian site](https://obsidian.md/). Create a new vault in a folder you’ll remember — something like `~/wiki` or `~/Documents/llm-wiki`.

A “vault” in Obsidian is just a folder. Everything in it is plain markdown.

### Step 2: Define a Note Template

Consistency is what makes your wiki queryable. Create a template file at `_templates/note.md`:

```markdown
# undefined

**Summary**: One sentence describing this note.
**Tags**: #topic1 #topic2
**Created**: 2026-04-06T00:00:00+00:00
**Last Updated**: 2026-04-06T00:00:00+00:00

---

## Content

Write the main content here.

## Related Notes

- [[Note Title]]
```

You don’t need to follow this exactly. The key is that every note has a summary line and tags. These give Claude quick signals about relevance without reading the full file.

### Step 3: Organize Into Broad Topic Folders

Don’t over-engineer this. Start with four or five top-level folders:

```plaintext
wiki/
├── _templates/
├── projects/
├── research/
├── reference/
├── meetings/
└── inbox/
```

The `inbox/` folder is for rough notes that haven’t been organized yet. Claude can help you triage these later.

### Step 4: Write Your First Notes

Migrate whatever knowledge matters most to you. Start with things you look up repeatedly — processes you’ve documented, concepts you’ve researched, decisions you’ve made and why.

Don’t try to import everything at once. The wiki grows most naturally when you add notes as you encounter new information.

### Step 5: Install Claude Code

You’ll need Node.js installed. Then run:

```bash
npm install -g @anthropic-ai/claude-code
```

Authenticate with your Anthropic account and you’re ready.

### Step 6: Query Your Wiki

Open a terminal and navigate to your wiki folder:

```bash
cd ~/wiki
claude
```

Now ask questions:

- *“What notes do I have about machine learning interpretability?”*
- *“Summarize everything in my research folder related to RAG systems.”*
- *“I’m writing a proposal on X — what relevant notes do I have?”*
- *“Find any notes where I mentioned the vendor Acme Corp and summarize the key points.”*

Claude will read through your markdown files, identify what’s relevant, and give you a grounded answer. It’ll cite which files it drew from so you can verify and dig deeper.

If you want a more opinionated walkthrough of this exact pattern — including specific Obsidian plugins and Claude Code commands — [How to build an AI second brain with Claude Code and Obsidian](https://www.mindstudio.ai/blog/build-ai-second-brain-claude-code-obsidian) covers the operational details Karpathy’s high-level idea skips.

---

## Best Practices for a Queryable Knowledge Base

A few structural habits make a significant difference in how well Claude can work with your wiki.

### Write Summaries, Not Just Content

![Hermes, walked through line by line — free 1-hour workshop](https://i.mscdn.ai/1b7301c0-de42-4e46-b110-e9c55396e7ca/generated-images/8edf5cbc-5b63-4999-9079-6aeca2aafd65.png?fm=auto&w=1200)

The one-line summary at the top of each note is surprisingly important. Claude reads it to decide whether the full note is relevant. A good summary costs you ten seconds and saves the model from reading files that don’t apply.

### Use Consistent Terminology

If you write “RAG” in some notes and “retrieval augmented generation” in others, Claude can still connect them — but you’ll get cleaner results if you pick one term and use it consistently. Add a brief alias line if a concept has multiple names.

### Link Notes to Each Other

Obsidian’s `[[wiki links]]` format creates connections between notes. Claude can follow these connections, which means a well-linked wiki gives the model a richer graph to reason over than a flat collection of isolated files. For a deeper look at this same idea applied to large codebases, [Graphify’s knowledge-graph approach for Claude Code](https://www.mindstudio.ai/blog/graphify-claude-code-knowledge-graph-large-codebase-70x) compresses huge repositories into navigable mental models — the same principle that makes a well-linked wiki outperform a flat folder.

### Keep Notes Focused

A 10,000-word catch-all document is harder to query than ten focused 1,000-word notes. If a note is covering multiple distinct topics, split it. The more specific each file, the more precisely Claude can locate and apply it.

### Use a /inbox Pattern for Capture

Don’t let perfect be the enemy of useful. Dump rough notes into `/inbox`, then periodically ask Claude to help you clean them up and move them to the right place:

*“Look at my inbox folder and suggest where each note should be filed and what tags it should get.”*

---

## Advanced: Adding Semantic Search

The basic setup — Claude reading files directly — works well for wikis up to a few hundred notes. At larger scale, you’ll want to add a semantic search layer so Claude can narrow candidates before reading full files.

This is where RAG (Retrieval Augmented Generation) comes in. Tools like [LlamaIndex](https://www.llamaindex.ai/) let you build a vector index over your markdown files, which Claude can query to retrieve the most semantically relevant chunks before synthesizing an answer.

Another path: package the wiki-querying logic as a reusable [Claude Code skill](https://www.mindstudio.ai/blog/5-claude-code-skills-cut-token-costs-70-percent-benchmarked). A well-designed skill can pre-filter notes, summarize subsections, and route queries — cutting the token cost of every question you ask the wiki by a meaningful margin once it grows past a few hundred notes.

For most people starting out, this is overkill. The direct file-reading approach scales further than you’d expect, especially on a focused personal knowledge base. Add semantic search when you notice Claude struggling to find things that you know are in your wiki.

---

## Where MindStudio Fits This Workflow

If you want to take your personal knowledge base further — beyond your local machine, or into something a team can use — MindStudio is worth looking at.

MindStudio is a no-code platform for building AI agents and workflows. One natural application: wrap your markdown wiki in a MindStudio agent that anyone on your team can query through a clean web interface, without needing to touch Claude Code or a terminal.

You can build a knowledge base agent that:

- Accepts natural language questions through a custom UI
- Searches your wiki files (synced to Google Drive, Notion, or any connected storage)
- Returns cited, grounded answers
- Logs queries so you can see what people are looking for — and what your wiki is missing
![A free 1-hour Hermes workshop](https://i.mscdn.ai/1b7301c0-de42-4e46-b110-e9c55396e7ca/generated-images/922211b2-4085-4d29-85af-55d6920d46d0.png?fm=auto&w=1200)

MindStudio gives you access to Claude, GPT, Gemini, and 200+ other models out of the box, so you’re not locked into any single provider. And with 1,000+ pre-built integrations, connecting your wiki to Slack, email, or your project management tools takes minutes rather than a full engineering sprint.

If you’re building this kind of knowledge infrastructure for a small team, it’s a much faster path than standing up your own RAG pipeline. You can [try MindStudio free at mindstudio.ai](https://mindstudio.ai/).

For individual workflows — just you and your local files — Claude Code direct is the simpler approach. For anything shared or team-facing, MindStudio handles the infrastructure so you can focus on the knowledge itself. If you want to take the pattern further and let Claude Code orchestrate multiple knowledge sources at once, [building an agentic operating system on Claude Code](https://www.mindstudio.ai/blog/how-to-build-agentic-operating-system-claude-code) walks through how to layer skills, hooks, and routing on top of a base workflow like this one.

---

## Frequently Asked Questions

### What exactly is Karpathy’s LLM wiki?

It’s a personal knowledge management system built on plain markdown files, designed to be queried by an LLM rather than browsed manually. Andrej Karpathy has advocated for storing notes in a structured, LLM-readable format so that coding agents like Claude Code can answer questions, synthesize information, and help manage the knowledge base directly. The core insight is that organizing information for a model to read is different — and in many ways simpler — than organizing it for human navigation.

### How is this different from just using Notion AI or ChatGPT?

The key difference is that your knowledge lives in files you control, not in a proprietary system. With a local markdown wiki and Claude Code, the model reads your actual files. You’re not uploading data to a third-party knowledge base, and you’re not dependent on one company’s AI staying useful or affordable. You also get much more precise answers because Claude is reading *your* specific notes, not doing a web search or drawing on general training data.

### Do I need to know how to code to use Claude Code?

No. Claude Code runs in a terminal and you interact with it through natural language. You type questions; it responds and reads your files. The “code” in the name refers to its ability to write and edit code — but for a personal wiki use case, you’re mostly asking questions and getting answers. If you’re comfortable opening a terminal and running one install command, you can use it.

### How many notes can Claude Code handle at once?

Claude’s context window is large — Claude 3.5 Sonnet supports around 200,000 tokens — which means it can comfortably read tens of thousands of words in a single session. For most personal wikis (up to a few hundred focused notes), this is more than enough. You’ll only need semantic search or RAG if your wiki grows very large, or if you need faster response times on a huge corpus.

### Is Obsidian required, or can I use a different editor?

![Wondering what the Hermes hype is about? Free 60-minute primer](https://i.mscdn.ai/1b7301c0-de42-4e46-b110-e9c55396e7ca/generated-images/c8d61682-41d9-44c0-a2fe-5299b2d46f88.png?fm=auto&w=1200)

Obsidian isn’t required. It’s just a convenient front-end for reading and writing markdown files. You could use VS Code, Typora, iA Writer, Zed, Vim, or any text editor. The wiki is just a folder of `.md` files. Obsidian is recommended because its graph view, backlinks, and plugin ecosystem are useful for managing a growing knowledge base — but Claude Code doesn’t care what editor you use.

### Can I use this workflow with other AI models besides Claude?

Yes. The markdown wiki pattern works with any model that can read files. Claude Code is the most natural interface because it’s built to work directly with your local filesystem. GPT-4 via the OpenAI API, Gemini, or any other capable model can also be pointed at markdown files through similar agent frameworks. Claude tends to perform well for document synthesis tasks, which is why it’s the common recommendation for this use case.

---

## Key Takeaways

- Karpathy’s LLM wiki is a simple pattern: structured markdown files, queried by Claude Code through natural language
- Plain markdown is the right format because it’s portable, future-proof, and something LLMs read natively
- Obsidian is the best front-end for managing the files — your data stays local and file-based
- Claude Code connects to your local filesystem directly, no copy-pasting required
- A summary line and consistent tags on each note dramatically improve query quality
- For team-facing or scaled knowledge bases, MindStudio can wrap the same concept in a shareable, no-code agent with a proper UI

The best knowledge management system is one you’ll actually use. A folder of markdown files is about as low-friction as it gets — and pointing Claude at it takes five minutes. Start small, keep notes focused, and let the system grow with you.