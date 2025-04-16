# ESG 新聞趨勢分析系統

此專案是一個自動化的 ESG（環境、社會、治理）新聞分析系統，用於從 ESG 新聞網站抓取最新標題，分析當前趨勢，並生成結構化的分析報告。

## 功能概述

- 自動從 [ESG News](https://esgnews.com/) 網站抓取最新新聞標題
- 提取並清理新聞標題
- 分析 ESG 趨勢（環境、社會、治理）
- 評估分析結果並提供反思
- 生成包含多角度影響分析的 Markdown 格式報告
- 自動保存報告到輸出目錄

## 系統架構

該系統使用 AutoGen 多智能體架構，包括以下專業代理：

1. **web_scraper_agent**：負責抓取 ESG 新聞網站的原始文本內容
2. **title_extractor_agent**：從原始文本中提取新聞標題
3. **analyst_agent**：分析新聞標題反映的 ESG 趨勢
4. **reflection_agent**：評估分析質量並提供反思輸入
5. **correction_agent**：在發現問題時協調修正過程
6. **draft_agent**：整合內容並生成報告草稿
7. **document_agent**：負責最終報告格式化和保存

## 環境需求

- Python 3.10 或更高版本
- Node.js (用於 MCP 服務器)
- 相關 Python 和 Node.js 套件

## 安裝指南

1. **創建並啟動虛擬環境**：

   ```bash
   # 使用 Anaconda 創建虛擬環境
   conda create -n esg_analyzer python=3.10
   conda activate esg_analyzer
   ```

2. **安裝 Python 依賴**：

   ```bash
   # 安裝必要的 Python 套件
   pip install autogen-agentchat autogen-ext autogen-core
   ```

3. **安裝必要的 Node.js 套件**：

   ```bash
   # 安裝 MCP 服務器相關套件
   npm install -g @modelcontextprotocol/server-filesystem
   ```

4. **將專案克隆到本地**：

   ```bash
   git clone <repository_url>
   cd <repository_directory>
   ```

## 使用方法

1. **配置路徑**：
   
   在 `esg_news_analyzer.py` 文件中，確認並調整以下路徑設置：
   
   - `fetch_mcp_server` 中的 `args` 路徑
   - `write_mcp_server` 中的 `args` 路徑，指向您的工作目錄

2. **確保 OpenAI API 設置**：
   
   確認您已經設置了 OPENAI_API_KEY。可以通過環境變數或專案設定檔設置。

3. **執行分析程序**：

   ```bash
   # 啟動虛擬環境
   conda activate esg_analyzer
   
   # 執行分析器
   python esg_news_analyzer.py
   ```

4. **檢視分析報告**：
   
   完成後，分析報告將保存在 `output` 目錄中，文件名格式為 `ESG_News_YYYY-MM-DD_HH-MM-SS.md`。

## 報告結構

生成的報告包含以下部分：

1. **新聞標題列表**：從網站提取的 10 條最新 ESG 新聞標題
2. **主要趨勢分析**：按 ESG 類別（環境、社會、治理）分類的趨勢分析
3. **趨勢影響分析**：從多角度分析趨勢影響
   - 對企業的影響
   - 對投資者的影響
   - 對消費者/社會的影響
   - 對從業者/監管機構的影響

## 自訂與配置

- **調整報告格式**：可以在 `draft_agent` 和 `document_agent` 的系統提示中修改報告結構。
- **擴展分析維度**：可以在 `analyst_agent` 的系統提示中添加新的分析維度。
- **更改資料來源**：可以在 `web_scraper_agent` 的系統提示中更改目標網站。

## 疑難排解

- **網頁抓取問題**：如果無法抓取網頁內容，請檢查目標網站是否可訪問，或嘗試調整 `fetch_txt` 工具的參數。
- **模型 API 錯誤**：確認您的 OPENAI_API_KEY 設置正確並且 API 使用額度充足。
- **輸出目錄錯誤**：確保 `output` 目錄存在且具有寫入權限。

## 注意事項

- 本系統僅用於分析公開發布的 ESG 新聞，請遵守相關網站的使用條款。
- API 使用會產生費用，請關注您的 OpenAI API 使用情況。 