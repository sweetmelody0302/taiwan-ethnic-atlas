# 台灣族群分布圖鑑 — 靜態部署包

## ✅ 已上線

**<https://sweetmelody0302.github.io/taiwan-ethnic-atlas/>**

- 平台：GitHub Pages（repo：`sweetmelody0302/taiwan-ethnic-atlas`，Public）
- 來源：`main` 分支 / 根目錄
- HTTPS：已強制啟用
- 線上驗證：**74 項斷言全部通過**（`node verify.js https://sweetmelody0302.github.io/taiwan-ethnic-atlas/`）

這是一份**純靜態網站**：只有 `index.html` 一個檔案（176 KB，零外部相依、離線可用）。
不需要 build、不需要 Node、不需要資料庫。

| 檔案 | 用途 |
|---|---|
| `index.html` | 網站本體（唯一必需的檔案） |
| `404.html` | 同內容，讓不存在的路徑也有正常頁面 |
| `.nojekyll` | 避免 GitHub Pages 用 Jekyll 處理 |
| `CNAME` | （尚未建立）綁自訂網域用，內容為網域一行 |

---

## 之後要更新內容

```bash
cd "C:\Users\frank\WorkBuddy AI\2026-10-05-20-03-42\taiwan-ethnic-atlas"
python build.py                       # 從 src/ 重新打包 index.html
cp index.html deploy/index.html
cp index.html deploy/404.html
cd deploy && git add -A && git commit -m "update" && git push
```

推上去後 GitHub 會自動重新建置，約 1 分鐘生效。

---

## 綁自訂網域（還沒做）

1. 在 `deploy/` 放一個 `CNAME` 檔，內容只有你的網域一行（例如 `atlas.example.com`），推上去
2. 到你的 DNS 服務商加記錄：

| 類型 | 名稱 | 值 |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `sweetmelody0302.github.io` |

3. DNS 生效（5–30 分鐘）後，在 repo 的 **Settings → Pages** 勾 **Enforce HTTPS**

> 或者用 API 一次做完（`bash gh_api.sh POST /repos/<owner>/<repo>/pages '{"cname":"你的網域",...}'`）。

---

## 其他部署選項（備案）

### Netlify Drop（最快，60 秒）
1. 開 <https://app.netlify.com/drop>
2. 把這個資料夾**整個拖進去** → 立刻拿到 `xxx.netlify.app`
3. 綁網域：**Site configuration → Domain management → Add a domain**

### Cloudflare Pages（網域 DNS 在 Cloudflare 時最順）
1. <https://dash.cloudflare.com> → **Workers & Pages** → **Create** → **Pages** → **Upload assets**
2. 拖入這個資料夾 → **Deploy** → 得到 `xxx.pages.dev`
3. **Custom domains** → **Set up a custom domain** → 填網域

### Zeabur
**Add Service** → 選 GitHub repo → 類型 **Static** → **Domain** 分頁綁網域
