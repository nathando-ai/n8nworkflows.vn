---
title: "🚀 Tự Động Hóa Báo Cáo Thị Trường Crypto Hàng Ngày Với Gemini AI & CoinGecko – Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp crypto nhận báo cáo thị trường crypto hàng ngày với phân tích AI chi tiết, bao gồm top movers, xu hướng cảm xúc và tổng quan thị trường, được gửi trực tiếp lên Discord. Tiết kiệm thời gian lên đến 5h/tuần và giảm thiểu sai sót trong phân tích."
slug: "tieu-dong-hoa-bao-cao-thi-truong-crypto-ai-gemini-coingecko"
tags: [n8n, crypto trading, AI automation, Gemini AI, Discord bot, no-code, tự động hóa thị trường tài chính]
keywords: [n8n workflow crypto, tự động hóa báo cáo crypto, Gemini AI phân tích thị trường, CoinGecko API tự động, Discord bot crypto, tự động hóa phân tích thị trường tài chính]
---

# 🚀 **Tự Động Hóa Báo Cáo Thị Trường Crypto Hàng Ngày Với Gemini AI & CoinGecko**

### **Giải pháp cho các sếp crypto muốn:**
- **Tiết kiệm 5h/tuần** phân tích thị trường thủ công.
- **Nhận báo cáo AI chính xác** với top movers, xu hướng cảm xúc và tổng quan thị trường.
- **Cập nhật tức thời** thông tin từ CoinGecko, NewsAPI và Gemini AI.
- **Gửi báo cáo tự động** lên Discord, Slack hoặc email hàng ngày.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần phân tích thủ công hàng ngày.
✅ **Chính xác cao**: Dữ liệu từ CoinGecko + phân tích AI Gemini.
✅ **Cá nhân hóa**: Báo cáo được gửi trực tiếp lên Discord với định dạng chuyên nghiệp.
✅ **Hoạt động 24/7**: Workflow tự động chạy hàng ngày, không cần can thiệp.
✅ **Tăng cường quyết định**: Nhận phân tích cảm xúc thị trường (Bullish/Bearish/Neutral) và top movers.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **API Key CoinGecko** (miễn phí, không cần đăng ký).
- **API Key NewsAPI** ([đăng ký miễn phí tại đây](https://newsapi.org/)) để lấy tin tức crypto.
- **API Key Google Gemini** ([đăng ký tại đây](https://makersuite.google.com/)) để sử dụng AI phân tích.
- **Token Bot Discord** hoặc **Webhook URL** để gửi báo cáo lên Discord.
- **Tài khoản Discord** để tạo channel nhận báo cáo (ví dụ: `#daily-market-summary`).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/10092](https://n8n.io/workflows/10092).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Bước 3**: Nếu muốn copy/paste, mở file JSON trong Notepad++/VS Code, sao chép toàn bộ nội dung và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần cấu hình kỹ lưỡng các node sau:

##### **🔹 Node 1: Schedule Trigger (8AM Hàng Ngày)**
- **Cấu hình**:
  - Thời gian mặc định là **8:00 AM** (UTC). Các sếp cần **chỉnh thời gian theo múi giờ của mình** (ví dụ: 3:00 PM Việt Nam = UTC+7).
  - Để thay đổi: Nhấp chuột phải vào node → **Edit** → Chọn **Schedule Trigger** → Điền lại thời gian (ví dụ: `0 0 15 * * ?` cho 3:00 PM hàng ngày).

##### **🔹 Node 2 & 3: Sentiment Data (NewsAPI) & Market Data (CoinGecko)**
- **Cấu hình**:
  - **NewsAPI**:
    - Điền **API Key** vào **Credentials** (tạo trong n8n: `n8n-nodes-base.httpRequest` → Thêm credential mới).
    - Tham số mặc định:
      ```json
      {
        "url": "https://newsapi.org/v2/top-headlines",
        "query": {
          "q": "crypto bitcoin ethereum solana blockchain",
          "apiKey": "{{$credentials.httpHeaderAuth.apiKey}}"
        }
      }
      ```
  - **CoinGecko**:
    - Không cần API Key (miễn phí).
    - Tham số mặc định:
      ```json
      {
        "url": "https://api.coingecko.com/api/v3/coins/markets",
        "query": {
          "vs_currency": "usd",
          "order": "market_cap_desc",
          "per_page": 10,
          "page": 1,
          "sparkline": false,
          "price_change_percentage_24h": true
        }
      }
      ```

##### **🔹 Node 4 & 5: Merge Data & Parse Data (Code)**
- **Lưu ý**:
  - Node **Merge Data** kết hợp dữ liệu từ CoinGecko và NewsAPI.
  - Node **Parse Data** chuẩn hóa dữ liệu thành định dạng chuẩn:
    ```json
    {
      "coin_name": "Bitcoin",
      "price_usd": 65000,
      "pct_change_24h": 2.5,
      "sentiment_score": 0.85, // (Tự động tính từ NewsAPI)
      "news_summary": "Bitcoin đạt mức cao mới trong tuần..."
    }
    ```
  - **Không cần chỉnh sửa** nếu các sếp muốn sử dụng cấu hình mặc định.

##### **🔹 Node 6: Research Analyst (Gemini AI Agent)**
- **Cấu hình**:
  - Chọn **Google Gemini API** trong **Credentials** (đã tạo trước đó).
  - **Prompt mặc định** (có thể tùy chỉnh):
    ```
    Analyze the following crypto market data and news:
    - Market Data: {{$json["market_data"]}}
    - News Data: {{$json["news_data"]}}
    Provide a concise summary including:
    1. Top 5 movers by 24h % change.
    2. Overall market sentiment (Bullish/Bearish/Neutral).
    3. Market summary (100-150 words).
    4. Analyst takeaway (1 actionable insight).
    Format output as JSON.
    ```
  - **Lưu ý**: Nếu muốn thay đổi mô hình AI, các sếp có thể thay thế bằng **OpenAI** hoặc **Anthropic** bằng cách chỉnh node `lmChatGoogleGemini` thành `lmChatOpenAI`.

##### **🔹 Node 7: Discord Auto-Poster**
- **Cấu hình**:
  - Chọn **Discord Bot Token** hoặc **Webhook URL** trong **Credentials**.
  - **Channel mặc định**: `#daily-market-summary` (các sếp có thể thay đổi).
  - **Định dạng embed**:
    ```json
    {
      "content": "📊 **Daily Crypto Market Summary**",
      "embeds": [
        {
          "title": "🪙 Top Movers",
          "description": "{{$json["top_movers"]}}",
          "fields": [
            { "name": "📈 Price (USD)", "value": "{{$json["price_usd"]}}", "inline": true },
            { "name": "📉 24H % Change", "value": "{{$json["pct_change_24h"]}}%", "inline": true }
          ]
        },
        {
          "title": "📊 Market Summary",
          "description": "{{$json["market_summary"]}}"
        },
        {
          "title": "💬 Sentiment",
          "description": "{{$json["sentiment"]}}"
        },
        {
          "title": "⚡ Analyst Takeaway",
          "description": "{{$json["takeaway"]}}"
        }
      ]
    }
    ```

---
### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Twitter API** để lấy xu hướng hashtag (#Bitcoin, #Ethereum) và tích hợp vào phân tích cảm xúc.
2. **Lưu báo cáo vào Google Sheets/Notion** để theo dõi lịch sử:
   - Sử dụng node **Google Sheets** hoặc **Notion** sau node **Discord Auto-Poster**.
   - Ví dụ:
     ```json
     {
       "url": "https://sheets.googleapis.com/v4/spreadsheets/{{$credentials.googleSheets.spreadsheetId}}/values/Sheet1!A1",
       "method": "POST",
       "body": {
         "values": [
           [
             "{{$json["date"]}}",
             "{{$json["coin_name"]}}",
             "{{$json["price_usd"]}}",
             "{{$json["pct_change_24h"]}}",
             "{{$json["sentiment"]}}"
           ]
         ]
       }
     }
     ```
3. **Gửi báo cáo qua Email** (nếu ưa thích):
   - Sử dụng node **Email** (ví dụ: Gmail SMTP) sau node **Discord Auto-Poster**.
4. **Tự động gửi báo cáo vào Slack** thay vì Discord:
   - Thay thế node **Discord** bằng **Slack Webhook**.
5. **Báo cáo định kỳ tuần/Tháng**:
   - Thay đổi **Schedule Trigger** từ hàng ngày sang `0 0 8 * * 1` (mỗi thứ Hai 8AM).
   - Thêm node **Google Calendar** để nhắc nhở.
:::

---
### **📌 Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp crypto **tự động hóa phân tích thị trường** với AI Gemini, nhận báo cáo hàng ngày trên Discord, và **tiết kiệm thời gian đáng kể** so với cách làm thủ công.

👉 **Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.io).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và chờ báo cáo đầu tiên vào 8AM ngày hôm sau!

---
**🚀 Chúc các sếp thành công với việc tự động hóa crypto!**
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **AFK Crypto** qua [Discord](https://discord.com/invite/v4DgTEUUJJ). 😊