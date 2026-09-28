---
title: "🚀 Tự Động Hóa Tin Tức Crypto Thời Gian Thực + Phân Tích Sentiment qua Telegram với GPT-4o (Miễn Code)"
description: "Workflow tự động hóa lấy tin tức crypto từ 10 nguồn uy tín, phân tích cảm xúc thị trường và gửi kết quả ngay qua Telegram với GPT-4o. Giúp các sếp crypto theo dõi thị trường 24/7 mà không cần check thủ công."
slug: "tieu-dong-hoa-tin-tuc-crypto-sentiment-telegram-gpt-4o"
tags: [n8n, automation, crypto, ai, telegram, openai, gpt-4o, no-code, finance]
keywords: [tự động hóa tin tức crypto, phân tích sentiment crypto, telegram bot crypto, gpt-4o n8n, rss feed crypto, tự động hóa thị trường crypto]
---

# 🚀 **Tự Động Hóa Tin Tức Crypto Thời Gian Thực + Phân Tích Sentiment qua Telegram với GPT-4o**

### **Giải pháp cho các sếp crypto muốn theo dõi thị trường 24/7 mà không cần check thủ công**

Hiện nay, thị trường crypto thay đổi cực nhanh, và việc theo dõi tin tức từ hàng chục nguồn uy tín như **CoinTelegraph, Bitcoin Magazine, CoinDesk** hay **Crypto Briefing** là một công việc tốn thời gian và dễ bỏ lỡ thông tin quan trọng. Thêm vào đó, phân tích **sentiment** (cảm xúc thị trường) từ những tin tức đó cũng đòi hỏi kiến thức chuyên sâu.

Workflow này **tự động hóa toàn bộ quá trình**:
✅ **Lấy tin tức crypto** từ 10 nguồn RSS uy tín.
✅ **Phân tích sentiment** và tổng hợp tin tức liên quan đến từ khóa của bạn (ví dụ: "Bitcoin", "NFT", "Ethereum").
✅ **Gửi kết quả ngay qua Telegram** với một bản tóm tắt ngắn gọn, phân tích cảm xúc thị trường và link tin tức chi tiết.

Không cần viết một dòng code, chỉ cần **cài đặt và chạy** trên n8n Self-hosted!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần check thủ công 10+ nguồn tin tức hàng ngày.
- **Phân tích sentiment tự động**: Hiểu được **cảm xúc thị trường** (tin tốt, xấu, trung lập) từ tin tức.
- **Tin tức cá nhân hóa**: Chỉ lấy tin tức liên quan đến từ khóa bạn nhập (ví dụ: "Solana" hoặc "Stablecoin").
- **Hoạt động 24/7**: Workflow chạy tự động, không cần người quản lý.
- **Gửi kết quả ngay qua Telegram**: Đọc tin tức và phân tích ngay trên app Telegram yêu thích.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:

### **1. Tài khoản Telegram Bot**
- Tạo **bot Telegram** bằng cách chat với [@BotFather](https://t.me/BotFather) và lấy **API Token**.
- Cài đặt bot vào nhóm hoặc chat cá nhân để nhận tin tức.

### **2. API Key OpenAI**
- Đăng ký tài khoản tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
- Chọn mô hình **GPT-4o-mini** (miễn phí và hiệu quả).

### **3. (Tùy chọn) Thêm nguồn RSS khác**
- Nếu muốn lấy tin tức từ nguồn khác, thêm **URL RSS** vào node `RSS Feed Read`.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/3751) (ấn **Export**).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor và tạo **Workflow mới**.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ mã từ [n8n.io/workflows/3751](https://n8n.io/workflows/3751).
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Telegram Bot**
- **Node**: `Send Crypto or Company Name for Analysis` (Telegram Trigger)
  - Điền **API Token** từ `@BotFather` vào `credentials` (tên: `telegramApi`).
  - **Chat ID**: Để trống hoặc nhập **dynamic value** như `<< Telegram ID here >>` (sẽ tự động lấy từ session).

- **Node**: `Sends Response` (Telegram)
  - Chọn **credentials** là `telegramApi` (cùng với bot trước).
  - **Chat ID**: Để trống để bot tự động gửi tin tức đến người dùng.

#### **🔹 Cấu hình OpenAI**
- **Node**: `OpenAI Chat Model` và `Summarize News & Sentiment (GPT-4o)`
  - Điền **API Key** vào `credentials` (tên: `openAiApi`).
  - **Model**: Đảm bảo chọn `gpt-4o-mini` (hoặc `gpt-4o` nếu có budget).

#### **🔹 Cấu hình RSS Feeds**
- **Nodes**: `RSS Cointelegraph`, `RSS Bitcoinmagazine`, ... (tất cả `rssFeedRead`)
  - Điền **URL RSS** của từng nguồn (đã được cấu hình sẵn trong workflow).

#### **🔹 Cấu hình Agent AI (Extract Keyword)**
- **Node**: `Crypto News & Sentiment Agent`
  - Đây là **AI Agent** tự động phân tích từ khóa người dùng (ví dụ: "Bitcoin") và trả về **keyword chính** để lọc tin tức.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi logic phân tích.

#### **🔹 Cấu hình Filter & Prompt**
- **Node**: `Filter by Query` (Code)
  - Đây là **lọc tin tức** dựa trên keyword từ AI Agent.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi logic lọc.

- **Node**: `Build Prompt` (Code)
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi cách xây dựng prompt cho GPT-4o.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn vào bot Telegram (ví dụ: **"Bitcoin"**).
   - Workflow sẽ:
     - Lấy tin tức liên quan.
     - Phân tích sentiment.
     - Gửi kết quả qua Telegram.

2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Thêm nguồn RSS khác**
- Mở rộng coverage bằng cách thêm **URL RSS** mới vào node `RSS Feed Read`.
- Ví dụ: `https://news.bitcoin.com/feed/` (Bitcoin.com).

### **🔹 Lưu log tin tức**
- Thêm **node `Set`** sau `Merge All Articles` để lưu tin tức vào **Google Sheets** hoặc **Database**.
- Cách làm:
  ```javascript
  // Node Code: Set (lưu vào Google Sheets)
  $json = {
    "title": $node["RSS Cointelegraph"].json["title"],
    "link": $node["RSS Cointelegraph"].json["link"],
    "sentiment": $node["Summarize News & Sentiment (GPT-4o)"].json["sentiment"]
  };
  return $json;
  ```

### **🔹 Gửi báo cáo định kỳ (Email/Telegram)**
- Thêm **node `Schedule`** để chạy workflow hàng ngày (ví dụ: 8h sáng).
- Sau đó, gửi báo cáo qua **Email** (node `Email`) hoặc **Telegram**.

### **🔹 Tích hợp với Discord/Slack**
- Thay thế node `Telegram` bằng `Slack` hoặc `Discord Webhook`.
- Cách làm:
  1. Tạo **Slack App** và lấy **Webhook URL**.
  2. Thay `telegramApi` bằng `slackApi` và điền **Webhook URL**.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp crypto để theo dõi thị trường một cách **tự động hóa, chính xác và cá nhân hóa**. Không cần viết code, chỉ cần **cài đặt và chạy** trên n8n Self-hosted.

**Bắt đầu ngay!**
1. Import workflow.
2. Cấu hình Telegram + OpenAI.
3. Gửi tin nhắn **"Bitcoin"** vào bot Telegram và xem kết quả AI phân tích!

🚀 **Hãy tự động hóa thị trường crypto của mình hôm nay!**