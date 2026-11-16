# 敘事集 Story Atlas — GitHub 版

繁體中文故事筆記整理網站，純 HTML/CSS/JavaScript。無須後端或安裝套件。AI 功能由使用者輸入自己的 Gemini API 金鑰。

## 檔案用途
- dist/：編輯用網站來源（index.html、app.js、ai.js）。
- docs/：由 dist 產生的 GitHub Pages 發布內容。
- AGENTS.md / CLAUDE.md：網站開發指引，不是網站程式，兩份內容相同。
- tests/：39 項 Node 原生測試。
- prepare-pages.mjs：只將網站檔案複製至 docs，避免發布開發文件。

## 先決定開發文件是否公開
如果儲存庫是 Public，別人可以從 GitHub 讀取根目錄的 AGENTS.md / CLAUDE.md，即使網站沒有入口。希望只有自己知道時，完整專案應上傳到 Private 儲存庫。

GitHub Free 的 Pages 支援公開儲存庫；私人儲存庫的 Pages 取決於付費方案。私人儲存庫不等於私人網頁；本版本不含 ChatGPT 登入保護。

官方說明：
https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

## 方法 A：帳號可使用私人儲存庫 Pages
1. 解壓縮。登入 GitHub，建立 story-atlas 儲存庫，選 Private 以保密開發文件。
2. 上傳 story-atlas 資料夾「裡面」的檔案和資料夾，不是只上傳 ZIP。儲存庫根目錄應直接看得到 README.md、AGENTS.md、dist/ 和 docs/。
3. Settings → Pages → Build and deployment → Source：選 Deploy from a branch。
4. Branch 選 main、資料夾選 /docs，按 Save。
5. 等待建置完成，開啟 Settings → Pages 顯示的實際網址。原始碼頁不是網站網址。

## 方法 B：GitHub Free，開發文件保持私人
1. 完整專案上傳到 Private 儲存庫，作開發交接與備份。
2. 另建 Public 的 story-atlas-web 儲存庫。
3. 只把 docs/index.html、docs/app.js、docs/ai.js 複製到該公開儲存庫根目錄。不要上傳 AGENTS.md、CLAUDE.md 或完整專案 ZIP。
4. 公開儲存庫 Settings → Pages → Deploy from a branch → main → /(root) → Save。
5. 等待 Pages 網址出現，再開啟使用。程式碼會公開，故事筆記仍由各使用者瀏覽器保存。

## 其他靜態主機
可上傳 dist/ 內容到支援 HTML/JS 的主機；無建置指令，發布目錄為 dist。不要發布整個專案根目錄。原有 Sites 網址不會因本次打包被關閉。

## 本機預覽與更新
不要直接雙擊 HTML；ES module 應由靜態伺服器載入。

    python3 -m http.server 8000 --directory dist

開啟 http://localhost:8000 。修改 dist 後執行：

    node --test tests/*.test.mjs
    node prepare-pages.mjs

再提交來源與 docs/ 更新；方法 B 的公開網站儲存庫也需同步三個網站檔案。

## AI、筆記與搬家
- 在網頁填自己的 Gemini API 金鑰，不要放進程式碼、GitHub Secrets、README 或開發文件。
- 金鑰只保留在頁面記憶體；筆記原文會傳送給 Google，可能產生 API 費用。
- 預設 gemini-3.8-flash；模型可用性、速度與配額依 Google 帳號而定。
- 筆記保存在同一來源的瀏覽器 localStorage，沒有雲端同步。
- 搬到新網址前，在舊站匯出 JSON 備份，於新站匯入。不同網址不會自動帶入筆記。
- 本包不含作者筆記、金鑰、瀏覽器資料、Git 歷史或 Sites 身分資訊。

## 驗證範圍
39 項自動化測試通過，並檢查 Pages 子路徑及發布檔案。不代表已建立你的 GitHub 儲存庫或完成 Pages 發布；真實 API 仍需用自己的金鑰測試。
