# PickEat 專題說明

## 1. 專案名稱

PickEat

## 2. 專案簡介

PickEat 是一個「今天吃什麼推薦網站」。使用者可以選擇地點、價格區間、距離，並輸入今天想吃什麼，網站會推薦適合的餐廳，幫助有選擇困難的人快速決定一餐。

## 3. MVP 是什麼

MVP 是 Minimum Viable Product，也就是「最小可行產品」。它不是完整正式版，而是先做出可以操作、可以展示核心概念的第一版。

PickEat 的第一版 MVP 目標是讓老師、同學與組員可以在瀏覽器中看到核心流程：輸入需求、篩選條件、取得推薦結果、點擊地圖或導航按鈕。後續已擴充成前端正式版體驗，加入 GPS 定位、收藏與歷史紀錄。正式版功能狀態保留在備註文件中說明，不顯示在操作頁面上。目前也已建立 Node.js 後端，用來保護 Google Places API Key；前端會優先透過後端取得真實店家資料，失敗時再退回示範資料。

## 4. 第一版 MVP 已完成的功能

- React + Vite + JavaScript 前端專案。
- 搜尋根據地：可使用瀏覽器 GPS 定位，或選擇台灣縣市後拖曳圖釘設定搜尋中心。
- 使用者 GPS 定位：可呼叫瀏覽器定位，未授權時保留彰化市測試推薦。
- 價格區間篩選：可能百元內、平價約 100～200 元、中等約 200～300 元、中高約 300～400 元、偏高約 400～500 元、高價 500 元以上。
- 距離篩選：1 公里內、2 公里內、5 公里內、不限。
- 需求輸入：支援熱湯、便宜、一個人、不油、清爽、聚餐、宵夜等簡單關鍵字。
- 快速需求選單：分成情境需求、餐點類型、用餐場景，可從下拉選單加入需求標籤。
- 推薦結果卡片：顯示餐廳名稱、價格區間、距離、評分、地址、營業狀態、推薦亮點與中文關鍵字。
- 扭蛋隨機抽模式：用動畫從符合條件的餐廳中抽出一間，適合展示「選擇困難」情境。
- 收藏餐廳功能：使用 localStorage 保存收藏清單，重新整理後仍會保留。
- 推薦歷史紀錄：使用 localStorage 保存最近 5 次推薦與扭蛋結果，可清除紀錄。
- Google Maps 搜尋 URL 與導航 URL。
- 正式版功能狀態備註：在文件中標示已實現功能與需後端/API 的功能。
- Node.js + Express 後端：提供 `/api/health`、`/api/restaurants/search`、`/api/places/nearby`，並用 `server/.env` 保存 Google Places API Key。
- 前端已接上後端：一般推薦與扭蛋隨機抽會優先使用 Google Places API，API 失敗時自動使用示範資料。

## 5. 最終版目標

正式版希望可以使用 Google Places API 搜尋真實餐廳，搭配使用者 GPS 位置、距離、價格區間、需求文字與 AI 推薦排序，最後讓使用者可以查看地圖並開始導航。

## 6. 假資料說明

- 目前餐廳資料由 AI 生成。
- 測試地區為彰化市。
- 所有店家皆為虛構店家。
- 不代表真實 Google Maps 店家。
- 虛構資料只用於專題 MVP 展示，避免誤導使用者以為是真實店家。

## 7. 為什麼第一版先使用 AI 生成假資料

第一版目標是先驗證網站核心流程與畫面，不需要一開始就處理 API 金鑰、費用、錯誤處理、後端代理、資料格式轉換等問題。假資料可以讓專題先快速完成可展示版本。

## 8. 為什麼第一版先不接 Google Places API

Google Places API 需要申請 API Key、設定帳單、限制來源與處理正式資料格式。第一版先用假資料完成流程，未來再把資料來源替換成 API 回傳資料。

## 9. 為什麼第一版先不接 Google Maps JavaScript API

目前需求只需要跳轉到 Google Maps 查看地點與導航，因此使用 Google Maps URL 即可。只有未來要在網頁中直接顯示互動式地圖時，才需要加入 Google Maps JavaScript API。

## 10. 為什麼第一版先不接 AI API

AI API Key 不應該放在 React 前端，否則可能被使用者看到並濫用。正式版應該透過後端呼叫 OpenAI API。第一版先用簡單關鍵字推薦邏輯，保留未來替換成 AI 推薦的空間。

## 11. Google Places API、Google Maps URL、Google Maps JavaScript API 的差別

- Google Places API：用來搜尋真實店家資料，例如店名、地址、評分、營業狀態、類型與價格等級。
- Google Maps URL：用來產生可點擊的地圖搜尋或導航連結，不需要在前端載入地圖。
- Google Maps JavaScript API：用來在網頁中顯示互動式地圖，例如標記店家、拖曳地圖、顯示路線。

## 12. 未來如何串接 Google Places API 取得真實店家資料

未來可以新增後端 API，由前端把使用者位置、距離、需求送到後端。後端使用 Google Places API 搜尋附近餐廳，再把資料整理成目前前端需要的格式。

目前已新增 `server/` 後端資料夾，前端的 `handleRecommend` 已改成呼叫：

```txt
GET http://127.0.0.1:8787/api/restaurants/search?lat=使用者緯度&lng=使用者經度&radius=距離公尺&q=使用者需求
```

後端會呼叫 Google Places API，並把資料整理成目前 `RestaurantCard` 可使用的格式。

## 13. 未來如何使用 Google Maps URL 做查看地圖與導航

目前 `src/services/mapService.js` 已經集中處理 Google Maps URL：

- `createSearchUrl(query)`：產生查看地圖連結。
- `createDirectionsUrl(destination)`：產生導航連結。

未來取得真實店家資料後，只要把真實店名、地址或 Place ID 放進 query，就可以沿用這個設計。

## 14. 未來如何取得使用者 GPS 定位

目前「定位我的位置」按鈕已經使用瀏覽器 Geolocation API。正式串接 Google Places API 後，可將經緯度送到後端查詢附近餐廳：

```js
navigator.geolocation.getCurrentPosition(successCallback, errorCallback);
```

取得使用者經緯度後，再送到後端查詢附近餐廳。若使用者拒絕授權，系統會保留彰化市示範資料推薦。

## 15. 未來如何導入 AI 分析需求、排序餐廳、產生推薦理由

PickEat 未來導入 AI 的目的不是取代 Google Places API，而是負責理解使用者需求、協助排序餐廳，以及產生自然的推薦理由。

AI 未來主要負責：

- 解析使用者輸入的自然語言需求。
- 根據 Google Places API 回傳的真實餐廳資料進行推薦排序。
- 產生推薦理由，讓使用者知道為什麼 PickEat 推薦這間餐廳。

未來 AI 流程：

使用者輸入需求
→ 前端送到後端
→ 後端呼叫 Google Places API 取得附近真實餐廳
→ 後端呼叫 OpenAI API 解析需求與排序餐廳
→ 回傳推薦結果與推薦理由給前端
→ 前端顯示推薦卡片與導航按鈕

OpenAI API Key 不應該放在 React 前端，正式版應該透過後端呼叫 OpenAI API，避免 API Key 暴露。

## 16. 未來如何部署上線

前端可以部署到 Vercel、Netlify 或 GitHub Pages。若未來加入 Google Places API 與 AI API，建議同時建立後端服務，並把 API Key 放在後端環境變數中。

## 17. 使用方式

1. 選擇價格區間。
2. 選擇距離。
3. 輸入今天想吃的需求，或從快速需求選單加入標籤，例如「熱湯」、「雞肉飯」、「朋友聚餐」。
4. 按下「幫我推薦」。
5. 如果還是選不出來，可以按「扭蛋隨機抽」讓系統抽出一間餐廳。
6. 看到喜歡的餐廳可以按「收藏」，並在「我的收藏」區塊查看。
7. 到「推薦歷史紀錄」查看最近推薦或清除紀錄。
8. 查看推薦餐廳卡片。
9. 點擊「查看地圖」或「開始導航」展示正式版導航流程。

## 18. 建立或修改了哪些檔案

- `package.json`
- `package-lock.json`
- `.gitignore`
- `vite.config.js`
- `index.html`
- `README.md`
- `PROJECT_NOTE.md`
- `src/main.jsx`
- `src/App.jsx`
- `src/App.css`
- `src/data/restaurants.js`
- `src/services/mapService.js`
- `src/services/placeApiService.js`
- `src/services/priceService.js`
- `src/services/recommendationService.js`
- `src/components/SearchPanel.jsx`
- `src/components/GachaMachine.jsx`
- `src/components/FavoriteList.jsx`
- `src/components/HistoryList.jsx`
- `src/components/RestaurantCard.jsx`
- `server/package.json`
- `server/package-lock.json`
- `server/.env.example`
- `server/index.js`
- `server/services/googlePlacesService.js`
- `server/services/priceService.js`

## 19. 每個檔案的用途

- `package.json`：專案設定、套件與 npm scripts。
- `package-lock.json`：鎖定 npm 套件版本，讓組員安裝時版本一致。
- `.gitignore`：排除 `node_modules`、`dist`、環境變數等不適合提交的檔案。
- `vite.config.js`：Vite 與 React plugin 設定。
- `index.html`：Vite 入口 HTML。
- `README.md`：快速介紹、安裝與啟動方式。
- `PROJECT_NOTE.md`：專題說明與未來擴充規劃。
- `src/main.jsx`：React 掛載入口。
- `src/App.jsx`：整合首頁、搜尋狀態、推薦結果與未來功能區。
- `src/App.css`：整體視覺樣式與響應式設計。
- `src/data/restaurants.js`：彰化市風格虛構餐廳資料。
- `src/services/mapService.js`：Google Maps 搜尋與導航 URL 產生邏輯。
- `src/services/placeApiService.js`：前端呼叫後端 `/api/restaurants/search`，取得 Google Places 真實餐廳資料。
- `src/services/priceService.js`：把 Google Places 的價格等級、餐廳類型與關鍵字轉成 PickEat 的價格區間分類。
- `src/services/recommendationService.js`：MVP 版推薦邏輯。
- `src/components/SearchPanel.jsx`：搜尋與篩選表單。
- `src/components/GachaMachine.jsx`：扭蛋隨機抽 UI 與動畫狀態。
- `src/components/FavoriteList.jsx`：收藏餐廳清單。
- `src/components/HistoryList.jsx`：推薦歷史紀錄與清除功能。
- `src/components/RestaurantCard.jsx`：推薦餐廳卡片。
- `server/package.json`：後端套件與啟動 scripts。
- `server/.env.example`：後端環境變數範例，不含真實 API Key。
- `server/index.js`：Express 後端入口與 API 路由。
- `server/services/googlePlacesService.js`：呼叫 Google Places API 並轉換餐廳資料格式。
- `server/services/priceService.js`：後端價格區間分類邏輯，讓 Google Places 回傳資料先整理成前端可顯示的中文價格區間。

## 20. 如何啟動專案

```bash
cd pickeat
npm install
npm run server:install
npm run dev
```

啟動後端：

```bash
npm run server
```

第一次使用真實 Google Places API 前，請先建立 `server/.env`：

```bash
GOOGLE_PLACES_API_KEY=你的_google_places_api_key
```

## 21. 下一步可以擴充的功能

- 串接 Google Places API。
- 將前端推薦流程改成呼叫後端 `/api/restaurants/search`。
- 導入 AI 自然語言分析與推薦排序，並同樣透過後端保護 OpenAI API Key。
- 收藏分類、備註或帳號同步。
- 顯示更完整的餐廳詳細資料。
- 部署上線。

## 22. 適合放在專題報告中的說明文字

PickEat 是一個以 MVP 概念逐步擴充的學生專題網站。目前版本已完成前端正式版體驗，包含需求篩選、扭蛋隨機抽、瀏覽器 GPS 定位、收藏餐廳、推薦歷史紀錄，以及 Google Maps 查看地圖與導航連結。此版本仍使用 AI 生成的彰化市虛構餐廳資料，不會誤導為真實店家。未來若串接 Google Places API 與後端 AI 推薦，PickEat 就能取得真實店家資料、即時營業狀態，並根據使用者需求產生更精準的排序與推薦理由。
