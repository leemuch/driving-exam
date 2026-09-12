# 任務：把這個 app 上架到 GitHub Pages

## 這是什麼
`index.html` 是一個台灣駕照筆試練習 app（機車+汽車），單一 HTML 檔、純前端、無外部相依、完全離線可用。目標是部署到 GitHub Pages，取得一個公開網址可以分享。

## 請幫我完成以下步驟

### 前提檢查
- 確認本機已安裝 `git` 和 `gh`（GitHub CLI）。若沒有 `gh`，請提示我安裝：`brew install gh`（Mac）。
- 確認我已登入 GitHub CLI。若未登入，請執行 `gh auth login` 並引導我完成。

### 部署步驟
1. 在這個資料夾初始化 git repository（若尚未初始化）：
   ```bash
   git init
   git add index.html CLAUDE.md
   git commit -m "駕照筆試練習 app"
   ```

2. 用 gh 建立一個新的**公開** repository 並推送。repo 名稱建議 `driving-exam`（若已被占用，換一個名字）：
   ```bash
   gh repo create driving-exam --public --source=. --push
   ```

3. 開啟 GitHub Pages（從 main 分支的根目錄部署）：
   ```bash
   gh api -X POST repos/{owner}/driving-exam/pages -f "source[branch]=main" -f "source[path]=/" 2>/dev/null || \
   gh api -X PUT repos/{owner}/driving-exam/pages -f "source[branch]=main" -f "source[path]=/"
   ```
   （若 API 方式失敗，請改用瀏覽器手動開啟：repo → Settings → Pages → Branch 選 main、資料夾選 / (root) → Save，並告訴我怎麼操作。）

4. 取得並回報最終網址給我。網址格式為：
   `https://<我的GitHub帳號>.github.io/driving-exam/`
   Pages 首次啟用後約需 1-2 分鐘才會生效，請提醒我稍等後再開啟。

### 完成後
- 把最終公開網址清楚地告訴我。
- 提醒我：之後要更新內容，只要覆蓋 `index.html` 再 `git add . && git commit -m "更新" && git push`，網站會自動更新。

## 注意事項
- 這個 app 用瀏覽器 localStorage 儲存錯題本，是正常的前端行為，不需要後端。
- 不要修改 index.html 的內容（題庫和邏輯都已完成並驗證過）。
- repo 必須是 public，GitHub Pages 免費版才能用。
