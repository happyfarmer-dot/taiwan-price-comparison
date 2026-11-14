# 台灣產品即時差價與單位價錢系統

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/happyfarmer-dot/taiwan-price-comparison/blob/main/colab/update_taiwan_prices.ipynb)

- **線上網頁（GitHub Pages）**：<https://happyfarmer-dot.github.io/taiwan-price-comparison/>
- **Colab 自動抓價／分析筆記本**：[`colab/update_taiwan_prices.ipynb`](https://colab.research.google.com/github/happyfarmer-dot/taiwan-price-comparison/blob/main/colab/update_taiwan_prices.ipynb)
- **即時價格資料檔**：[`data/prices.json`](data/prices.json)

## 系統架構（Google Colab ＋ GitHub Pages）

1. **Google Colab 算力層**（[`colab/update_taiwan_prices.ipynb`](colab/update_taiwan_prices.ipynb)）：
   - 載入 `data/prices.json` 並使用 Pandas 整理所有品牌、規格與單位價。
   - 嘗試透過公開搜尋 API（如 PChome 24h）抓最新報價並更新歷史低點 `histLow`（具異常降級保護）。
   - 提供表單式通路調價與實體 vs 網購價差 Matplotlib 圖表分析。
   - 產出最新 `data/prices.json`，支援在 Colab 設定 `GITHUB_TOKEN` Secret 後一鍵推送回 GitHub 自動更新網頁。
2. **靜態前端網站層**（[`index.html`](index.html)）：
   - 自動讀取 `./data/prices.json` 顯示最新價格與最後更新來源（若於本機離線開啟則自動降級使用內建資料）。
   - **查詢產品直接依價錢順序排列**：優先顯示 `【品牌】完整商品名稱 ＋ 規格`，並將「🏪 實體門市品項」與「🛒 網路電商品項」分開呈現。
   - **歷史低價燈號提示**：`🟢 近期低點・值得買`、`🟡 常態均價`、`🔴 偏貴・建議等特價`。
   - **實體店來回路程成本折算**：支援機車 / 開車油資 / 含時間成本折算重新排序。
   - **購物籃同店一次買齊比較**：比較「分開去各家買」與「同一家店一次買齊」的淨價差與來回路程成本。
   - **超商／超市惜食雷達 ＆ 促銷計算機 ＆ 深淺色切換**。
