# 拾作審美練習 (GitHub Pages 前端)

這個資料夾是審美練習網站的前端，放在 GitHub Pages 上，資料還是存在 Google 試算表「拾作審美練習資料庫」，透過 Apps Script 網頁應用程式的 JSON API 讀寫，跟瀏覽器登了幾個 Google 帳號無關

## 檔案
- index.html:整個網站 (今日、歷史、我的審美三頁)，由上一層的 build_pages.py 從 Index.html 產生，不要直接改這份
- .nojekyll:讓 GitHub Pages 原樣輸出檔案，不經過 Jekyll
- README.md:這份說明

## 怎麼開
- 第一次在一台裝置開，要用帶金鑰的網址:`https://<帳號>.github.io/<repo>/?k=<金鑰>`
- 開過一次後，金鑰會記在那台裝置的瀏覽器 (localStorage)，之後不帶 ?k= 也能開
- 金鑰不在任何檔案裡，只在網址和你的瀏覽器裡，所以 repo 公開也讀不到資料

## API (Apps Script 那一端)
- 讀資料:GET `<API_URL>?action=getData&k=<金鑰>`，回 `{"ok":true,"data":{items,responses,taste,serverTime}}` 或 `{"ok":false,"error":"..."}`
- 備援:同一個網址加 `&callback=函式名` 會回 JSONP
- 存回覆:POST `<API_URL>`，Content-Type `text/plain` (避免 CORS 預檢)，內容 `{"action":"saveResponse","k":"<金鑰>","payload":{"id","score","choice","guess","reason"}}`
- API_URL 寫在 index.html 最上面的 `var API_URL=`，換部署網址時改 build_pages.py 再重跑

## 常見狀況
- 顯示「這台裝置還沒有金鑰」:用帶 ?k= 的網址開一次
- 顯示「金鑰不正確」:金鑰換過了，用新的帶 ?k= 網址開一次
- 顯示「連不上伺服器」:Apps Script 還是舊版 (沒有 action API)，或部署權限不是「所有人」
