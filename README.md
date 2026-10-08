# 字樹花園獨立介紹頁

字樹花園的獨立靜態介紹頁，建立於 2026-10-08。網站內容位於 `site/`，使用 GitHub Pages 發布。

[開啟介紹頁](https://wordtreegarden.com/)

使用 `Gavin0099/wordtreegarden-site` 作為獨立公開儲存庫。本資料夾位於現有專案旁邊，不會被現有練習網站的部署流程載入。

## 本機預覽

```powershell
Set-Location E:\BackUp\Git_EE\wordtreegarden-site
python -m http.server 8765 --bind 127.0.0.1 --directory site
```

開啟 `http://127.0.0.1:8765/`。頁面為 HTML/CSS 靜態頁，不需安裝套件或建置；FAQ 使用瀏覽器原生 details，沒有登入、追蹤程式或表單。

## 結構

- `site/`：唯一發布內容。含介紹頁、樣式與品牌素材。
- `.github/workflows/pages.yml`：手動執行的 GitHub Pages 工作流程，僅上傳 `site/`。
- `SETUP.md`：購買、網域驗證、DNS、HTTPS、轉寄與驗收步驟。
- `deployment/CNAME`：未啟用的網域名稱備稿。這個 Actions 發布方式以 Pages 設定中的 Custom domain 為準，CNAME 檔不能取代該設定。
- `deployment/dns-records.csv`：本次網站 DNS 設定參照表；不包含既有郵件與憑證記錄，不可用它整批取代 DNS。
- `artifacts/`：本機驗證與截圖，不包含在 Pages 上傳範圍。

## 正式網址與內容檢查

1. 本頁聯絡信箱為 `hello@wordtreegarden.com`，免費轉寄至 `reiko0099@gmail.com`。使用者於 2026-10-08 回報測試信已在 Gmail 垃圾信箱收到，兩個 mailto 連結已更新。
2. 網域已在 GitHub 個人帳號驗證，並綁定此獨立儲存庫；已開啟 Enforce HTTPS。
3. canonical 與 `og:url` 使用 `https://wordtreegarden.com/`。網站 DNS 使用根網域 ALIAS 與 `www` CNAME，均指向 `gavin0099.github.io`。
4. 沒有放置尚未確認的 App Store 或 TestFlight 下載連結。取得有效的公開連結並確認可用後再補。
5. 練習示意已明確標註，沒有將概念圖稱為 App 截圖。iOS 和網頁版的差異也已說明。
6. 隱私與支援直接連到既有網址，不改 App Store 上的既有連結。

## 素材與文案來源

品牌方向參考 `english-vocab-trainer/DESIGN.md`，年齡與起點參考該專案 README；聯絡與訪客資料說明參考已上線的支援頁。

`site/assets/tree.svg`、`sprout.svg`、`apple.svg` 和 `favicon.png` 複製自相鄰 `english-vocab-trainer/public/` 的既有品牌素材。SVG 的 JSX 屬性拼法已在複本改成標準 SVG 屬性，供靜態圖片渲染；來源檔未修改。

本頁沒有宣稱學習成效、正式程度認證、考試通過率或 App Store 上架狀態。
