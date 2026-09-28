---
title: "🚀 Tạo bản tin thị trường hằng ngày từ Google Sheets, Alpha Vantage, Reddit, OpenAI & Slack"
description: "Tự động tổng hợp dữ liệu cổ phiếu, tin tức và cảm xúc xã hội, rồi gửi bản tóm tắt AI vào Slack mỗi ngày."
slug: "tao-ban-tin-thi-truong-hang-ngay"
tags: [n8n, automation, no-code, crypto-trading, ai-summarization]
keywords: [n8n workflow, tự động hóa, market brief, AI summarization, Alpha Vantage, Reddit, Slack]
---

# 🚀 Tạo bản tin thị trường hằng ngày từ Google Sheets, Alpha Vantage, Reddit, OpenAI & Slack

Bạn có bao giờ phải **đọc hàng chục nguồn tin, mở nhiều tab, sao chép dữ liệu giá cổ phiếu** chỉ để có một cái nhìn tổng quan cho ngày giao dịch?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, khiến các quyết định đầu tư trở nên kém chính xác.  

**Workflow này** sẽ tự động:

1. Lấy danh sách cổ phiếu từ Google Sheets.  
2. Thu thập giá cổ phiếu (Alpha Vantage), tin tức thị trường (RSS) và cảm xúc Reddit (RSS).  
3. Gửi toàn bộ dữ liệu vào OpenAI để **tóm tắt, lọc nhiễu và đưa ra hành động cụ thể**.  
4. Đẩy bản tin ngắn gọn, dễ đọc vào kênh Slack của bạn mỗi sáng.

Kết quả: **Bạn nhận được bản tin thị trường chuẩn AI, không cần mở bất kỳ trang web nào** – chỉ cần mở Slack và bắt đầu giao dịch.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn mở 10‑15 trang web mỗi ngày.  
- **Độ chính xác cao**: Dữ liệu được lấy trực tiếp từ API, giảm lỗi nhập tay.  
- **Cá nhân hoá**: Chỉ phân tích những cổ phiếu trong danh sách của bạn.  
- **Hoạt động liên tục**: Bản tin được gửi tự động vào đúng giờ, 7 ngày/tuần.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tài khoản Google, tạo sheet chứa cột `Symbol` (mã cổ phiếu).  
- **Alpha Vantage**: API key (miễn phí, giới hạn 5 yêu cầu/phút).  
- **OpenAI**: API key (ChatGPT‑3.5‑Turbo hoặc GPT‑4).  
- **Slack**: Workspace và token OAuth2 (có quyền `chat:write`).  
- **n8n**: Đã cài đặt và có quyền tạo credentials cho các dịch vụ trên.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc: https://n8n.io/workflows/12944).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON hoặc dán nội dung JSON vào ô **Import from Clipboard**.  
3. Nhấn **Import**, workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node quan trọng và cách cấu hình chúng:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Daily Market Brief Trigger** | `scheduleTrigger` | Chọn thời gian chạy hằng ngày (ví dụ: 07:00 AM UTC). |
| **Read portfolio holdings** | `googleSheets` | - **Spreadsheet ID**: ID của Google Sheet chứa danh sách cổ phiếu.<br>- **Sheet Name**: Tên sheet (mặc định `Sheet1`).<br>- **Credentials**: `googleSheetsOAuth2Api`. |
| **Stock Price (Alpha Vantage)** | `httpRequest` | - **URL**: `https://www.alphavantage.co/query`<br>- **Query Parameters**: `function=TIME_SERIES_DAILY_ADJUSTED`, `symbol={{ $json["Symbol"] }}`, `apikey=YOUR_ALPHA_VANTAGE_KEY`.<br>- **Credentials**: Không cần, chỉ nhập API key ở query. |
| **RSS Read** (Market News) | `rssFeedRead` | - **Feed URL**: URL RSS tin tức thị trường (ví dụ: `https://www.reuters.com/rssFeed`). |
| **Reddit Sentiment – RSS** | `rssFeedRead` | - **Feed URL**: RSS của subreddit liên quan (ví dụ: `https://www.reddit.com/r/CryptoCurrency/.rss`). |
| **Ai Analysis** | `openAi` (node `@n8n/n8n-nodes-langchain.openAi`) | - **Credentials**: `openAiApi`.<br>- **Model**: `gpt-3.5-turbo` (hoặc `gpt-4`).<br>- **Prompt**: Sử dụng output của node **Prepare AI Context** (được tạo tự động). |
| **Send actionable daily brief message** | `slack` | - **Channel**: ID hoặc tên kênh Slack nhận bản tin.<br>- **Message Text**: Dùng output của node **Parse AI Market Output**.<br>- **Credentials**: `slackOAuth2Api`. |
| **Normalize Stock Data**, **Normalize Market News**, **Normalize Reddit News**, **Parse AI Market Output**, **Prepare AI Context** | `code` | Không cần chỉnh, chỉ cần để nguyên. |
| **Process each stock** | `splitInBatches` | - **Batch Size**: 5 (để tránh vượt giới hạn API). |
| **Sticky Note** (nếu có) | `stickyNote` | Chỉ là ghi chú, không ảnh hưởng. |

> **Lưu ý:** Đảm bảo **các credentials** đã được tạo trong n8n → Credentials và được gán đúng cho từng node. Nếu chưa có, vào **Credentials → New Credential** và nhập API key tương ứng.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.  
2. Kiểm tra log của từng node, đặc biệt là **Ai Analysis** và **Send actionable daily brief message**.  
3. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram**: Thêm node `Telegram` sau node Slack để gửi bản tin tới nhóm Telegram.  
- **Lưu log vào Google Sheets**: Dùng một sheet phụ để ghi lại ngày, tổng quan thị trường và link báo cáo.  
- **Tạo PDF báo cáo**: Dùng node `HTML to PDF` + `Email` để gửi bản tin dạng PDF tới email cá nhân.  
- **Mở rộng nguồn dữ liệu**: Thêm `httpRequest` để lấy dữ liệu từ CoinGecko (crypto) hoặc Bloomberg.  
- **Alert dựa trên ngưỡng**: Thêm node `IF` để phát hiện biến động >5% và gửi cảnh báo ngay lập tức.

### 📌 Kết luận
Với workflow này, **các sếp sẽ không còn phải “đánh nhau” với hàng tá tab và báo cáo**. Một cú click vào Slack là đã có bản tin thị trường được tóm tắt, phân tích và kèm hành động cụ thể – giúp quyết định giao dịch nhanh hơn, chính xác hơn và giảm thiểu rủi ro.  

Hãy **import ngay**, cấu hình các credentials và để n8n làm việc cho bạn! 🚀