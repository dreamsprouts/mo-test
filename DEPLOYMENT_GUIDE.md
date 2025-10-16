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
5. **設定環境變數**（如需要）：
   - 在 "Environment Variables" 區塊
   - 添加變數名稱和值
   - 選擇環境（Production, Preview, Development）
6. 點擊 "Deploy"（Vercel 會自動偵測設定）

### 方法 B：使用 Vercel CLI
```bash
# 安裝 Vercel CLI
npm i -g vercel

# 部署到 Vercel
vercel --prod
```

### 方法 C：使用 Vercel CLI 設定環境變數
```bash
# 設定環境變數
vercel env add VARIABLE_NAME

# 或批量設定
vercel env add API_URL
vercel env add DATABASE_URL
vercel env add SECRET_KEY

# 部署
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

## 環境變數設定

### 常見環境變數範例

```bash
# API 相關
API_URL=https://api.example.com
API_KEY=your_api_key_here

# 資料庫相關
DATABASE_URL=postgresql://user:password@host:port/database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp
DB_USER=username
DB_PASSWORD=password

# 第三方服務
STRIPE_SECRET_KEY=sk_test_...
STRIPE_PUBLISHABLE_KEY=pk_test_...
GOOGLE_ANALYTICS_ID=GA-XXXXXXXXX

# 應用設定
NODE_ENV=production
PORT=3000
JWT_SECRET=your_jwt_secret
```

### 環境變數檔案（.env.local）

```bash
# 建立本地環境變數檔案
cat > .env.local << 'EOF'
API_URL=https://api.example.com
API_KEY=your_api_key_here
DATABASE_URL=postgresql://user:password@host:port/database
NODE_ENV=development
EOF
```

### 測試階段：預設環境變數

對於測試階段，可以在專案中直接設定預設值，避免手動輸入：

```bash
# 建立 .env.example 檔案（可以提交到 Git）
cat > .env.example << 'EOF'
# 測試用環境變數範例
API_URL=https://jsonplaceholder.typicode.com
API_KEY=test_key_12345
DATABASE_URL=sqlite:///test.db
NODE_ENV=development
PORT=3000
EOF

# 建立 .env 檔案（測試用，可以提交）
cat > .env << 'EOF'
# 測試環境變數
API_URL=https://jsonplaceholder.typicode.com
API_KEY=test_key_12345
DATABASE_URL=sqlite:///test.db
NODE_ENV=development
PORT=3000
EOF
```

### 在程式碼中使用環境變數

```javascript
// 前端 JavaScript - 帶預設值
const apiUrl = process.env.API_URL || 'https://jsonplaceholder.typicode.com';
const apiKey = process.env.API_KEY || 'test_key_12345';

// 使用環境變數
fetch(`${apiUrl}/posts`, {
  headers: {
    'Authorization': `Bearer ${apiKey}`
  }
})
.then(response => response.json())
.then(data => console.log('API 資料:', data));
```

### 測試用 API 服務

```javascript
// 使用免費測試 API，無需真實金鑰
const testConfig = {
  apiUrl: 'https://jsonplaceholder.typicode.com',  // 免費測試 API
  apiKey: 'test_key_12345',                      // 測試用金鑰
  databaseUrl: 'sqlite:///test.db',              // 本地測試資料庫
  nodeEnv: 'development'
};

// 在程式碼中使用
const config = {
  apiUrl: process.env.API_URL || testConfig.apiUrl,
  apiKey: process.env.API_KEY || testConfig.apiKey,
  databaseUrl: process.env.DATABASE_URL || testConfig.databaseUrl,
  nodeEnv: process.env.NODE_ENV || testConfig.nodeEnv
};
```

## 重要注意事項

1. **GitHub 倉庫 URL**：記得替換為你的實際 GitHub 倉庫 URL
2. **專案名稱**：可以修改 `package.json` 中的 `name` 欄位
3. **Vercel 設定**：`vercel.json` 確保正確的靜態檔案部署
4. **分支名稱**：使用 `main` 作為預設分支（符合 GitHub 新標準）
5. **環境變數安全**：
   - 不要將敏感資訊提交到 Git
   - 使用 `.env.local` 進行本地開發
   - 在 Vercel 控制台設定生產環境變數
   - 敏感變數使用 Vercel 的加密存儲

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
- [ ] 環境變數已設定（如需要）
- [ ] Vercel 部署成功
- [ ] 網站功能正常
- [ ] 環境變數在生產環境中正常工作

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

# 建立 .env.local 範例檔案
cat > .env.local << 'EOF'
# 本地開發環境變數
API_URL=http://localhost:3000
API_KEY=your_local_api_key
NODE_ENV=development
EOF

# 建立 .gitignore 避免提交敏感資訊
cat > .gitignore << 'EOF'
# 敏感環境變數檔案
.env.local
.env.production

# 依賴
node_modules/

# 建置輸出
dist/
build/

# 日誌
*.log

# 系統檔案
.DS_Store
Thumbs.db
EOF

# Git 操作
git init
git add .
git commit -m "Initial commit: Hello World app"
git branch -M main
git remote add origin $GITHUB_URL
git push -u origin main

echo "專案已成功推送到 GitHub: $GITHUB_URL"
echo "現在可以前往 Vercel 進行部署"
echo "記得在 Vercel 控制台設定生產環境變數！"
```

## 環境變數最佳實踐

### 1. 測試階段：預設值部署
```bash
# 建立測試用 .env 檔案（可以提交到 Git）
cat > .env << 'EOF'
# 測試環境變數 - 可以直接推送到 GitHub
API_URL=https://jsonplaceholder.typicode.com
API_KEY=test_key_12345
DATABASE_URL=sqlite:///test.db
NODE_ENV=development
PORT=3000
EOF

# 推送到 GitHub，Vercel 會自動使用這些值
git add .env
git commit -m "Add test environment variables"
git push origin main
```

### 2. 生產階段：Vercel 控制台設定
```bash
# 生產環境才需要手動設定敏感資訊
# 前往 Vercel 控制台 > Project Settings > Environment Variables
# 設定真實的 API 金鑰和資料庫連線
```

### 3. 混合方式：程式碼預設值
```javascript
// 在程式碼中設定預設值，避免手動輸入
const config = {
  // 測試用預設值
  apiUrl: process.env.API_URL || 'https://jsonplaceholder.typicode.com',
  apiKey: process.env.API_KEY || 'test_key_12345',
  databaseUrl: process.env.DATABASE_URL || 'sqlite:///test.db',
  
  // 生產環境會覆蓋這些值
  isProduction: process.env.NODE_ENV === 'production'
};

// 使用配置
console.log('API URL:', config.apiUrl);
console.log('Environment:', config.isProduction ? 'Production' : 'Development');
```

### 4. 免費測試服務清單
```javascript
// 這些服務不需要真實金鑰，適合測試
const freeTestServices = {
  jsonPlaceholder: 'https://jsonplaceholder.typicode.com',  // 假資料 API
  reqres: 'https://reqres.in/api',                          // 測試 API
  httpbin: 'https://httpbin.org',                          // HTTP 測試
  mockaroo: 'https://api.mockaroo.com'                      // 假資料生成
};
```

這份指南確保任何 agent 都能精準複製整個部署流程。
