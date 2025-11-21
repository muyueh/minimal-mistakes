# 在 GitHub Pages 上啟用 Decap CMS

這個範例設定讓 Minimal Mistakes 部落格可以透過 Decap CMS (原 Netlify CMS) 管理 `_posts` 文章。完成下列步驟後，即可在 `https://<你的網域>/admin/` 進入後台。

## 1. 設定 GitHub OAuth App

Decap CMS 的 GitHub 後端需要 OAuth 流程才能在瀏覽器取得存取權杖。

1. 到 GitHub 建立 **OAuth App**，Authorization callback URL 建議填入 `https://<你的網域>/admin/`。
2. 取得 `Client ID`，並產生一組 `Client Secret`。
3. 若不想自架 OAuth 代理，可使用公開的 `auth_type: implicit` 流程，記得在 `admin/config.yml` 填入 `app_id`（也就是 Client ID）。
4. 如果你使用自架或託管的 OAuth 代理服務，把網址填入 `base_url`。

> 參考文件：<https://decapcms.org/docs/intro/>

## 2. 更新 CMS 後端設定

編輯 [`admin/config.yml`](../admin/config.yml) 並填入自己的 GitHub Pages 資訊：

- `repo`: 你的 GitHub repo，例如 `username/username.github.io` 或 `username/blog`。
- `branch`: 儲存文章的預設分支，通常是 `main` 或 `master`，若你在其他分支（如 `work`）維護內容就填該分支。
- `site_domain`: 部落格網域（例如 `username.github.io` 或自訂網域）。
- `app_id`: 在上一步取得的 GitHub OAuth App Client ID。
- 若使用自架或託管的 OAuth 代理，把 `base_url` 解除註解並改成代理網址。例如採用公開的 `decap-cms-oauth-server` 託管服務時，可設定 `base_url: https://decap-cms-oauth-server.onrender.com`。

如果想在本機端測試 CMS，可以保持 `local_backend: true`，並啟動 Jekyll 伺服器後執行 `npx decap-server`：

```bash
bundle exec jekyll serve
npx decap-server
```

## 3. 上傳路徑與預設欄位

- 檔案上傳會存放在 `assets/uploads/`，網站上以 `/assets/uploads/` 提供靜態檔案。
- 新文章預設 `layout: single`，且支援分類、標籤、摘要與 Markdown 內文欄位。欄位可依需求在 `admin/config.yml` 中調整。

完成設定後推送到 GitHub，稍待 GitHub Pages 重新部署，就能透過 `/admin/` 管理文章。

## GitHub Pages 會有什麼限制嗎？

不會。Decap CMS 只需要能提供靜態檔案、並透過瀏覽器呼叫 GitHub API 寫入內容，GitHub Pages 天生符合這兩點。但有幾個細節要留意：

- GitHub Pages 只提供前端頁面，無法保管機密金鑰，因此 `admin/config.yml` 需要使用 `auth_type: implicit` 或 OAuth 代理（`base_url`）。
- 建議站點使用 HTTPS 網域（`https://username.github.io` 或自訂網域），並把同樣的網址填入 OAuth callback URL 與 `site_domain`。
- 如果你的 repo 是公開的，預設設定即可；若是私有 repo，還是需要透過 OAuth 正常授權後才能寫入內容。

只要完成上面的 OAuth 設定，GitHub Pages 本身不需要額外的伺服器或外掛，就能正常運作 CMS。
