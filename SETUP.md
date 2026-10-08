# wordtreegarden.com 購買與設定步驟

查核日期為 2026-10-08。這是購買、發布與網域設定操作手冊；各階段執行結果須依實際驗證判定。當次價格、續約價格與帳號權限需以實際畫面為準。

## 1. 購買與帳號

在 [Porkbun 網域搜尋](https://porkbun.com/) 查詢 `wordtreegarden.com`。若可購買，只選 `.com` 一年；確認首年總額、續約價格與自動續約設定，WHOIS 隱私已開，其他加購略過。完成帳號的雙重驗證，妥善保管復原碼。密碼、付款資料與驗證碼請直接在官方頁面輸入，不需要貼到聊天。

## 2. 先發布獨立網站

經使用者確認儲存庫名稱、公開可見性與發布後，才在 `Gavin0099` 下建立獨立的 `wordtreegarden-site`，上傳本資料夾中已確認的程式碼與文件。不要把這些檔案推到 `english-vocab-trainer`，也不要建立或更動 `Gavin0099.github.io` 帳號網站。

在新儲存庫 Settings → Pages → Build and deployment，把 Source 設為 GitHub Actions；到 Actions 手動執行 `Publish introduction site`。工作流程只發布 `site/`，不會發布 artifacts 或設定備稿。

先確認 `https://gavin0099.github.io/wordtreegarden-site/` 可以載入。此時不要設定自訂網域，也不要更改現有 `english-vocab-trainer` 的 Pages 設定。

官方來源：[設定 Pages 發布來源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

## 3. 在 GitHub 個人帳號驗證網域

購買完成後，進入 GitHub **個人帳號** Settings → Pages → Add a domain，輸入 `wordtreegarden.com`。這一步與儲存庫 Settings → Pages 的 Custom domain 是不同設定。

GitHub 會顯示需建立的 TXT 記錄。Porkbun DNS 的 Host 預期為 `_github-pages-challenge-Gavin0099`，但 Host 與 Answer 均以 GitHub 畫面實際給出的值為準，不猜驗證碼。

新增 TXT 後，確認公開 DNS 已生效，再回 GitHub 按 Verify。驗證成功後保留 TXT 記錄，不要移除。

官方來源：[驗證 GitHub Pages 自訂網域](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)。

## 4. 先綁定新網站，再修改網站 DNS

只在新儲存庫 `wordtreegarden-site` 的 Settings → Pages → Custom domain 填入 `wordtreegarden.com` 並儲存，接著才設定指向 GitHub 的 A/AAAA/CNAME。不要把網域綁在現有練習儲存庫，避免改變它的網址與隱私、支援入口。

本包使用 GitHub Actions 發布，GitHub 官方說明此模式不靠 CNAME 檔啟用網域。`deployment/CNAME` 只是名稱備稿，不能當成已綁定證據。

官方來源：[管理 GitHub Pages 自訂網域](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)。

## 5. Porkbun DNS 記錄

先記錄目前 DNS。移除與根網域或 `www` 衝突的網站停放 A、AAAA、CNAME 或 ALIAS 記錄；不要整批清空 DNS，也不要刪除郵件轉寄所需的 MX、郵件 TXT 或 GitHub 驗證 TXT。Porkbun 根網域 Host 留空；`@` 表示相同的根網域概念。

| Type | Host | Answer | 需求 |
| --- | --- | --- | --- |
| A | 空白（根網域） | 185.199.108.153 | 必要 |
| A | 空白（根網域） | 185.199.109.153 | 必要 |
| A | 空白（根網域） | 185.199.110.153 | 必要 |
| A | 空白（根網域） | 185.199.111.153 | 必要 |
| AAAA | 空白（根網域） | 2606:50c0:8000::153 | 可選 |
| AAAA | 空白（根網域） | 2606:50c0:8001::153 | 可選 |
| AAAA | 空白（根網域） | 2606:50c0:8002::153 | 可選 |
| AAAA | 空白（根網域） | 2606:50c0:8003::153 | 可選 |
| CNAME | www | Gavin0099.github.io | 必要 |
| TXT | GitHub 提供的驗證 Host | GitHub 畫面提供的實際值 | 必要並持續保留 |

`www` 的 Answer 只能是主機名稱，不加 `https://`、儲存庫名稱、斜線或 `*.pages.github.io`。不要新增 wildcard `*` 指向 GitHub。四個 A 記錄都保留；若加 IPv6，四個 AAAA 也一起加。DNS 傳播可能需要最多 24 小時。

官方來源：[GitHub 網域與 DNS](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)、[Porkbun DNS 管理](https://kb.porkbun.com/article/68-how-to-edit-dns-records)、[Porkbun 根網域 Host 留空](https://kb.porkbun.com/article/231-how-to-add-dns-records-on-porkbun)。

## 6. HTTPS 與 canonical

回到新儲存庫 Pages 確認 DNS check 通過，等待 HTTPS 憑證可用，再開啟 Enforce HTTPS。此選項可用也可能需最多 24 小時。

確認根網域載入正確介紹頁，`www` 自動導向 `https://wordtreegarden.com/`，再將 `site/index.html` 中 canonical 和 `og:url` 兩處由預計的 Pages 網址改為 `https://wordtreegarden.com/`，重新發布。

官方來源：[GitHub Pages HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)。

## 7. 免費信箱轉寄

Porkbun Domain Management → 網域右側 EMAIL 圖示 → Porkbun Email Forwarding。建立 `hello`，Destination 填你的 Gmail。避免改用付費 hosted email，除非另有明確需求。

使用與收件 Gmail **不同的信箱**，人工寄信到 `hello@wordtreegarden.com`，確認收件匣或垃圾信件中確實收到。公開 MX/TXT 查詢只能證明 DNS 狀態，不能證明信件送達。

免費轉寄提供收信；從 Gmail 回覆會顯示 Gmail 地址，不會自動以 `hello@wordtreegarden.com` 寄出。若未測試成功，介紹頁繼續使用既有 Gmail。成功後再替換兩個 `mailto:reiko0099@gmail.com`。

官方來源：[Porkbun 免費轉寄與測試](https://kb.porkbun.com/article/10-how-to-set-up-email-forwarding-service)。

## 8. 驗收

Windows 公開 DNS 檢查：

```powershell
Resolve-DnsName wordtreegarden.com -Type A -Server 1.1.1.1
Resolve-DnsName wordtreegarden.com -Type AAAA -Server 1.1.1.1
Resolve-DnsName www.wordtreegarden.com -Type CNAME -Server 1.1.1.1
Resolve-DnsName _github-pages-challenge-Gavin0099.wordtreegarden.com -Type TXT -Server 1.1.1.1
Resolve-DnsName wordtreegarden.com -Type MX -Server 1.1.1.1
```

未設定可選 AAAA 時，沒有 AAAA 回答是預期狀態。查詢結果須與實際設定比對，不能只看指令是否執行。

- [ ] 根網域使用 HTTPS 顯示字樹花園介紹頁，沒有憑證警告。
- [ ] `www` 的最終網址為 `https://wordtreegarden.com/`。
- [ ] 新網站手機版、FAQ、聯絡、隱私與支援連結可用。
- [ ] 原本 `https://gavin0099.github.io/english-vocab-trainer/` 仍顯示練習程式，沒有被導向介紹頁。
- [ ] 原本的 `privacy.html` 與 `support.html` 仍使用既有網址，沒有被導向新網域。
- [ ] 新儲存庫名稱、Custom domain、DNS check 和 Enforce HTTPS 設定皆記錄。
- [ ] GitHub 個人帳號的 Verified domain 狀態成功，TXT 持續保留。
- [ ] 不同寄件信箱的轉寄測試確實收到後，才更換聯絡信箱。

若網站 DNS 有問題，先核對新儲存庫的 Custom domain 與 DNS 快照，修正衝突記錄。不要透過改動舊練習儲存庫來排除新網站問題。
