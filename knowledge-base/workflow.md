# 工作流程最佳實踐

此分類記錄工作流程和效率相關的經驗和最佳實踐。

---

## 🔧 戰略情報偵察工具組 (Strategic Reconnaissance Toolset)
**日期：** 2026-02-11
**情境：** 需要根據「資訊精準度」與「覆蓋廣度」的需求，選擇正確的檢索路徑。
**最佳實踐：**
1. **Antigravity Web_Search (廣度優先)**：
   - 適用：主題研究初探、非特定網域的背景調查。
   - 特點：覆蓋面廣但雜訊多，適合在 LLM 需要廣泛上下文時使用。
2. **Brave Search API + 戰略過濾 (精準優先)**：
   - 適用：每日特定產業監測 (如 AI、半導體)、追蹤關鍵地緣政策。
   - 特點：透過 `ALLOWED_DOMAINS` 與「路徑深度校驗」實現極高信噪比。
3. **BlogWatcher RSS (權威優先)**：
   - 適用：跟蹤特定專家分析 (Stratechery)、頂級媒體專欄 (FT Lex)。
   - 特點：100% 權威推送，零雜訊，適合長期深度戰略追蹤。
**混合工作法 (Mixed Workflow)**：優先使用「Brave + BlogWatcher」雙軌制進行每日監聽，若遇到未知新議題再調用「Web Search」進行擴張。

---

## 🔧 Obsidian 推播路徑偏好 (Obsidian Push Preference)
**日期：** 2026-02-13
**情境：** 當用戶指令包含「推播Obsidian」時，應統一將檔案推送到指定的 iCloud 路徑。
**最佳實踐：**
- **推播路徑**：`~/Library/Mobile Documents/iCloud~md~obsidian`
- **操作指南**：
  - 識別關鍵字：「推播Obsidian」、「推到Obsidian」、「Push to Obsidian」。
  - 檔案操作：確保檔案以 `.md` 格式寫入上述目錄或其子目錄。
  - **路徑動態化**：必須自動將 `~/` 解析為當前系統的 Home 目錄（如 `/Users/username/`），以確保跨機器相容性。
  - 路徑驗證：若該路徑不存在，請先嘗試確認 iCloud 文件夾掛載狀態。
