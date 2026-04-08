# LLM Wiki Template

一個用 LLM 建構個人知識庫的 vault 模板（繁體中文版）。

有別於傳統 RAG（每次查詢時從原始文件檢索），LLM 會**增量編譯並維護一個結構化的 wiki**——摘要、概念頁、實體頁、交叉引用——隨著你加入來源持續更新。知識是累積的，不是每次重新推導。

靈感來自 [Andrej Karpathy 的做法](https://x.com/karpathy/status/2039805659525644595) 和他的 [llm-wiki 模式文件](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)。

## 結構

```
your-vault/
├── CLAUDE.md              ← Schema：規則、頁面格式、工作流程
├── index.md               ← Wiki 索引（自動維護）
├── log.md                 ← 時間順序操作日誌
├── raw/
│   ├── sources/           ← 你的來源文件（文章、論文、筆記）
│   └── assets/            ← 下載的圖片附件
├── wiki/
│   ├── sources/           ← 來源文摘
│   ├── concepts/          ← 概念文章
│   ├── entities/          ← 實體頁面（人物、工具、組織）
│   └── analyses/          ← 歸檔的查詢結果與分析
└── .claude/
    └── commands/
        ├── init-wiki.md   ← /init-wiki — 初始化 vault 結構
        ├── ingest.md      ← /ingest — 將來源處理進 wiki
        └── lint.md        ← /lint — Wiki 健康檢查
```

## 快速開始

1. 將模板複製到新的 vault：

**macOS / Linux：**
```bash
cp -r llm-wiki-template/* llm-wiki-template/.claude /path/to/your-vault/
```

**Windows（PowerShell）：**
```powershell
Copy-Item -Recurse llm-wiki-template\* path\to\your-vault\
Copy-Item -Recurse llm-wiki-template\.claude path\to\your-vault\
```

2. 在 vault 目錄開啟 Claude Code session。

3. 執行 `/init-wiki` 建立目錄結構、索引和日誌。

4. 將來源檔案放入 `raw/sources/`。支援的格式包括 Markdown、PDF、Word、純文字、圖片等。網頁文章可透過 [Obsidian Web Clipper](https://obsidian.md/clipper) 擷取為 Markdown。

5. 執行 `/ingest` 將來源處理進 wiki。

6. 直接提問——LLM 會閱讀 wiki 回答，不是每次重新處理原始來源。

7. 定期執行 `/lint` 檢查 wiki 健康狀態。

## 運作方式

**你**負責策展來源、提問和思考。**LLM** 負責其餘一切——摘要、交叉引用、歸檔、維護所有 wiki 頁面的一致性。

### 三個核心操作

| 操作 | 觸發方式 | 說明 |
|------|----------|------|
| **Ingest** | `/ingest` | LLM 閱讀來源、建立文摘、更新概念／實體頁面、維護交叉引用 |
| **Query** | 直接提問 | LLM 讀取 wiki 索引、找到相關頁面、綜合回答。有價值的回答可歸檔為分析頁 |
| **Lint** | `/lint` | LLM 檢查矛盾、孤立頁面、缺頁概念、過時資訊，並建議新的探索方向 |

### 設計原則

- `raw/` 是唯讀的——LLM 永遠不修改原始來源
- `wiki/` 由 LLM 完全擁有——你閱讀，LLM 撰寫與維護
- wiki 中的每個主張都可追溯到來源
- 交叉引用是核心價值——寧可多連結，不要少連結
- 知識編譯一次並持續更新，不是每次查詢重新推導

## 建議搭配

- **[Obsidian](https://obsidian.md/)** 作為瀏覽器——瀏覽 wiki、用 graph view 查看連結關係
- **[Obsidian Web Clipper](https://obsidian.md/clipper)** 將網頁文章擷取為 markdown
- **一個領域一個 vault**——保持每個知識庫的焦點，索引也更好管理

## 授權

MIT
