## 🔧 ThinkTank / BlogWatcher v5.2 智庫級監測經驗庫
**日期：** 2026-02-14
**技能：** thinktank
**情境：** 整合 BlogWatcher v5.0 以來的進階動態，確立以 ThinkTank 為核心的戰略監察規格。
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
- **檔案命名與整潔管理 (File Naming & Clean Management)**：
    - **精簡資料夾結構**：將所有報告統一儲存於 `Blogwatcher_Report` 資料夾，移除冗餘的 `BlogWatcher` 與 `BlogWatcher_Reports` 分類。
    - **統一命名規範**：將 Obsidian 報告檔案統一為 `YYYYMMDD.md` 格式（如 `20260212.md`）。
    - **雙重命名備援 (Legacy Backup)**：為確保 Obsidian 搜尋相容性，生成 `YYYYMMDD.md` 的同時，保留一份 `YYYY-MM-DD 每日洞察.md` 的複本於同資料夾。
    - **自動標題對齊**：腳本生成時自動在開頭加入 `# YYYYMMDD` 標題。
- **AI 全自動翻譯 (LLM Translation Integration)**：
    - **Gemini 整合**：整合 `google-genai` 套件，使用 `gemini-2.0-flash` 模型對新聞標題與概要進行高品質繁體中文翻譯（包含台灣用語校準）。
    - **API 金鑰管理**：API Key (`AIzaSy...`) 已直接嵌入 `daily_report_generator.py` 的 `GEMINI_API_KEY` 變數中。
- **路徑修正**：將 `OBSIDIAN_VAULT_PATH` 定位為 `/Users/thomastseng/Library/Mobile Documents/iCloud~md~obsidian/Documents`。
- **術語規範**：禁止直譯 `ASEAN/亞細安`，統一修正為 `亞洲`。
- **時效性參數微調 (Time Sensitivity Tuning)**：
    - 將 `brave_search` 的 `freshness` 參數從 `pw` (Past Week) 調整為 `pd` (Past Day)，可顯著提升報告的即時性，但需注意這會導致在新聞淡季時報告篇幅變短。
    - **參數建議**：平日建議使用 `pd` 維持即時監測；週末或長假結束後可改回 `pw` 以捕捉遺漏的重大消息。
- **深度摘要規格 (Strategic Prompt v1.0)**：
    - 切換 LLM 角色為「科技與經貿戰略分析師」，要求產出約 **150 字** 的繁體中文深度摘要。
    - 內容涵蓋：事件背景、核心動態、潛在影響，提升報告的洞察價值。
- **防止覆蓋**：在寫入 Obsidian 之前，先檢查檔案是否存在。如果存在，必須詢問用戶。
**關鍵檔案/路徑：**
- `~/Library/Mobile Documents/com~apple~CloudDocs/Documents/Antigravity_Workspace/Antigravity_System/skills/blogwatcher/daily_report_generator.py`
- `~/Library/Mobile Documents/com~apple~CloudDocs/Documents/Antigravity_Workspace/Antigravity_System/skills/blogwatcher/monitoring_lists.md`
**keywords：** dual-path, blogwatcher, authority-filter, gemini-translation, traditional-chinese, obsidian-sync, freshness-tuning, strategy-prompt, overwrite-protection

## 🔧 Paywall Fallback & Accessibility (付費牆備援機制)
**日期：** 2026-02-12
**技能：** blogwatcher
**情境：** 解決 Bloomberg/WSJ 等高價值新聞因付費牆無法閱讀，導致使用者體驗中斷的問題。
**解法：**
- **自動備援搜尋 (Automated Fallback)**：
    - 偵測到付費牆網域 (如 `bloomberg.com`) 時，自動觸發第二輪搜尋。
    - **黑名單邏輯 (Blacklist Logic)**：不使用白名單，而是排除已知付費牆，廣泛接受 `yahoo.com`, `reuters.com`, `apnews.com`, `gmanetwork.com` 等開放來源。
    - **關鍵字放寬**：搜尋時移除 `-site:` 限制，改用 `"{Title}" news` 模糊比對，增加命中率。
- **連結優先權 (Link Priority)**：
    - 在排序與篩選階段，給予非付費牆來源額外權重 (Bonus Score)，優先展示可直接閱讀的連結。
**keywords：** paywall-fallback, open-access, blacklist-logic, brave-search, accessibility, bloomberg-alternative

## 🔧 Cross-Source Synthesis (跨來源資訊揉合)
**日期：** 2026-02-12
**技能：** blogwatcher
**情境：** 避免多個主流媒體（如 Bloomberg, Reuters, FT）對同一事件（如 USMCA）的報導造成報告內容重複，並提供多維度觀點。
**解法：**
- **智能聚類 (Semantic Clustering)**：
    - 使用 `difflib.SequenceMatcher` 或關鍵字重疊率 (>0.4) 將相似標題的新聞歸類為一組。
- **自動摘要與觀點對照 (Synthesis Prompt)**：
    - 針對聚類後的新聞群組，使用 LLM 生成包含「主線新聞 (Main Story)」與「觀點差異 (Viewpoint Contrast)」的綜合報告。
    - 提示詞架構：`Synthesize these N reports into a single Main Story... and list contrasting viewpoints`.
- **完整溯源 (Consolidated Citations)**：
    - 在綜合報告末尾列出所有原始來源，並使用 `extract_media` 顯示具體媒體名稱（如 REUTERS, BLOOMBERG），而非通用標籤。
**keywords：** cross-source-synthesis, semantic-clustering, viewpoint-contrast, consolidated-citations, deduplication

## 🔧 BlogWatcher v5.0: Pure Brave Strategic Edition (智庫級進化)
**日期：** 2026-02-12
**技能：** blogwatcher
**情境：** 解決 BlogWatcher RSS 來源雜訊過多、HTML 結構干擾導致 AI 幻覺，以及個人 Blog 戰略價值下降的問題。
**解法：**
- **純化架構 (Pure Search Strategy)**：
    - **完全捨棄 RSS**：移除對 BlogWatcher CLI (RSS) 的依賴，解決所有因非標準 HTML 結構造成的 AI 記憶混淆與來源誤判。
    - **強勢白名單 (Authoritative Whitelist)**：監測範圍縮減至 30+ 門全球頂尖權威媒體（如 FT, WSJ, Bloomberg, Nikkei Asia, The Economist）。
- **幻覺防禦機制 (Hallucination Prevention)**：
    - **上下文錨定 (Context Anchoring)**：在翻譯與評析階段，強制 AI 同時讀取標題與內容描述。解決了過去因資訊不足導致 AI 根據熱門標籤自行腦補（如將英國新聞寫成中國新聞）的問題。
    - **排除關鍵字 (Exclusion Keywords)**：在配置中加入 `exclusion_keywords`，自動過濾社群網路爭議、仇恨言論審查等非戰略相關噪音。
- **智庫級語義整合 (Advanced Synthesis)**：
    - **雙重清洗層**：導入二次清洗邏輯，確保即使是綜合報導中的細項，也經過標題與描述的二次校驗。
    - **術語標準化**：修正翻譯層，確保 `ASEAN/東盟/亞細安` 統一譯為台灣慣用的 `東協`。
- **維護性優化**：
    - **全動態路徑**：全腳本移除硬編碼路徑，自動適配不同使用者的 Home 目錄與 iCloud 結構。
- **檔案策略**：
    - 暫停使用 `REPORT_PARADIGM.md` 直到系統穩定生成至少 3 份高品質報告。
**關鍵檔案/路徑：**
- `daily_report_generator.py`
- `monitoring_settings.json` (新增 `exclusion_keywords`)
- `sent_urls.json` (新增媒體來源緩存)
**keywords：** pure-brave, strategic-monitoring, whitelist-only, anti-hallucination, traditional-chinese-taiwan, context-anchoring, exclusion-filter
