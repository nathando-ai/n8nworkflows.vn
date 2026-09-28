---
title: "🚀 Tự Động Hóa Email Giao Tiếp Cá Nhân Hóa AI + Bot Telegram + Scraping Website - Demo Thực Hành Cho Agencies"
description: "Workflow này giúp các agency AI tự động hóa quá trình demo email cá nhân hóa thông minh, thu hút khách hàng tiềm năng thông qua bot Telegram và scraping website. Giúp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và cá nhân hóa tương tác 1:1."
slug: "tieu-dong-hoa-email-canh-bao-ai-telegram-scraping"
tags: [n8n, automation, no-code, ai-chatbot, lead-nurturing, email-marketing, scraping-website, telegram-bot, postgres-database]
keywords: [n8n workflow email tự động, tự động hóa email cá nhân hóa AI, bot telegram demo, scraping website tự động, demo email cá nhân hóa, n8n với AI và RAG, tự động hóa lead nurturing]
---

# 🚀 **Tự Động Hóa Email Giao Tiếp Cá Nhân Hóa AI + Bot Telegram + Scraping Website**

## **📌 Giới Thiệu**
Bạn là một agency AI hoặc chuyên gia tự động hóa muốn **hiển thị khả năng của mình** cho khách hàng tiềm năng? Hoặc bạn đang gặp khó khăn khi phải **gửi email cá nhân hóa thủ công** cho từng khách hàng? Workflow này sẽ giúp bạn **tự động hóa toàn bộ quá trình demo email cá nhân hóa** thông qua:
✅ **Bot Telegram** để tương tác trực tiếp với khách hàng.
✅ **AI RAG (Retrieval-Augmented Generation)** để tạo nội dung email thông minh.
✅ **Scraping website** để lấy dữ liệu từ trang web của khách hàng.
✅ **Gửi email tự động** qua SparkPost (hoặc SMTP khác).
✅ **Quản lý log và giới hạn gửi email** để tránh spam.

Workflow này **không cần code**, chỉ cần cấu hình và chạy 24/7 trên **n8n Self-hosted** để tối ưu chi phí và hiệu suất.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gửi email thủ công, AI tự động tạo nội dung cá nhân hóa.
- **Tăng tỷ lệ chuyển đổi**: Email được tối ưu hóa dựa trên dữ liệu website của khách hàng.
- **Tương tác thực thời**: Khách hàng có thể thử demo qua Telegram mà không cần hỗ trợ trực tiếp.
- **Quản lý log và giới hạn**: Tránh spam và theo dõi hiệu quả của mỗi khách hàng.
- **Scalability cao**: Dễ dàng mở rộng cho nhiều khách hàng khác nhau.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).
✔ **Docker** (để chạy Crawl4AI).
✔ **Crawl4AI** (để scraping website hiệu quả).
✔ **Telegram Bot** (tạo qua [@BotFather](https://t.me/BotFather)).
✔ **SparkPost hoặc SMTP** (để gửi email).
✔ **Cơ sở dữ liệu PostgreSQL/MySQL/SQLite** (để lưu log khách hàng).
✔ **API Key OpenAI** (để sử dụng AI RAG và chatbot).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10143](https://n8n.io/workflows/10143) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (n8n.io/editor).
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô nhập.
  3. Nhấn **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Telegram Bot**
- **Node**: `Telegram Trigger`, `Telegram`, `TelegramTrigger`
- **Cần thiết**:
  - Đăng ký bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
  - Trong **Credentials** của n8n, thêm `telegramApi` với token này.
  - Cấu hình **Chat ID** của khách hàng (hoặc sử dụng `/start` để bắt đầu demo).

#### **🔹 Cấu hình OpenAI API**
- **Nodes**: `openAi`, `lmChatOpenAi`, `embeddingsOpenAi`, `agent`
- **Cần thiết**:
  - Tạo **API Key OpenAI** tại [OpenAI](https://platform.openai.com/).
  - Thêm `openAiApi` trong **Credentials** của n8n với API Key.
  - Chọn **model** phù hợp (ví dụ: `gpt-4.1-mini` cho `lmChatOpenAi`).

#### **🔹 Cấu hình Database (PostgreSQL)**
- **Nodes**: `postgresTool`, `memoryPostgresChat`, `vectorStorePGVector`
- **Cần thiết**:
  - Tạo bảng `logs` với các cột:
    - `name` (tên khách hàng)
    - `id` (ID Telegram hoặc ID duy nhất)
    - `email_sent` (để đếm số email đã gửi)
  - Cấu hình **PostgreSQL Connection** trong **Credentials** của n8n.

#### **🔹 Cấu hình Crawl4AI (Docker)**
- **Nodes**: `crawl4ai`, `crawl4ai1`
- **Cần thiết**:
  - Cài **Docker** và chạy Crawl4AI theo hướng dẫn tại [GitHub](https://github.com/unclecode/crawl4ai).
  - Cấu hình **URL Docker** trong `HTTP Request` để Crawl4AI hoạt động.

#### **🔹 Cấu hình Email (SparkPost/SMTP)**
- **Nodes**: `emailSend`
- **Cần thiết**:
  - Nếu dùng **SparkPost**:
    - Tạo tài khoản và lấy **API Key**.
    - Cấu hình trong `smtp` credentials của n8n.
  - Nếu dùng **SMTP khác** (Gmail, SendGrid...), cấu hình tương tự.

#### **🔹 Cấu hình Giới Hạn Email**
- **Nodes**: `If1`, `If2`, `set maximum email per id`
- **Cần thiết**:
  - Đặt số lượng email tối đa cho mỗi khách hàng (ví dụ: 3 email/ngày).
  - Nếu vượt quá giới hạn, bot sẽ gửi thông báo lỗi qua Telegram.

#### **🔹 Cấu hình Scraping Website**
- **Nodes**: `sitemap.xml request`, `sitemap_index.xml request`, `crawl4ai`
- **Cần thiết**:
  - Điền **URL website** của khách hàng vào `HTTP Request`.
  - Nếu scraping thất bại, Crawl4AI sẽ tự động thay thế.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** với dữ liệu mẫu (ví dụ: ID Telegram của bạn).
   - Kiểm tra bot Telegram có phản hồi đúng không.
2. **Bật Active**:
   - Đặt **Schedule Trigger** để chạy hàng ngày (nếu cần).
   - Hoặc để **Telegram Trigger** hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Tối ưu hóa AI RAG**
- **Cải thiện prompt** trong `Email Craft` và `Page Sumarize` để email trở nên cá nhân hóa hơn.
- **Sử dụng vector store** (`vectorStorePGVector`) để lưu trữ và tra cứu dữ liệu website hiệu quả.

### **🔹 Quản lý log và báo cáo**
- **Thêm node `insert log`** để lưu tất cả tương tác của khách hàng.
- **Sử dụng `dataTable`** để tạo báo cáo thống kê số email đã gửi.

### **🔹 Tăng cường tương tác Telegram**
- **Thêm menu bot** để khách hàng dễ dàng chọn chức năng.
- **Gửi thông báo hoàn thành** (`Finish notif`) khi email được gửi thành công.

### **🔹 Scraping website hiệu quả**
- **Sử dụng `XML` node** để phân tích sitemap.xml trước khi scraping.
- **Lưu trữ nội dung website** trong PostgreSQL để tránh scraping lại.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các agency AI **demo email cá nhân hóa** một cách tự động, không cần code. Bằng cách kết hợp **Telegram Bot, AI RAG, Scraping Website và Email Automation**, bạn có thể:
✔ **Tiết kiệm thời gian** trong quá trình demo.
✔ **Tăng tỷ lệ chuyển đổi** với email cá nhân hóa.
✔ **Quản lý khách hàng hiệu quả** với log và giới hạn gửi email.

**Hãy thử ngay và biến demo của bạn thành một trải nghiệm tuyệt vời cho khách hàng!** 🚀

---
**🔗 [Xem demo live tại @email_demo_bot](https://t.me/email_demo_bot)** (nếu có)