依照 CLAUDE.md 的 Ingest 工作流程，入庫指定的來源文件。

使用方式：`/ingest raw/sources/filename.md` 或 `/ingest`（不帶參數時掃描 raw/sources/ 列出未入庫的檔案）

步驟：

1. 若未指定檔案，掃描 `raw/sources/` 中所有檔案，比對 `wiki/sources/` 中已存在的文摘，列出尚未入庫的來源，讓使用者選擇
2. 閱讀原始來源全文
3. 與使用者討論重點與有趣之處
4. 建立來源文摘於 `wiki/sources/`（格式依 CLAUDE.md）
5. 更新或建立相關概念頁（`wiki/concepts/`）
6. 更新或建立相關實體頁（`wiki/entities/`）
7. 更新交叉引用：檢查現有 wiki 頁面，在相關處加入連結
8. 更新 `index.md`：加入新頁面條目
9. 追加 `log.md`：記錄本次 ingest（日期、來源、建立的頁面、更新的頁面、備註）
10. 向使用者報告：建立了哪些頁面、更新了���些頁面、發現了什麼有趣的關聯
