# 拾作審美練習 (GitHub Pages 前端)

這個資料夾是審美練習網站的前端，放在 GitHub Pages 上，資料存在 Google 試算表「拾作審美練習資料庫」，透過 Apps Script 網頁應用程式的 JSON API 讀寫

## 檔案 (repo 根目錄對應)
- index.html:整個網站 (今日、歷史、我的審美)，由上一層的 build_v5.py 從 app_v5.html 產生，不要直接改這份
- clips/:每題一支 8 秒無聲並排小影片 (.mp4) 和封面 (.jpg)，檔名是題號小寫，例如 q-2026-11-19-1.mp4
- .nojekyll:讓 GitHub Pages 原樣輸出檔案
- README.md:這份說明

## 怎麼開
- 第一次在一台裝置開，要用帶金鑰的網址 `https://qaz3508845.github.io/aesthetic/?k=<金鑰>`，之後金鑰記在那台裝置 (localStorage)，不帶 ?k= 也能開
- 金鑰不在任何檔案裡，repo 公開也讀不到資料 (影片本身是公開的，只是示意小片)

## API
- 讀:GET `<API_URL>?action=getData5&k=<金鑰>`，備援 `&callback=` JSONP
- 存選擇:POST text/plain `{"action":"saveChoice","k","payload":{"qid","choice","comment","seconds"}}`
- 收進指南:POST text/plain `{"action":"acceptRule","k","payload":{"rid","action","week"}}`

## 常見狀況
- 「這台裝置還沒有金鑰」:用帶 ?k= 的網址開一次
- 「讀不到資料 · 不支援的動作:getData5」:Apps Script 還是 v4，要部署 v5
- 影片黑掉:clips/ 資料夾沒傳上去，或檔名大小寫不對
