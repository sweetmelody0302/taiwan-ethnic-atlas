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

## 選項 C：GitHub Pages ← 已選定，只差最後一步

這個資料夾**已經是 git repo**（`main` 分支、commit 已完成），remote 也設好了：

```
origin  https://github.com/sweetmelody0302/taiwan-ethnic-atlas.git
```

### 你只需要做 1 件事：建立空的 repo

1. 開這個連結：<https://github.com/new?name=taiwan-ethnic-atlas>
2. **Name 已自動填好** `taiwan-ethnic-atlas`，確認 **Public** 有選到
3. ⚠️ **不要**勾 Add a README / Add .gitignore / Choose a license —— 勾了會造成推送衝突
4. 按 **Create repository**

### 然後跟我說一聲「好了」，我幫你 push

你的 git 憑證我這邊可以直接用（已實測讀取 `liff-app` 成功），所以推送我可以代勞。

> 想自己推的話，開終端機貼這兩行也可以：
> ```
> cd "C:\Users\frank\WorkBuddy AI\2026-10-05-20-03-42\taiwan-ethnic-atlas\deploy"
> git push -u origin main
> ```
> 應該看到 `branch 'main' set up to track 'origin/main'` 和一段上傳進度。

### 開啟 Pages

推完後：repo → **Settings** → 左側 **Pages** → Source 選 `Deploy from a branch`、
Branch 選 **`main`** / 資料夾選 **`/(root)`** → **Save**。

約 1 分鐘後網址是：

```
https://sweetmelody0302.github.io/taiwan-ethnic-atlas/
```

### 綁自己的網域

在 Pages 同一頁的 **Custom domain** 填入你的網域 → Save。
然後到你的 DNS 服務商加這些記錄：

| 類型 | 名稱 | 值 |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `sweetmelody0302.github.io` |

DNS 生效（通常 5–30 分鐘）後，回 Pages 頁面勾 **Enforce HTTPS**。

> 也可以在這個資料夾放一個檔名為 `CNAME` 的檔案（內容只有網域一行），
> push 上去後 GitHub 會自動套用 —— 告訴我網域，我幫你加。

## 選項 D：Zeabur（備案）

1. 把 `deploy` 內容推上 GitHub（或直接用 Zeabur 的上傳功能）
2. Zeabur 專案內 **Add Service** → 選該 repo → 類型選 **Static**
3. 到 **Domain** 分頁綁你的網域，依指示加 DNS 記錄

---

## 之後要更新內容

只要重新覆蓋 `index.html` 再重新部署一次即可：

- Netlify / Cloudflare Pages（拖曳上傳）：再拖一次資料夾
- GitHub Pages：換掉檔案後 `git add -A && git commit -m update && git push`
