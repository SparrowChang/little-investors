# Little Investors — Max & Lawrence

適合兩位孩子使用的「美股模擬投資」單頁網站，可直接使用 GitHub Pages 免費部署。

## 中文 / English 雙語切換

網站右上角有 **中文 / English** 切換按鈕，所有主要頁面、交易流程、錯誤提示、投資日記與設定都會切換。語言選擇會和投資紀錄一起保存在同一個瀏覽器。**切換語言不會變更交易或日記內容**（孩子輸入的筆記會保持原文）。

## 功能

- **Max 和 Lawrence 獨立帳本**：每人各有 $10,000 虛擬現金。
- **最多 5 支美股**：自選股票代號加入觀察清單（watchlist）。
- **模擬買賣**：支援小數股、現金與持倉檢查、理由記錄及最後一筆撤銷。沒有任何真實交易。
- **歷史走勢**：個股及投資組合 1D / 1W / 1M / 1Y / MAX。個股 MAX 是資料供應商可取得的歷史；投資組合 MAX 以第一筆模擬交易起算。
- **投資日記**、買賣紀錄。
- **存檔**：此瀏覽器 localStorage 自動儲存；設定頁有 JSON 匯出、匯入，避免資料遺失。
- **行情模式**：直接使用的「示範行情」與需 API key 的「市場資料」有獨立帳本。示範行情完全是生成數據，不是實際股價。
- **手機與電腦響應式介面**。

## 部署到 GitHub Pages（約幾個步驟）

1. 在 GitHub 登入，按 **New repository**，取名 `little-investors`，設成 Public。
2. 在 repository 頁面按 **Add file → Upload files**，上傳 `index.html`，Commit changes。
3. 在 **Settings → Pages → Build and deployment**，Source 選 `Deploy from a branch`，Branch 選 `main` / `/(root)`，Save。
4. 等 GitHub 部署後前往：`https://你的GitHub帳號.github.io/little-investors/`。
5. 首次打開即是「示範行情」，不用 API key 就能完整試用互動操作。

> 網頁是純靜態頁面，不能自動同步 Max 和 Lawrence 在不同瀏覽器／不同裝置的紀錄。可使用 JSON 備份搬移。要真正跨裝置同步，需要之後接 Firebase / Supabase 及登入與資料庫權限。

## 真實行情選擇性設定

1. 前往 [Twelve Data](https://twelvedata.com/) 註冊自己的帳號並取得 API key。
2. 開啟網站右上角「設定 / 備份」，貼上 key 並按「儲存金鑰」。
3. 按「切換市場資料」。新增股票後可查參考報價與歷史線圖。
4. 這個免費 API 有速率／點數和歷史資料限制，受支援範圍影響；若 API 顯示錯誤或等待，請稍後更新。不同股票的資料與延遲程度依供應商方案，非保證即時。
5. **請不要把自己的 API key 寫在 index.html 然後提交到公開 GitHub**。網站只從瀏覽器設定頁讀取 key。瀏覽器儲存不是伺服器級的秘密金鑰保護；使用者的裝置或瀏覽器擴充套件可能讀到它。如果要完全隱藏 key，日後需要另外架後端。

## 重要說明

- 預設本金 $10,000，純虛擬；不是券商交易帳戶。
- 買賣用畫面當下參考價格模擬成交，不包含交易成本、稅、滑價、股息或配股、拆股對歷史模擬部位的校正。因此總資產的歷史報酬**僅供理財教育參考，不是精確可交易績效**。
- 當市場模式資料無法取得時，畫面會顯示錯誤，不會偷偷改用示範數據。
- 貼進網站的觀察筆記和交易理由存於本機；使用私人、可信任的瀏覽器裝置。
- 本工具不構成投資建議。

## 本地開啟

將 `index.html` 雙擊以瀏覽器開啟，示範行情可立即使用。如瀏覽器禁止 file:// localStorage，改用 Python 本地伺服器：

```bash
python -m http.server 8000
```

接著開啟 `http://localhost:8000/`。

## 原始碼

不需要 build 或安裝前端套件；HTML、CSS 和 JavaScript 全在 `index.html` 裡，方便修改和部署。


---

## English — Little Investors (Max & Lawrence)

A bilingual (Traditional Chinese + English), free, interactive stock-investing practice site for two kids. **No real trading.**

- Each child gets a separate $10,000 **virtual** portfolio and a watchlist of up to **five U.S. stocks**.
- Practice fractional-share buys/sells, track trades and investments, keep a journal, undo the last trade, and explore **1D / 1W / 1M / 1Y / MAX** charts.
- Click **中文 / English** in the top-right corner to change the interface instantly. Language selection is saved in the browser; stock choices, trade history and journal text are preserved.
- Includes clearly labeled **synthetic demo prices**. Optionally enter your own Twelve Data API key to use market data in a separate practice ledger. Real price availability may be limited or delayed.
- Records are saved **locally in the current browser**, not in GitHub or a cloud database. Export/import the JSON backup in **Settings / Backup** to transfer data to another device.

### GitHub Pages quick setup

1. Create a public GitHub repository named `little-investors`.
2. Upload the included **`index.html`** file to the repository root.
3. Go to **Settings → Pages → Deploy from a branch → main / (root) → Save**.
4. Open `https://YOUR-USERNAME.github.io/little-investors/` once GitHub finishes publishing.
5. Later updates: replace `index.html` with the newest bilingual version and commit. **Existing locally saved portfolios remain available** if you keep the same website URL, browser and origin and do not clear browser storage.

**Security:** Do not paste the market-data API key into publicly committed code. Using the website’s browser-only key storage is more private than committing a key, but still exposes the key to this browser, its extensions and anyone with access to the device. This tool is for education, not financial advice.
