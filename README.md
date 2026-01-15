# ☁️ 智能客服機器人 - Vercel API

為 NUWA Collibot EA1 機器人提供後端 API 服務。

## 📋 API 端點

### POST `/api/chat`
與 OpenAI Assistant 對話

**Request:**
```json
{
  "message": "用戶問題",
  "thread_id": "thread_xxx" // 可選，用於延續對話
}
```

**Response:**
```json
{
  "reply": "AI 回答",
  "thread_id": "thread_xxx"
}
```

---

### POST `/api/tts`
文字轉語音 (OpenAI TTS)

**Request:**
```json
{
  "text": "要轉換的文字",
  "voice": "alloy",  // 可選: alloy, echo, fable, onyx, nova, shimmer
  "speed": 1.0       // 可選: 0.25 ~ 4.0
}
```

**Response:**
- Content-Type: `audio/mpeg`
- 直接回傳 MP3 音檔

---

## 🚀 部署步驟

### 1. 準備工作

確保你有：
- [Vercel 帳號](https://vercel.com)
- OpenAI API Key
- OpenAI Assistant ID（已建立的 Assistant）

### 2. 部署到 Vercel

**方法 A：使用 Vercel CLI**
```bash
# 安裝 Vercel CLI
npm i -g vercel

# 登入
vercel login

# 部署
cd robot-assistant-vercel
vercel
```

**方法 B：使用 GitHub**
1. 將此專案推送到 GitHub
2. 在 Vercel Dashboard 匯入專案
3. Vercel 會自動部署

### 3. 設定環境變數

在 Vercel Dashboard 中設定：

| 變數名稱 | 說明 |
|---------|------|
| `OPENAI_API_KEY` | 你的 OpenAI API Key |
| `OPENAI_ASSISTANT_ID` | 你的 Assistant ID |

**設定位置：** Vercel Dashboard → 你的專案 → Settings → Environment Variables

### 4. 取得 API URL

部署完成後，你的 API URL 會是：
```
https://your-project-name.vercel.app
```

---

## 🔧 本地開發

```bash
# 安裝依賴
npm install

# 建立 .env 檔案
cp .env.example .env
# 編輯 .env 填入你的 API Key 和 Assistant ID

# 啟動開發伺服器
npm run dev
```

本地測試 URL：`http://localhost:3000`

---

## 📱 機器人端設定

部署完成後，在 Android 專案的 `index.html` 中設定：

```javascript
const CONFIG = {
    API_ENDPOINT: 'https://your-project-name.vercel.app/api/chat',
    TTS_ENDPOINT: 'https://your-project-name.vercel.app/api/tts',
    // ...
};
```

---

## 🧪 測試 API

### 測試 Chat API
```bash
curl -X POST https://your-project.vercel.app/api/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "你好"}'
```

### 測試 TTS API
```bash
curl -X POST https://your-project.vercel.app/api/tts \
  -H "Content-Type: application/json" \
  -d '{"text": "你好，我是智能客服"}' \
  --output test.mp3
```

---

## 📁 專案結構

```
robot-assistant-vercel/
├── api/
│   ├── chat.js          # OpenAI Assistant API
│   └── tts.js           # OpenAI TTS API
├── public/              # 靜態檔案 (可選)
├── vercel.json          # Vercel 設定
├── package.json         # NPM 設定
├── .env.example         # 環境變數範例
├── .gitignore           # Git 忽略清單
└── README.md            # 本說明文件
```

---

## ⚠️ 注意事項

1. **API Key 安全**：永遠不要將 API Key 提交到版本控制
2. **費用控管**：OpenAI API 會產生費用，建議設定用量限制
3. **CORS**：已設定允許跨域請求，機器人可直接呼叫

---

## 📄 授權

MIT License

---

Made with ❤️ for NUWA Collibot EA1
