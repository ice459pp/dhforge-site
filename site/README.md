# DSH Forge 公開產品資訊網站

這個目錄不是 DSH Web 的執行頁面，也不會由 `start.sh`／`start.bat` 提供。
它是 DSH Forge 對外發布時使用的**共用產品資訊與 OAuth 品牌網站來源**，內容包含：

- 應用程式首頁、共用 OAuth 連線原則與目前支援服務；
- Google API 資料使用與 Limited Use 聲明；
- 隱私權政策；
- 服務條款；
- Google OAuth 同意畫面使用的 120×120 品牌標誌。

## 共用政策頁原則

首頁、隱私權政策與服務條款是所有 OAuth 供應商的共用公開資訊，不應為 Gmail、Sheets、Notion、
Figma 或其他服務各複製一套頁面。新增供應商時應更新共用的「連線與服務」目錄，並在隱私權政策
加入該供應商的資料種類、用途、分享、保存與撤銷差異；只有供應商政策明確要求獨立頁面時才例外。

Google API Limited Use 聲明與 Workspace 八項權限表是目前的 Google 專屬附錄，不應被誤套用到
其他供應商，也不能因網站已列出某服務就宣稱產品已完成該服務的 OAuth 實作。

## 為什麼必須部署到外部公開網址

Google OAuth 正式發布與驗證需要任何使用者及審查人員都能在未登入 DSH 的情況下開啟首頁、
隱私權政策與服務條款。`127.0.0.1`、私人儲存庫內的檔案或只有開發者能存取的測試網站均不符合
這個目的。因此本目錄必須部署到公開 GitHub Pages、可公開存取的靜態網站服務，或日後由維護者
擁有並可驗證的正式網域。

## 目前部署拓撲

- **內容來源：** 本私人 `ice459pp/dhforge` 儲存庫的 `site/`；網站內容應與實際 Google API
  權限、資料處理及產品行為同步維護。
- **公開部署：** `ice459pp/dhforge-site` 公開儲存庫；GitHub Actions 只發布該儲存庫的
  `site/` artifact。
- **公開網址：** `https://ice459pp.github.io/dhforge-site/`
- **政策網址：** `https://ice459pp.github.io/dhforge-site/privacy/` 與
  `https://ice459pp.github.io/dhforge-site/terms/`

公開儲存庫是部署鏡像，不應加入 DSH 原始碼、測試輸出、OAuth Client Secret、access／refresh
token、authorization code、完整 callback URL 或任何使用者資料。變更產品能力或資料處理方式時，
先更新本目錄及相關插件契約，再同步公開部署副本；兩邊內容不得長期分歧。

## Google Cloud 品牌欄位

目前 GitHub Pages URL 可用於公開展示。Google 正式 OAuth 驗證仍可能要求維護者證明網域所有權；
若日後取得自有網域，應將同一份靜態網站綁定該網域，並同步更新：

1. 每頁的 canonical URL 與 404 頁絕對路徑；
2. Google Cloud Branding 的首頁、隱私權政策與服務條款 URL；
3. Authorized domains、正式 OAuth Client 的 redirect URI／origin（若適用）；
4. Search Console 網域驗證及公開頁面中的產品／資料處理描述。

## 品牌標誌

`assets/dsh-forge-google-oauth-logo.png` 沿用專案既有錘子 icon，固定為 120×120 PNG 且小於
1 MB，可直接上傳 Google Cloud 的 OAuth 品牌頁。若更換圖示，應同時更新網站 favicon、公開部署
副本與 Google Cloud 品牌設定，並重新檢查 Google 的驗證要求。

## 發布前檢查

1. 首頁、`privacy/`、`terms/` 與標誌均回傳 HTTP 200。
2. 導覽與相對連結可在 GitHub Project Pages 子路徑下使用。
3. 隱私權內容與目前憑證保存、AI 模型傳輸、對話歷史及刪除行為一致。
4. 沒有秘密、測試帳戶內容或私人識別資訊進入公開 artifact。
5. 公開部署完成後，再把正式 URL 填入 Google Cloud；不要使用尚未成功發布的預期網址。
