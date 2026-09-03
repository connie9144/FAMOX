# XPORTS 親子體能賽全功能系統 (2026)

本專案為 XPORTS 親子體能賽之前端報名、對帳查詢與公司端管理後台系統，採 HTML5 / Tailwind CSS / Vanilla JS 靜態架構，可直接部署於 GitHub Pages。

## 系統架構與功能

1. **客戶端線上報名**：支援 1-6 組階梯式團報計價，動態限制梯次容量（每梯上限 5 組）。
2. **參賽編號與對帳查詢**：輸入家長電話或姓名，可即時查詢審核狀態與分配號碼。
3. **公司端後台管理**：
   - **驗證密碼**：`XPORTS-52359844`
   - **核對發號**：自動依照組別與梯次生成參賽編號（格式：`幼幼組1梯1號`）。
   - **報表匯出**：支援 UTF-8 BOM 格式 CSV 匯出（防 Excel 簡體或亂碼）。

## 雲端資料庫設定 (Firebase Firestore)

本系統內建 Firebase 雲端資料庫串接（Project ID: `famox-ab3d0`）。若須開啟後台跨裝置同步，請至 [Firebase Console](https://console.firebase.google.com/) 將 Firestore 安全性規則（Security Rules）配置如下：

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /orders/{document} {
      allow read, write: if true;
    }
  }
}