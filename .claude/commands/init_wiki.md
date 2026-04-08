依照 CLAUDE.md 的規則，初始化本 vault 的 LLM Wiki 結構。

步驟：

1. 讀取 CLAUDE.md，確認 Schema 存在
2. 將 CLAUDE.md 中的 `{VAULT_NAME}` 替換為本 vault 的實際目錄名稱
3. 建立目錄結構：`raw/sources/`、`raw/assets/`、`wiki/sources/`、`wiki/concepts/`、`wiki/entities/`、`wiki/analyses/`
4. 建立 `index.md`（空索引，格式依 CLAUDE.md 定義）
5. 建立 `log.md`（記錄 init 事件，含日期與建立的目錄清單）
6. 掃描 `raw/sources/` 是否已有檔案，若有則列出並詢問是否立即入庫
7. 向使用者確認初始化完成，並說明可用的操作（/ingest、/lint、直接提問）
