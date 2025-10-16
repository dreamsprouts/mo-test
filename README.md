# Hello World App

一個簡單的 Hello World 網頁應用程式。

## 功能

- 點擊按鈕顯示 "Hello World!" 訊息
- 響應式設計，支援各種裝置
- 美觀的漸層背景和動畫效果

## 本地開發

```bash
# 啟動本地伺服器
python3 -m http.server 8000

# 或使用 npm
npm start
```

然後在瀏覽器中開啟 `http://localhost:8000`

## 部署

### GitHub

1. 將專案推送到 GitHub：
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/dreamsprouts/mo-test.git
git push -u origin main
```

### Vercel

1. 連接到 Vercel 帳號
2. 選擇 GitHub 倉庫 `dreamsprouts/mo-test`
3. 自動部署完成

或使用 Vercel CLI：
```bash
npm i -g vercel
vercel --prod
```

## 技術規格

- 純 HTML/CSS/JavaScript
- 響應式設計
- 無需建置步驟
- 靜態檔案部署

## 授權

MIT License
