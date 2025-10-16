# 最小專案部署流程指南

## 概述
本指南提供建立最小網頁專案並部署到 GitHub + Vercel 的完整流程，適用於任何 AI agent 精準複製。

## 前置需求
- Git 已安裝
- GitHub 帳號
- Vercel 帳號（可選，也可透過 GitHub 自動部署）

## 步驟 1：建立專案目錄結構

```bash
# 建立專案目錄
mkdir -p mo-test
cd mo-test
```

## 步驟 2：建立核心檔案

### 2.1 建立 index.html
```bash
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World App</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        
        .container {
            text-align: center;
            background: white;
            padding: 3rem 2rem;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            color: #333;
            margin-bottom: 2rem;
            font-size: 2rem;
        }
        
        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 1rem 2rem;
            font-size: 1.2rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 15px 30px rgba(102, 126, 234, 0.4);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .message {
            margin-top: 2rem;
            font-size: 1.5rem;
            color: #667eea;
            font-weight: bold;
            opacity: 0;
            transition: opacity 0.5s ease;
        }
        
        .message.show {
            opacity: 1;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hello World App</h1>
        <button class="btn" onclick="showHello()">點我說 Hello World!</button>
        <div id="message" class="message"></div>
    </div>

    <script>
        function showHello() {
            const messageEl = document.getElementById('message');
            messageEl.textContent = 'Hello World! 🌍';
            messageEl.classList.add('show');
            
            // 添加一些動畫效果
            setTimeout(() => {
                messageEl.style.transform = 'scale(1.1)';
                setTimeout(() => {
                    messageEl.style.transform = 'scale(1)';
                }, 200);
            }, 100);
        }
    </script>
</body>
</html>
EOF
```

### 2.2 建立 package.json
```bash
cat > package.json << 'EOF'
{
  "name": "mo-test",
  "version": "1.0.0",
  "description": "A simple Hello World web application",
  "main": "index.html",
  "scripts": {
    "start": "python3 -m http.server 8000",
    "dev": "python3 -m http.server 8000"
  },
  "keywords": [
    "hello-world",
    "web",
    "simple"
  ],
  "author": "dreamsprouts",
  "license": "MIT",
  "repository": {
    "type": "git",
    "url": "https://github.com/dreamsprouts/mo-test.git"
  },
  "homepage": "https://mo-test.vercel.app"
}
EOF
```

### 2.3 建立 vercel.json
```bash
cat > vercel.json << 'EOF'
{
  "version": 2,
  "builds": [
    {
      "src": "index.html",
      "use": "@vercel/static"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/index.html"
    }
  ]
}
EOF
```

### 2.4 建立 README.md
```bash
cat > README.md << 'EOF'
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
EOF
```

## 步驟 3：Git 初始化和提交

```bash
# 初始化 Git 倉庫
git init

# 添加所有檔案
git add .

# 提交變更
git commit -m "Initial commit: Hello World app"

# 設定主分支為 main
git branch -M main
```

## 步驟 4：推送到 GitHub

```bash
# 添加遠端倉庫（替換為你的 GitHub 倉庫 URL）
git remote add origin https://github.com/dreamsprouts/mo-test.git

# 推送到 GitHub
git push -u origin main
```

## 步驟 5：Vercel 部署

### 方法 A：透過 Vercel 網站
1. 前往 https://vercel.com
2. 使用 GitHub 帳號登入
3. 點擊 "New Project"
4. 選擇 `dreamsprouts/mo-test` 倉庫
5. 點擊 "Deploy"（Vercel 會自動偵測設定）

### 方法 B：使用 Vercel CLI
```bash
# 安裝 Vercel CLI
npm i -g vercel

# 部署到 Vercel
vercel --prod
```

## 驗證部署

部署完成後，你可以：
1. 檢查 GitHub 倉庫：https://github.com/dreamsprouts/mo-test
2. 訪問 Vercel 部署的網址（通常在 Vercel 控制台顯示）
3. 測試按鈕功能是否正常

## 檔案結構

```
mo-test/
├── index.html      # 主要網頁檔案
├── package.json    # 專案配置
├── vercel.json     # Vercel 部署配置
├── README.md       # 專案說明
└── .git/          # Git 倉庫
```

## 重要注意事項

1. **GitHub 倉庫 URL**：記得替換為你的實際 GitHub 倉庫 URL
2. **專案名稱**：可以修改 `package.json` 中的 `name` 欄位
3. **Vercel 設定**：`vercel.json` 確保正確的靜態檔案部署
4. **分支名稱**：使用 `main` 作為預設分支（符合 GitHub 新標準）

## 故障排除

### 常見問題

1. **Git 推送失敗**：檢查 GitHub 倉庫是否存在，URL 是否正確
2. **Vercel 部署失敗**：確認 `vercel.json` 配置正確
3. **本地測試**：使用 `python3 -m http.server 8000` 測試本地版本

### 檢查清單

- [ ] 所有檔案已建立
- [ ] Git 倉庫已初始化
- [ ] 檔案已提交到 Git
- [ ] 已推送到 GitHub
- [ ] Vercel 部署成功
- [ ] 網站功能正常

## 自動化腳本

可以將整個流程合併為一個腳本：

```bash
#!/bin/bash
# 建立最小專案並部署到 GitHub + Vercel

# 設定變數
PROJECT_NAME="mo-test"
GITHUB_URL="https://github.com/dreamsprouts/mo-test.git"

# 建立目錄
mkdir -p $PROJECT_NAME
cd $PROJECT_NAME

# 建立檔案（使用上述 cat 命令）
# ... 檔案建立代碼 ...

# Git 操作
git init
git add .
git commit -m "Initial commit: Hello World app"
git branch -M main
git remote add origin $GITHUB_URL
git push -u origin main

echo "專案已成功推送到 GitHub: $GITHUB_URL"
echo "現在可以前往 Vercel 進行部署"
```

這份指南確保任何 agent 都能精準複製整個部署流程。
