# LLM Wiki Template

A ready-to-use vault template for building personal knowledge bases with LLMs.

Instead of traditional RAG (retrieving from raw documents on every query), the LLM **incrementally compiles and maintains a structured wiki** — summaries, concept pages, entity pages, cross-references — all kept current as you add sources. The knowledge compounds over time rather than being re-derived from scratch.

Inspired by [Andrej Karpathy's approach](https://x.com/karpathy/status/2039805659525644595) and [Tobi Lütke's LLM Wiki pattern](https://github.com/tobi/llm-wiki).

## Structure

```
your-vault/
├── CLAUDE.md              ← Schema: rules, page formats, workflows
├── index.md               ← Wiki index (auto-maintained)
├── log.md                 ← Chronological operation log
├── raw/
│   ├── sources/           ← Your source documents (articles, papers, notes)
│   └── assets/            ← Downloaded images
├── wiki/
│   ├── sources/           ← Source digests
│   ├── concepts/          ← Concept articles
│   ├── entities/          ← Entity pages (people, tools, orgs)
│   └── analyses/          ← Filed query results and comparisons
└── .claude/
    └── commands/
        ├── init_wiki.md   ← /init_wiki — initialize vault structure
        ├── ingest.md      ← /ingest — process a source into the wiki
        └── lint.md        ← /lint — wiki health check
```

## Quick Start

1. Copy the template into a new vault:

```bash
cp -r llm-wiki-template/* llm-wiki-template/.claude /path/to/your-vault/
```

2. Open a Claude Code session in the vault directory.

3. Run `/init_wiki` to set up the directory structure, index, and log.

4. Drop source files (markdown, via [Obsidian Web Clipper](https://obsidian.md/clipper) or manually) into `raw/sources/`.

5. Run `/ingest` to process sources into the wiki.

6. Ask questions — the LLM answers by reading the wiki, not re-processing raw sources.

7. Run `/lint` periodically to health-check the wiki.

## How It Works

**You** curate sources, ask questions, and think. **The LLM** does everything else — summarizing, cross-referencing, filing, and maintaining consistency across all wiki pages.

### Three Operations

| Operation | Trigger | What happens |
|-----------|---------|--------------|
| **Ingest** | `/ingest` | LLM reads a source, creates a digest, updates concept/entity pages, maintains cross-references |
| **Query** | Ask any question | LLM reads the wiki index, finds relevant pages, synthesizes an answer. Valuable answers can be filed back as analysis pages |
| **Lint** | `/lint` | LLM checks for contradictions, orphan pages, missing concepts, stale info, and suggests new explorations |

### Design Principles

- `raw/` is read-only — the LLM never modifies source documents
- `wiki/` is LLM-owned — you read it, the LLM writes and maintains it
- Every claim in the wiki traces back to a source
- Cross-references are the core value — link generously
- Knowledge is compiled once and kept current, not re-derived on every query

## Recommended Setup

- **[Obsidian](https://obsidian.md/)** as the viewer — browse the wiki, use graph view to see connections
- **[Obsidian Web Clipper](https://obsidian.md/clipper)** to capture web articles as markdown
- **One vault per domain** — keeps each knowledge base focused and the index manageable

## License

MIT
