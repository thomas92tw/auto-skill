## 🔧 BlogWatcher 報告規格優化與雙軌制監控 (Dual-Path)
**日期：** 2026-02-11
**技能：** blogwatcher
**情境：** 為提升報告資訊密度並防止非權威來源（如 Wikipedia）混入，確立雙軌制執行模式。
**解法：**
- **雙軌運作 (Dual-Path)**：
    1. **精準搜尋 (Brave Search API)**：設定 `freshness="pd"` 抓取過去 24 小時即時動態。
    2. **廣泛搜尋 (BlogWatcher RSS)**：鎖定垂直媒體與個人部落格 (如 Stratechery) 的戰略深度。
- **嚴格網域過濾 (Authority Filtering)**：
    - 建立 `ALLOWED_DOMAINS` 列表，非列表網域強制剔除。
    - **一區一門戶 (Regional Portals)**：確立區域權威來源，排除 Vocus, Medium, Substack 等個人創作平台。
- **深度路徑校驗 (Path Depth Validation)**：
    - 禁止取用媒體根目錄 (首頁) URL，路徑深度至少需包含 1 個段落 (確保連向具體文章)。
    - **內容黑名單**：排除包含 `search`, `category`, `tag`, `author` 等索引性質的 URL，解決「點擊後找不到具體訊息」的問題。
- **路徑修正**：將 `OBSIDIAN_VAULT_PATH` 定位為 iCloud Documents 根目錄。
- **術語規範**：禁止直譯 `ASEAN/亞細安`，統一修正為 `亞洲`。
**關鍵檔案/路徑：**
- `/Users/thomastseng/Documents/Antigravity_Workspace/Antigravity_System/skills/blogwatcher/daily_report_generator.py`
- `/Users/thomastseng/Documents/Antigravity_Workspace/Antigravity_System/skills/blogwatcher/monitoring_lists.md`
**keywords：** dual-path, blogwatcher, authority-filter, regional-portals, strategic-analysis, traditional-chinese
