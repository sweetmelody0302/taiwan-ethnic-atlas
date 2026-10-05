# 台灣族群分布圖鑑 — 靜態部署包

這是一份**純靜態網站**：只有 `index.html` 一個檔案（175 KB，零外部相依、離線可用）。
不需要 build、不需要 Node、不需要資料庫。任何靜態主機都能直接放。

| 檔案 | 用途 |
|---|---|
| `index.html` | 網站本體（唯一必需的檔案） |
| `404.html` | 同內容，讓不存在的路徑也有正常頁面（Netlify / GitHub Pages 會自動使用） |
| `.nojekyll` | 給 GitHub Pages 用，避免 Jekyll 多做處理 |

**只有 `index.html` 是必要的。** 專案其他檔案（`tw.json`、`*.py`、`verify.js` 等）都是開發工具，不用上傳。

---

## 選項 A：Netlify Drop（最快，60 秒、不用先設定任何東西）

1. 開 <https://app.netlify.com/drop>
2. 把 `deploy` 資料夾**整個拖進去**
3. 立刻拿到一個 `xxx.netlify.app` 網址

綁自己的網域：**Site configuration → Domain management → Add a domain**，依指示加 DNS 記錄，SSL 自動簽發。

## 選項 B：Cloudflare Pages（若你的網域 DNS 在 Cloudflare，最順）

1. <https://dash.cloudflare.com> → 左側 **Workers & Pages** → **Create** → **Pages** → **Upload assets**
2. 專案名稱填 `taiwan-ethnic-atlas` → 拖入 `deploy` 資料夾 → **Deploy**
3. 得到 `xxx.pages.dev` 後 → **Custom domains** → **Set up a custom domain** → 填你的網域
4. 網域 DNS 在 Cloudflare 就一鍵完成；在別家就到該家 DNS 加一筆 **CNAME** 指向 `xxx.pages.dev`

## 選項 C：GitHub Pages（用你的 sweetmelody0302 帳號）

**你必須自己執行推送** —— 我這邊的執行環境被設定了 `GIT_TERMINAL_PROMPT=0`，無法輸入憑證。

開 **PowerShell**，逐行貼上（把 `<repo>` 換成你要的專案名稱）：

```
cd "C:\Users\frank\WorkBuddy AI\2026-10-05-20-03-42\taiwan-ethnic-atlas\deploy"
git init -b main
git add -A
git commit -m "台灣族群分布圖鑑"
git remote add origin https://github.com/sweetmelody0302/<repo>.git
git push -u origin main
```

> 先在 GitHub 網頁上 **New repository** 建一個空 repo（**不要**勾 Add README / .gitignore）。
> 推送時若跳出 GCM 登入視窗，選 **Sign in with your browser** 即可（你機器上已設定 `credential.helper=manager`）。

推完後：repo → **Settings** → **Pages** → Source 選 `Deploy from a branch`、Branch 選 `main` / `(root)` → Save。
約 1 分鐘後網址：`https://sweetmelody0302.github.io/<repo>/`

綁自己的網域：同一頁 **Custom domain** 填網域，然後到你的 DNS 加：

| 類型 | 名稱 | 值 |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `sweetmelody0302.github.io` |

等 DNS 生效後勾 **Enforce HTTPS**。

## 選項 D：Zeabur

1. 把 `deploy` 內容推上 GitHub（或直接用 Zeabur 的上傳功能）
2. Zeabur 專案內 **Add Service** → 選該 repo → 類型選 **Static**
3. 到 **Domain** 分頁綁你的網域，依指示加 DNS 記錄

---

## 之後要更新內容

只要重新覆蓋 `index.html` 再重新部署一次即可：

- Netlify / Cloudflare Pages（拖曳上傳）：再拖一次資料夾
- GitHub Pages：換掉檔案後 `git add -A && git commit -m update && git push`
