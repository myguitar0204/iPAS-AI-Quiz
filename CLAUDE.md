# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 執行與預覽

此專案無建置步驟，`index.html` 是唯一的應用程式檔案。

```powershell
# 本機預覽（必須用 HTTP server，不能直接雙擊開啟，Playwright 封鎖 file://）
cd C:\myguitar_claude\AI_Quiz_Bank
python -m http.server 8080
# 開啟 http://localhost:8080
```

## 架構

**單一檔案應用**：所有 HTML / CSS / JavaScript 內嵌於 `index.html`。沒有框架、沒有打包工具、沒有 node_modules。

外部依賴只有兩個（均為 CDN）：
- `cdn.jsdelivr.net/npm/chart.js` — 雷達圖與折線圖
- `generativelanguage.googleapis.com` — Gemini AI（使用者自備 Key）

### JavaScript 分區結構

`index.html` 的 JS 依功能分為以下區塊（以註解 `// ====` 分隔）：

| 區塊 | 主要內容 |
|------|---------|
| 雲端設定與資料初始化 | `CLOUD_API_URL`、`defaultQuizData`、從 localStorage 載入六種資料 |
| 作答統計計數器 | `userStats`、`checkDateReset()`、`updateAnswerStatsUI()` |
| 倒數時鐘與雲端同步 | `startExamCountdown()`、`syncToCloud()`、`syncFromCloud()`、`forceSyncFromCloud()` |
| 測驗與遊戲邏輯 | `startQuiz()`、`loadQuestion()`、`checkAnswer()`、`showResult()` |
| 互動操作與視窗綁定 | 所有 `addEventListener` / `.onclick` 綁定 |
| AI 自動出題與審核 | `btnGenerateWithAI`、`renderAIReviewList()` |
| 匯出 PDF / 列印 | `printQuestions()` |
| 學習儀表板 | `renderAnalyticsCharts()`（Chart.js） |

### 資料層

所有持久化資料存於 `localStorage`：

| Key | 說明 |
|-----|------|
| `customQuizData` | 自訂題庫（JSON 陣列） |
| `officialQuizData` | 官方考古題（以屆次為 key 的物件） |
| `wrongAnswerHistory` | 弱點題庫 |
| `favoriteQuestions` | 我的最愛 |
| `quizHistory` | 測驗分數紀錄 |
| `userStats` | 總作答數、本日作答數、最後作答日期 |
| `geminiApiKey` | Gemini API 金鑰 |
| `cloudApiUrl` | GAS 執行網址（空字串 = 關閉雲端同步）|

### 雲端同步邏輯重點

`CLOUD_API_URL` 從 `localStorage.getItem('cloudApiUrl')` 讀取，空字串時 `syncToCloud()` 與 `syncFromCloud()` 均直接 return，不發出任何請求。

合併策略：**取筆數較多的那份**（除 `quizHistory` 是雙向合併去重，`userStats` 是逐欄取最大值）。這代表刪除操作不會同步到其他裝置。

## 常見修改點

**新增考試屆次**：需同時修改 HTML 中兩處 `<select>` 的 `<option>`：
- `#quizOfficialSession`（官方考古題測驗選擇視窗）
- `#importOfficialSession`（官方題庫管理視窗）

**修改考試倒數目標日期**：JS 區塊「倒數時鐘」中的 `new Date('2026-05-16T00:00:00')`，共出現 **2 處**（`startExamCountdown()` 與 `showResult()`）。

**題目格式**：`answer` 欄位必須與 `options` 陣列中的某個字串**完全相同**，`checkAnswer()` 以字串相等判斷答對。
