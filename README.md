# PickEat

PickEat 是一個學生專題網站，主題是「今天吃什麼推薦網站」。目前版本已完成前端正式版體驗，使用彰化市風格的示範餐廳資料，展示使用者依照地點、價格區間、距離與需求快速取得餐廳推薦的核心概念。
目前已加入 Node.js 後端，前端會優先透過後端呼叫 Google Places API 取得真實店家；若後端或 API 暫時不可用，會自動退回示範資料。

## 安裝方式

```bash
cd pickeat
npm install
npm run server:install
```

## 啟動方式

前端：

```bash
npm run dev
```

啟動後依照終端機顯示的網址開啟瀏覽器，通常會是 `http://localhost:5173/`。

後端：

```bash
npm run server
```

後端會啟動在 `http://127.0.0.1:8787`。

## 後端與 API Key 設定

1. 複製 `server/.env.example`，建立 `server/.env`。
2. 在 `server/.env` 填入自己的 Google Places API Key：

```bash
GOOGLE_PLACES_API_KEY=你的_api_key
```

3. 啟動後端：

```bash
npm run server
```

4. 測試後端是否正常：

```bash
curl http://127.0.0.1:8787/api/health
```

目前已建立的後端 API：

- `GET /api/health`：檢查後端是否啟動，以及是否讀到 Google Places API Key。
- `GET /api/restaurants/search?lat=24.0758&lng=120.5440&radius=2000&q=火鍋`：搜尋真實餐廳資料。
- `GET /api/places/nearby?lat=24.0758&lng=120.5440&radius=2000`：搜尋附近餐廳。

API Key 只放在 `server/.env`，不要放進 React 前端，也不要上傳到 GitHub。

## 使用技術

- React
- Vite
- JavaScript
- CSS
- Node.js
- Express
- Google Maps URL 連結格式
- localStorage
- Browser Geolocation API

## 目前功能

- 可使用瀏覽器 GPS 定位，或選擇台灣縣市後拖曳圖釘設定搜尋中心。
- 可使用瀏覽器 GPS 定位，未授權時仍以彰化市測試資料推薦。
- 可選擇價格區間：可能百元內、平價約 100～200 元、中等約 200～300 元、中高約 300～400 元、偏高約 400～500 元、高價 500 元以上。
- 可選擇距離：1 公里內、2 公里內、5 公里內、不限。
- 可輸入需求文字，例如熱湯、便宜、一個人、清爽、聚餐。
- 可使用分組快速需求選單，加入情境需求、餐點類型、用餐場景標籤。
- 優先透過後端呼叫 Google Places API 搜尋真實餐廳。
- 如果後端或 Google Places API 無法使用，會自動退回 AI 生成示範餐廳資料。
- 示範資料模式會依照價格區間、距離與需求關鍵字推薦餐廳。
- 提供扭蛋隨機抽模式，用動畫抽出一間符合條件的餐廳。
- 可收藏餐廳，收藏清單會保存在瀏覽器 localStorage。
- 可記錄最近 5 次推薦與扭蛋抽選歷史，並可清除紀錄。
- 顯示餐廳名稱、價格區間、距離、評分、地址、營業狀態、推薦亮點與中文關鍵字。
- 提供「查看地圖」與「開始導航」按鈕。
- 正式版功能狀態改放在專案備註文件中說明，頁面維持使用者操作體驗。

## 注意事項

- 前端已接上後端 Google Places API 代理層。
- 示範餐廳資料仍作為 API 失敗時的備援資料。
- 尚未串接 AI API。
- 店家資料皆為虛構，不代表真實 Google Maps 店家。
- Google Maps 按鈕目前只用 URL 跳轉展示，因為是假資料，可能找不到真正店家。
- 收藏與歷史紀錄目前只存在使用者自己的瀏覽器，不會同步到其他裝置。

## 未來規劃

- 優化 Google Places API 回傳資料的排序與欄位顯示。
- 顯示真實營業狀態、評分、地址與價格區間。
- 透過後端導入 AI API，解析自然語言需求、排序餐廳並產生推薦理由。
- 加入帳號系統、收藏同步與歷史紀錄。
- 部署到 Vercel、Netlify 或 GitHub Pages，讓老師、同學與組員可以直接使用。
