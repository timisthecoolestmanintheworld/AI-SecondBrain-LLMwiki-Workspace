---
title: "What is OKF? Understanding Google’s Open Knowledge Format"
source: "https://www.gitbook.com/blog/what-is-okf-open-knowledge-format"
author:
published:
created: 2026-09-28
description: "Learn how Google’s Open Knowledge Format (OKF) structures markdown documentation for AI agents, how it compares to RAG, and what documentation teams can do today to make their docs more agent-ready | 18 Jun, 2026"
tags:
  - "clippings"
---
AI summary

Google’s Open Knowledge Format (OKF) is an open, markdown-based specification designed to structure documentation into traversable knowledge graphs for AI agents, moving beyond the limitations of standard RAG systems. By adopting structured metadata, consistent cross-linking, and version-controlled markdown, documentation teams can make their knowledge agent-ready without needing to author a separate, proprietary format.

## TL;DR

The Open Knowledge Format (OKF) is a vendor-neutral, markdown-based open specification from Google Cloud that turns structured documentation into traversable knowledge. A bundle is a directory of markdown files with YAML frontmatter, cross-linked so an AI agent can traverse it deliberately instead of guessing.

This post explains what OKF is, why it changes how you think about docs, and what documentation teams should do about it now.

## The problem OKF is solving

[AI agents read your knowledge](https://www.gitbook.com/blog/what-is-mcp-server-documentation) badly because your knowledge lives everywhere and lacks consistency and structure. RAG chops documents into fragments and retrieves them by similarity, but the relationships between concepts often have to be inferred rather than explicitly represented. At the same time, Metadata catalogs describe the shape of your data behind their own APIs, but they say nothing about how a metric is computed or why a table exists.

Markdown dumps fix the fragmentation but reintroduce the chaos. A folder of `.md` files has no agreed convention for what a document is about, how documents link, or which fields an agent can query.

Plenty of teams already built around this gap. [Andrej Karpathy’s LLM Wiki gist](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) named the pattern, and `AGENTS.md` files, Obsidian vaults wired to coding agents, and “metadata as code” repos all chase the same idea. Each one is bespoke. You have no standard way to hand structured knowledge to an agent, so every agent builder solves context assembly from scratch.

## What OKF actually is

[OKF](https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf) is an open specification from [Google Cloud](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) that defines how to package knowledge as a directory of markdown files with YAML frontmatter, cross-linked into a graph that AI agents can read. [The v0.1 spec](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md) fits on a single page. It sets a small number of conventions so that a knowledge bundle written by one producer can be consumed by any agent without translation.

It’s equally important to understand what OKF doesn’t do. It’s not a runtime, so you do not install anything to use it. It’s not a search index, so it does not retrieve or rank fragments for you. It’s not a model. Google puts it plainly: “What’s missing is a format, not another service.”

The format builds on the LLM-wiki pattern that developers had already started using. Karpathy described the idea in his LLM Wiki gist, and you have probably seen variations of it already in [AGENTS.md](http://agents.md/) files and Obsidian vaults wired to coding agents.

Each of those efforts stayed bespoke, with no shared rules for what fields a document carries or what filenames mean. OKF turns the pattern into a defined schema with a portability guarantee, so the same bundle works across tools, clouds, and agent frameworks.

## How an OKF bundle works

A bundle is a directory of markdown files where each file represents one concept. A concept can be a table, a dataset, a metric, a runbook, or an API endpoint.

For example, a SaaS company might represent its `orders` table, its “weekly active users” metric, and the runbook used to investigate billing failures as three separate concepts linked together through markdown references.

The file path becomes the concept’s identity, so `metrics/weekly_active_users.md` is both the location and the address other documents point to.

Every file carries YAML frontmatter on top and a markdown body below. The frontmatter holds the queryable fields. OKF v0.1 reserves six of them.

```
---
type: BigQuery Table
title: Orders
description: One row per completed customer order.
resource: <https://console.cloud.google.com/bigquery?p=acme&d=sales&t=orders>
tags: [sales, revenue]
```

Only `type` is required. The producer decides what types exist and what other fields each document carries, which keeps the spec [minimally opinionated](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing).

Concepts connect to each other with ordinary markdown links. A link from `metrics/weekly_active_users.md` to `tables/orders.md` turns a flat directory into a graph that captures relationships the filesystem alone cannot express. `index.md` files act as entry points and offer progressive disclosure. `log.md` files record chronological change history. Both are optional.

An agent navigates the bundle by reading an `index.md`, scoping to a topic, then following links the same way you would click through a wiki. Link resolution is just path resolution, so the agent traverses deliberately rather than guessing. No SDK, no runtime, and no proprietary schema sits between the agent and the files. You can ship the whole thing as a tarball, host it in a git repo, or mount it on a filesystem.

## OKF vs. RAG and metadata catalogs

Retrieval-augmented generation pulls fragments at query time. You embed your docs, store the vectors, and at runtime the system fetches the chunks that look closest to the question. The agent never sees how those chunks relate. It guesses at structure from whatever text happens to land in the context window.

OKF inverts that process. The relationships are written down before the agent ever asks a question. Concepts link to each other with markdown links, so the agent can start at one file and walk to the orders table, then to the metric that depends on it, then to the runbook that explains the join. It traverses meaning deliberately instead of stitching together whatever the retriever returned.

Metadata catalogs and OpenAPI specs solve a different problem. They describe shapes. A catalog tells an agent that a column is a timestamp and a table has ten million rows. An OpenAPI spec tells it which endpoints exist and what they accept. Neither tells it what the data means or why two things connect.

OKF describes meaning and linkage. RAG answers “what text is similar to this query.” A schema answers “what does this data look like.” OKF answers “how does this knowledge fit together.”

Here’s a quick summary that explains the differences between OKF, RAG and metadata catalogs:

| OKF | RAG | Metadata catalogs |
| --- | --- | --- |
| Represents relationships between concepts | Retrieves relevant text | Describes data structures |
| Markdown + YAML | Vector embeddings | Schema metadata |
| Traversable knowledge graph | Similarity search | Data inventory |
| Human and AI readable | Primarily retrieval-oriented | Primarily governance-oriented |

## What OKF means for documentation teams

OKF changes who reads your documentation. The same markdown files you write for engineers and users [now feed the agents that answer questions on their behalf](https://gitbook.com/docs/ai-and-search/llm-ready-docs). Your docs become the knowledge layer an agent traverses, which means the quality of your docs sets a ceiling on the quality of the agent’s answers.

The practical demands are specific. Headings have to map cleanly to concepts, because an agent uses structure to scope what it reads. Frontmatter has to be consistent across pages, because OKF makes fields like `type`, `title`, and `description` queryable. Cross-links between related pages stop being a nicety and start carrying real weight, because they form the graph an agent walks to assemble context.

Version control matters for the same reason it matters in code. An agent reasoning over a stale bundle gives confidently wrong answers. Git-backed history tells you what changed, when, and against which version of a concept, so you can trust what the agent is reading.

The implications of ignoring this are real. If your docs live in a wiki with no consistent structure, or scatter the same information across three pages with no links between them, no OKF producer can turn that mess into a clean bundle. You can wire up the best agent framework available and still get poor answers, because the knowledge underneath is unstructured. If you treat documentation as a publishing afterthought, that afterthought becomes the bottleneck. If you already write structured and versioned markdown with links included, you have most of the work done.

## Preparing your docs for OKF

Even if you never publish an OKF bundle, the practices behind the format are worth adopting now. Agents are increasingly reading your documentation whether or not you’ve packaged it as OKF, whether they [scrape your docs regularly](https://www.gitbook.com/blog/ai-docs-data-april-2026) or [connect to an MCP docs server](https://gitbook.com/docs/ai-and-search/mcp-servers-for-published-docs). And the same structural habits that make a bundle useful make your docs better for every reader.

- **Structure content around clear concepts.** Each page should cover one thing, whether that’s a feature, a process, an API endpoint, or something else. Pages that mix multiple concerns are harder for agents to scope and harder for humans to maintain.
- **Add metadata consistently.** OKF reserves fields like `type`, `title`, and `description` for a reason: they make content queryable. Even outside OKF, consistent frontmatter or page properties let tools reason about your docs rather than just read them.
- **Link related topics together.** Explicit cross-links are how OKF builds its knowledge graph. In any docs system, links between related pages reduce the chance an agent — or a reader — has to guess at connections.
- **Keep documentation under version control.** [Git-backed history](https://gitbook.com/docs/getting-started/git-sync) is load-bearing in OKF because it keeps paths stable and lets you trust what the agent is reading. The same is true for any team that needs to audit changes or roll back a bad edit.
- **Reduce duplicated information across pages.** Duplication is the enemy of structured knowledge. When the same fact lives in three places, updates break consistency and agents may retrieve contradictory answers.

## Why markdown-native, version-controlled docs are the foundation

OKF makes three demands of any knowledge source, and they read like a description of good documentation practice. The format stores concepts as plain markdown files, so the source has to author in markdown rather than export to it. Each concept needs queryable YAML frontmatter, which means structured fields written consistently across every page.

The third requirement is harder for most tools to meet. OKF ships a `log.md` convention for chronological change history, and the file path itself acts as a concept’s identity. A knowledge source that moves or renames pages freely breaks the graph. You need [Git-backed versioning](https://www.gitbook.com/features/git-sync) so links resolve, paths stay stable, and an agent can trust that yesterday’s reference still points somewhere.

Fortunately, many modern documentation workflows already align with these requirements. GitBook, for example, [already works this way through it’s two-way Git Sync workflow](https://gitbook.com/docs/getting-started/git-sync). Pages are rendered in markdown, synced to a Git repository, and carry structured metadata rather than free-form layout. The version history you rely on for human review is the same versioning OKF treats as load-bearing.

None of this requires a separate pipeline to produce OKF bundles. A documentation set that is markdown-native, versioned, and consistently structured already holds the raw material the format expects. The work is the discipline, not the export.

## GitBook as an OKF-ready knowledge source

A GitBook space already looks like the directory OKF describes. You can write pages in markdown, organize them into a navigable hierarchy, and link concepts to each other the same way an OKF bundle turns a folder of files into a traversable graph. The structure an agent needs is the same structure you build for human readers.

The capabilities map cleanly. GitBook pages carry structured headings and metadata, so the frontmatter fields OKF reserves have a natural home. Git Sync keeps your docs in a version-controlled repository, which gives you the file-and-history backbone OKF expects. [GitBook also exposes machine-readable output](https://gitbook.com/docs/getting-started/ai-documentation), so an agent can read the same content your readers see.

GitBook gives your docs a dual life. You maintain one set of docs that publishes a clean site for people and serves organized, linked knowledge to agents reasoning over it.

If you want documentation to work for both audiences at once, GitBook is the best starting point. You write docs the way you already do, keep them in version control, and end up with a knowledge source an OKF consumer can read without a rewrite.

Check how AI-friendly your current docs are using [this agent-readiness checker](https://www.gitbook.com/agent-score), which highlights areas for improvement to make your docs more readable by agents.

## FAQs

**Is OKF the same as an LLM wiki?**

No. An LLM wiki is the practice of keeping cross-linked markdown notes that an agent can read and update. OKF formalizes that practice into a portable schema with a required `type` field and a small set of reserved frontmatter fields, so a bundle written by one producer works with any consumer without translation.

**Do I need to restructure all my docs to use OKF?**

Not entirely. OKF requires one thing of every concept document: a `type` field in YAML frontmatter. Consistent headings, explicit cross-links, and one concept per file make a bundle far more useful to an agent, but the spec leaves your content model to you.

**Does OKF replace RAG?**

No. RAG retrieves text fragments at query time based on similarity. OKF gives an agent a pre-structured graph it can traverse deliberately. Many agent stacks will run both, using OKF for relational context and retrieval for long-tail lookups.

**Is OKF only for Google Cloud?**

No. Google authored the spec, but OKF is vendor-neutral by design and requires no proprietary account, runtime, or SDK. A bundle is plain markdown and YAML you can host in any git repo, mount on any filesystem, or ship as a tarball.

## Conclusion

OKF turns well-structured documentation into a first-class input for AI agents rather than a human-only output. If you already write markdown-native, version-controlled, cross-linked docs, you can produce OKF-compatible bundles without a rewrite. And if your documentation already has good structure, solid links, and version-control, youre much closer to OKF readiness than you might think.

Start with documentation that is [already agent-ready](https://gitbook.com/docs/getting-started/ai-documentation). [GitBook](https://gitbook.com/) gives you the markdown-native, Git-backed structure OKF expects, so your docs serve both readers and agents from one source.

[**→ Research: Do AI coding agents actually read your docs?**](https://www.stateofdocs.com/research/projects/do-ai-coding-agents-actually-read-your-docs)

[**→ MCP explained: What is an MCP server and why it matters for documentation**](https://www.gitbook.com/blog/what-is-mcp-server-documentation)

[**→ Research: AI agents are now the majority reader of your docs**](https://www.gitbook.com/blog/ai-docs-data-april-2026)

![ContentGaps, LinkAudit, revamped Analytics](https://framerusercontent.com/images/8f7ViPrlXMlHw7TAw0EFnTRTlfo.png?width=1620&height=847)

Oct 1, 2026

### [A new quality layer for documentation: What's new in GitBook](https://www.gitbook.com/events/quality-2026)

Read more

Industry

[The writing was never the hard part: notes from the State of Docs panel with WTD NYC](https://stateofdocs.com/blog/the-writing-was-never-the-hard-part-notes-from-the-state-of-docs-panel-with-wtd-nyc)

[Improving your docs and advocating for them are two different jobs](https://www.gitbook.com/blog/documentation-metrics-that-matter)

[Supporting AI standards at GitBook: What OKF, MCP and llms.txt tell us about the future of docs](https://www.gitbook.com/blog/supporting-ai-standards-gitbook)

[Humans are still the real readers of your documentation](https://www.gitbook.com/blog/humans-are-still-your-doc-readers)

[5 things we’re still thinking about after Write the Docs Portland](https://www.gitbook.com/blog/write-the-docs-portland-2026)[View all blog posts](https://www.gitbook.com/blog)

Get the latest product news, useful resources and more in your inbox. **130k+** people read it every month.

Email

![](https://framerusercontent.com/images/bFH6d5ctekz3XMtNpISWvpO0kaE.png?width=1600&height=900)

25 Aug, 2026

##### [The writing was never the hard part: notes from the State of Docs panel with WTD NYC](https://stateofdocs.com/blog/the-writing-was-never-the-hard-part-notes-from-the-state-of-docs-panel-with-wtd-nyc)

![A profile photo of Tal Gluck](https://framerusercontent.com/images/jGNbrY1fo6UxnGwJBOIq1wjRkWQ.jpeg?width=512&height=512)

Tal Gluck

DevRel

![Docs sites measurements including page views, search terms, and support topics](https://framerusercontent.com/images/l4rqMQbr3y42fSIvibtLKgnMM.png?width=2293&height=1204)

3 Aug, 2026

##### [Improving your docs and advocating for them are two different jobs](https://www.gitbook.com/blog/documentation-metrics-that-matter)

![A profile photo of Tal Gluck](https://framerusercontent.com/images/jGNbrY1fo6UxnGwJBOIq1wjRkWQ.jpeg?width=512&height=512)

Tal Gluck

DevRel

![Display of AI standards including OKF, MCP, and llms.text](https://framerusercontent.com/images/4w4ZRqZj5O3Z684na9ln0W7VI.png?width=2293&height=1204)

22 Jun, 2026

##### [Supporting AI standards at GitBook: What OKF, MCP and llms.txt tell us about the future of docs](https://www.gitbook.com/blog/supporting-ai-standards-gitbook)

![A headshot of Steven Hall](https://framerusercontent.com/images/G9IZam8RIzcDdQUfsNZIOqOWTA.jpeg?width=512&height=512)

Steven Hall

Head of Engineering[View all blog posts](https://www.gitbook.com/blog)

## Accurate docs. Better answers.

Your docs are already feeding AI. Are users getting the right answers or the wrong ones?

We use cookies to personalize content, run ads, and analyze traffic.