## 🛡️ Social Media Sentinel: 跨領域 X 帳號戰略監測規範
**日期：** 2026-02-14
**技能：** social-sentinel
**情境：** 針對 AI Tech, Digital Sovereignty, Minimalism 三大領域的高價值 X 帳號進行系統化監測。
**解法：**
- **領域敏感度 (Domain Sensitivity)**：
    - **AI Tech**：側重於模型更新、論文解析與 AGI 路線討論。
    - **Digital Sovereignty**：側重於內容變現模型、一人公司系統化與個人品牌美學。
    - **Minimalism**：側重於意圖性生活、數位清空與美學減法。
- **繼承戰略規格 (Inherited Strategic Standards)**：
    - 必須引用的參考：`skill-thinktank.md` (原 `skill-blogwatcher.md`)。
    - **連結處理**：對貼文中出現的 URL 執行自動網域過濾，且優先展示非付費牆新聞。
    - **翻譯風格**：統一採用高品質繁體中文，術語需經台灣在地化處理（如「東協」、「軟體」）。
- **報導式摘要 (Narrative Synthesis)**：
    - 禁止單純的條列貼文；必須進行現象級的歸納。
    - 結構必須包含：【戰略總結】、【領域動態細節】、【Data Log】。
- **視覺同步 (Visual Synergy)**：
    - 報告中建議搭配 `concept_viz` (OpenAI Style) 來視覺化複雜的思維框架或產業影響力地圖。
- **執行經驗與最佳化 (Execution Insights & Optimization)**：
    - **Obsidian 重複路徑修復**：避免在腳本中重複拼接 `note_2026`（例如 `OBSIDIAN_ROOT` 包含 `note_2026` 而 `config` 也包含時），應統一基準點為 `~/Documents`。
    - **Brave Search 語法**：若抓不到動態，可簡化 query 為 `site:x.com {handle}` 以擴大搜尋範圍。
    - **絕對路徑強制化**：在執行環境（如 cron）不穩定時，`BASE_PATH` 應使用絕對路徑以確保正確讀取 `sentinel_config.json`。
**關鍵檔案/路徑：**
- `.agent/workflows/social_sentinel.md`
- `skills/social-sentinel/sentinel_monitor.py`
- `Command_Templates.md` (新增 /social_sentinel)
**keywords：** social-sentinel, x-monitoring, strategic-synthesis, digital-sovereignty, minimalism, path-fix, absolute-path, brave-optimization
