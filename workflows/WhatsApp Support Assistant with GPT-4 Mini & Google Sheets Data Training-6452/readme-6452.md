---
title: "🤖 Hướng dẫn tự động hóa hỗ trợ khách hàng WhatsApp với GPT-4 Mini & Google Sheets"
description: "Tự động hóa hoàn toàn quy trình hỗ trợ khách hàng qua WhatsApp bằng công nghệ AI, lưu trữ dữ liệu vào Google Sheets và huấn luyện mô hình để cải thiện chất lượng dịch vụ."
slug: "tu-dong-hoa-ho-tro-khach-hang-whatsapp-gpt4mini-googlesheets"
tags: [n8n, automation, no-code, ai, chatbot, whatsapp, google-sheets]
keywords: [n8n workflow, tự động hóa, chatbot, whatsApp, google sheets, AI]
---

# 🤖 Tự động hóa hỗ trợ khách hàng WhatsApp với GPT-4 Mini & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình hỗ trợ khách hàng qua WhatsApp
- Tiết kiệm thời gian và nhân lực cho đội ngũ chăm sóc khách hàng
- Cải thiện chất lượng dịch vụ nhờ khả năng xử lý thông tin từ dữ liệu huấn luyện
- Lưu trữ và quản lý thông tin khách hàng một cách hiệu quả trên Google Sheets
- Hỗ trợ đa ngôn ngữ nhờ khả năng huấn luyện mô hình AI
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (hoặc sử dụng các dịch vụ như Twilio, MessageBird)
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ OpenAI (để sử dụng GPT-4 Mini)
- Google Sheets đã được cấu hình với các bảng dữ liệu: thông tin công ty, sản phẩm, dịch vụ
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/6452](https://n8n.io/workflows/6452)
2. Nhấn nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào
4. Nhấn "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook** (Node đầu tiên):
   - Cấu hình webhook để nhận tin nhắn từ WhatsApp
   - Đảm bảo webhook được cấu hình đúng với dịch vụ bạn sử dụng (Twilio, MessageBird, WhatsApp Business API)

2. **Read Company Basic Information** (Google Sheets Tool):
   - Cấu hình Google Sheets API credentials
   - Chỉ định ID của Google Sheet chứa thông tin cơ bản của công ty
   - Đảm bảo bảng dữ liệu có cấu trúc phù hợp với yêu cầu của workflow

3. **Read Product Sheet** (Google Sheets Tool):
   - Cấu hình Google Sheets API credentials
   - Chỉ định ID của Google Sheet chứa thông tin sản phẩm
   - Đảm bảo bảng dữ liệu có cấu trúc phù hợp với yêu cầu của workflow

4. **Read Service Sheet** (Google Sheets Tool):
   - Cấu hình Google Sheets API credentials
   - Chỉ định ID của Google Sheet chứa thông tin dịch vụ
   - Đảm bảo bảng dữ liệu có cấu trúc phù hợp với yêu cầu của workflow

5. **OpenAI Model1** (lmChatOpenAi):
   - Cấu hình OpenAI API credentials
   - Chọn mô hình GPT-4 Mini (hoặc mô hình tương thích khác)
   - Điều chỉnh các tham số như nhiệt độ, độ dài phản hồi,...

6. **AI Agent - Customer Support Agent** (Agent):
   - Cấu hình các công cụ hỗ trợ cho Agent
   - Đảm bảo Agent có quyền truy cập vào các công cụ cần thiết (Google Sheets, OpenAI,...)
   - Tùy chỉnh prompt và hướng dẫn cho Agent

7. **Log Customer Issues** (Google Sheets Tool):
   - Cấu hình Google Sheets API credentials
   - Chỉ định ID của Google Sheet để lưu trữ thông tin vấn đề khách hàng
   - Đảm bảo bảng dữ liệu có cấu trúc phù hợp với yêu cầu của workflow

8. **Send Message Using HTTP Request** (httpRequest):
   - Cấu hình HTTP Request để gửi tin nhắn phản hồi đến khách hàng
   - Đảm bảo có quyền truy cập vào API của dịch vụ tin nhắn bạn sử dụng

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa quy trình hỗ trợ khách hàng.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có vấn đề khách hàng mới
- Lưu log chi tiết các tương tác khách hàng để phân tích sau này
- Gửi báo cáo định kỳ về các vấn đề khách hàng phổ biến
- Tích hợp với các hệ thống CRM khác để quản lý thông tin khách hàng toàn diện
- Sử dụng các mô hình AI khác để cải thiện chất lượng dịch vụ

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quy trình hỗ trợ khách hàng qua WhatsApp, giúp các doanh nghiệp tiết kiệm thời gian và nhân lực, đồng thời cải thiện chất lượng dịch vụ nhờ khả năng xử lý thông tin từ dữ liệu huấn luyện. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tối ưu hóa quy trình làm việc của bạn!