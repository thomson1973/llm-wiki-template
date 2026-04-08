# LLM Wiki Template

A ready-to-use vault template for building personal knowledge bases with LLMs.

一個用 LLM 建構個人知識庫的 vault 模板。

Instead of traditional RAG (retrieving from raw documents on every query), the LLM **incrementally compiles and maintains a structured wiki** — summaries, concept pages, entity pages, cross-references — all kept current as you add sources. The knowledge compounds over time rather than being re-derived from scratch.

有別於傳統 RAG（每次查詢時從原始文件檢索），LLM 會**增量編譯並維護一個結構化的 wiki**——摘要、概念頁、實體頁、交叉引用——隨著你加入來源持續更新。知識是累積的，不是每次重新推導。

Inspired by [Andrej Karpathy's approach](https://x.com/karpathy/status/2039805659525644595) and [Tobi Lütke's LLM Wiki pattern](https://github.com/tobi/llm-wiki).

靈感來自 [Andrej Karpathy 的做法](https://x.com/karpathy/status/2039805659525644595) 和 [Tobi Lütke 的 LLM Wiki 模式](https://github.com/tobi/llm-wiki)。

## Structure / 結構

```
your-vault/
├── CLAUDE.md              ← Schema: rules, page formats, workflows
│                            Schema：規則、頁面格式、工作流程
├── index.md               ← Wiki index (auto-maintained)
│                            Wiki 索引（自動維護）
├── log.md                 ← Chronological operation log
│                            時間順序操作日誌
├── raw/
│   ├── sources/           ← Your source documents (articles, papers, notes)
│   │                        你的來源文件（文章、論文、筆記）
│   └── assets/            ← Downloaded images
│                            下載的圖片附件
├── wiki/
│   ├── sources/           ← Source digests / 來源文摘
│   ├── concepts/          ← Concept articles / 概念文章
│   ├── entities/          ← Entity pages (people, tools, orgs)
│   │                        實體頁面（人物、工具、組織）
│   └── analyses/          ← Filed query results and comparisons
│                            歸檔的查詢結果與分析
└── .claude/
    └── commands/
        ├── init_wiki.md   ← /init_wiki — Initialize vault structure / 初始化 vault 結構
        ├── ingest.md      ← /ingest — Process a source into the wiki / 將來源處理進 wiki
        └── lint.md        ← /lint — Wiki health check / Wiki 健康檢查
```

## Quick Start / 快速開始

1. Copy the template into a new vault: / 將模板複製到新的 vault：

```bash
cp -r llm-wiki-template/* llm-wiki-template/.claude /path/to/your-vault/
```

2. Open a Claude Code session in the vault directory. / 在 vault 目錄開啟 Claude Code session。

3. Run `/init_wiki` to set up the directory structure, index, and log. / 執行 `/init_wiki` 建立目錄結構、索引和日誌。

4. Drop source files (markdown, via [Obsidian Web Clipper](https://obsidian.md/clipper) or manually) into `raw/sources/`. / 將來源檔案放入 `raw/sources/`。

5. Run `/ingest` to process sources into the wiki. / 執行 `/ingest` 將來源處理進 wiki。

6. Ask questions — the LLM answers by reading the wiki, not re-processing raw sources. / 直接提問——LLM 會閱讀 wiki 回答，不是每次重新處理原始來源。

7. Run `/lint` periodically to health-check the wiki. / 定期執行 `/lint` 檢查 wiki 健康狀態。

## How It Works / 運作方式

**You** curate sources, ask questions, and think. **The LLM** does everything else — summarizing, cross-referencing, filing, and maintaining consistency across all wiki pages.

**你**負責策展來源、提問和思考。**LLM** 負責其餘一切——摘要、交叉引用、歸檔、維護所有 wiki 頁面的一致性。

### Three Operations / 三個核心操作

| Operation / 操作 | Trigger / 觸發 | Description / 說明 |
|---|---|---|
| **Ingest** | `/ingest` | LLM reads a source, creates a digest, updates concept/entity pages, maintains cross-references / LLM 閱讀來源、建立文摘、更新概念／實體頁面、維護交叉引用 |
| **Query** | Ask directly / 直接提問 | LLM reads the wiki index, finds relevant pages, synthesizes an answer. Valuable answers can be filed as analysis pages / LLM 讀取索引、找到相關頁面、綜合回答。有價值的回答可歸檔為分析頁 |
| **Lint** | `/lint` | LLM checks for contradictions, orphan pages, missing concepts, stale info, and suggests explorations / LLM 檢查矛盾、孤立頁面、缺頁概念、過時資訊，並建議新探索方向 |

### Design Principles / 設計原則

- `raw/` is read-only — the LLM never modifies source documents / `raw/` 是唯讀的——LLM 永遠不修改原始來源
- `wiki/` is LLM-owned — you read it, the LLM writes and maintains it / `wiki/` 由 LLM 完全擁有——你閱讀，LLM 撰寫與維護
- Every claim in the wiki traces back to a source / wiki 中的每個主張都可追溯到來源
- Cross-references are the core value — link generously / 交叉引用是核心價值——寧可多連結，不要少連結
- Knowledge is compiled once and kept current, not re-derived on every query / 知識編譯一次並持續更新，不是每次查詢重新推導

## Recommended Setup / 建議搭配

- **[Obsidian](https://obsidian.md/)** as the viewer — browse the wiki, use graph view to see connections / 作為瀏覽器——瀏覽 wiki、用 graph view 查看連結關係
- **[Obsidian Web Clipper](https://obsidian.md/clipper)** to capture web articles as markdown / 將網頁文章擷取為 markdown
- **One vault per domain** — keeps each knowledge base focused and the index manageable / 一個領域一個 vault——保持焦點，索引也更好管理

## License / 授權

MIT
