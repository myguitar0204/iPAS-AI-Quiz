 # 🎯 iPAS AI應用規劃師 刷題系統

  > 專為備考 **iPAS 人工智慧/生成式 AI 應用規劃師認證**打造的全功能刷題平台

  [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
  ![HTML](https://img.shields.io/badge/HTML-Single%20File-orange)
  ![Netlify](https://img.shields.io/badge/Deploy-Netlify-00C7B7)

  ## ✨ 功能特色

  | 模式 | 說明 |
  |------|------|
  | 😊 **正常模式** | 自訂題數，答完即看解答，無時間壓力 |
  | 🔥 **生存模式** | 30 秒倒數，答對 +3s，答錯 -5s |
  | 🎯 **弱點特訓** | 自動彙整歷史答錯題目，針對弱點練習 |
  | ❤️ **我的最愛** | 收藏重點題目，隨時複習 |
  | 🏆 **iPAS 模考模式** | 50 題 / 60 分鐘，模擬正式考試情境 |
  | 🎓 **歷屆官方考古題** | 依屆次與科目作答，原汁原味還原考題 |

  **其他功能：**
  - 🤖 **AI 導師解析** — 答錯時由 Gemini AI 即時講解錯誤觀念
  - ✨ **AI 自動出題** — 輸入關鍵字，讓 AI 生成符合 iPAS 格式的新題目
  - ☁️ **雲端同步** — 透過 Google Apps Script 跨裝置同步題庫與紀錄
  - 📊 **學習儀表板** — 五維能力雷達圖 + 歷次模考成績走勢圖
  - 🖨️ **列印錯題/最愛** — 一鍵匯出 PDF 考前精華整理

  ---

  ## 🚀 快速開始

  ### 方法一：直接使用（無需安裝）

  點擊下方連結即可使用：

  👉 **[線上版本](https://your-netlify-url.netlify.app)**

  ### 方法二：下載到本機

  ```bash
  git clone https://github.com/myguitar0204/iPAS-AI-Quiz.git
  cd iPAS-AI-Quiz
  # 用瀏覽器直接開啟 index.html，或啟動本機伺服器：
  python -m http.server 8080
  # 瀏覽器開啟 http://localhost:8080

  ---
  ⚙️ 設定說明

  1. Gemini API Key（啟用 AI 功能）

  AI 導師解析與自動出題功能需要 Gemini API Key：

  1. 前往 Google AI Studio (https://aistudio.google.com/app/apikey)
  2. 登入 Google 帳號 → 點擊「Create API Key」
  3. 開啟系統右下角「🤖 AI 導師設定」→ 貼入金鑰儲存

  ▎ 金鑰僅存於您自己的瀏覽器 localStorage，不會上傳至任何伺服器。

  2. 雲端同步（可選，跨裝置同步資料）

  若需要多裝置同步題庫與作答紀錄，需自行部署 Google Apps Script：

  1. 前往 Google Apps Script (https://script.google.com) 建立新專案
  2. 部署為「網頁應用程式」取得執行網址
  3. 開啟「🤖 AI 導師設定」→ 貼入 GAS 執行網址

  ▎ 不設定此項目，所有資料仍會正常儲存於本機。

  ---
  📥 匯入題庫

  題庫使用標準 JSON 格式，可自行擴充：

  [
    {
      "subject": "科目1：人工智慧基礎概論",
      "question": "題目內容",
      "options": ["選項A", "選項B", "選項C", "選項D"],
      "answer": "正確的選項文字"
    }
  ]

  點擊右下角「⚙️ 自訂題庫」→「📁 從本機選擇 JSON 檔案載入」即可匯入。

  ---
  🛠️ 技術架構

  - 前端：純 HTML / CSS / JavaScript，單一檔案，零框架相依
  - 圖表：Chart.js (https://www.chartjs.org/)
  - AI：Google Gemini 2.5 Flash Lite API
  - 雲端同步：Google Apps Script（需自行部署）
  - 部署：Netlify（靜態網頁，免費方案即可）

  ---
  📋 支援科目

  - 科目 1：人工智慧基礎概論
  - 科目 2：生成式 AI 應用與規劃

  ---
  🤝 貢獻

  歡迎提交 Issue 或 Pull Request！

  1. Fork 此 Repository
  2. 建立新分支 git checkout -b feature/你的功能
  3. Commit 更改 git commit -m 'feat: 新增功能說明'
  4. Push git push origin feature/你的功能
  5. 開啟 Pull Request

  ---
  📄 License

  MIT License — 自由使用、修改、散布，保留原始作者聲明即可。
