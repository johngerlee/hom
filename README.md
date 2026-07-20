# 成長星球集點簿（GitHub Pages + Firebase）

這是一個純前端網頁，可部署在 GitHub Pages；管理者使用 Firebase Authentication 的電子郵件與密碼登入，資料儲存在 Cloud Firestore。

## 功能

- 初始點數 3,702 點
- 管理者帳號密碼登入
- A～E 類優良表現快速集點
- 閱讀頁數自動換算
- 自訂集點類別、名稱、點數與「固定／每頁」計點方式
- 3C 時間兌換
- 雲端紀錄與跨裝置同步
- 復原上一筆紀錄
- 孩子名字與代表圖片設定

## 一、建立 Firebase 專案

1. 進入 Firebase Console，建立一個專案。
2. 新增「Web 應用程式」。
3. 複製 SDK 設定，貼到 `firebase-config.js`。
4. Authentication > Sign-in method，啟用「電子郵件／密碼」。
5. Authentication > Users，新增一組管理者電子郵件與密碼。
6. 複製該使用者的 UID。
7. 建立 Cloud Firestore 資料庫，建議選擇離台灣較近的區域。
8. 將 `firestore.rules` 中的 `REPLACE_WITH_ADMIN_UID` 改成管理者 UID，並發布規則。

## 二、部署到 GitHub Pages

1. 在 GitHub 建立新的 repository。
2. 上傳本資料夾內的 `index.html`、`firebase-config.js`。
3. Repository Settings > Pages。
4. Source 選擇 `Deploy from a branch`。
5. Branch 選 `main`，資料夾選 `/root`，按 Save。
6. 等待 GitHub 提供公開網址。

## 三、Firebase 授權網域

Firebase Authentication > Settings > Authorized domains：

- 加入 `你的帳號.github.io`
- 使用自訂網域時，也要加入該網域

## 安全注意事項

- 不要把管理者密碼寫入 HTML 或 JavaScript。
- `firebase-config.js` 不是密碼；資料安全依賴 Firestore Security Rules。
- 必須將規則中的 UID 改成真正管理者 UID，否則程式無法存取資料。
- 若要多人管理，可在 `isAdmin()` 內加入多個 UID。
