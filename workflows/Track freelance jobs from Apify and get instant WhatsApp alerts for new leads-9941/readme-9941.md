---
title: "🚀 Theo dõi việc làm freelance từ Apify và nhận thông báo tức thì qua WhatsApp"
description: "Tự động hóa việc theo dõi việc làm freelance từ các nền tảng như Upwork, Fiverr và nhận thông báo tức thì qua WhatsApp khi có cơ hội mới. Giúp tiết kiệm thời gian và không bỏ lỡ cơ hội làm việc."
slug: "theo-doi-viec-lam-freelance-tu-apify-va-nhan-thong-bao-qua-whatsapp"
tags: [n8n, automation, no-code, freelance, apify, whatsapp]
keywords: [n8n workflow, tự động hóa, theo dõi việc làm, freelance, apify, whatsapp]
---

# 🚀 Theo dõi việc làm freelance từ Apify và nhận thông báo tức thì qua WhatsApp

[Đoạn mở đầu: Các sếp là freelancer, agency hay solopreneur thường phải theo dõi liên tục các nền tảng việc làm như Upwork, Fiverr để không bỏ lỡ cơ hội. Với workflow này, các sếp có thể tự động hóa quy trình này và nhận thông báo tức thì qua WhatsApp khi có việc làm mới phù hợp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi liên tục các nền tảng việc làm.
- Nhận thông báo tức thì: Có cơ hội làm việc mới sẽ được thông báo ngay qua WhatsApp.
- Quản lý hiệu quả: Tất cả thông tin việc làm mới được lưu trữ trong Google Sheets.
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify với một Actor hoạt động để scrape việc làm từ các nền tảng như Upwork, Freelancer, Fiverr.
- Cài đặt WhatsApp API hoặc Twilio để gửi thông báo.
- Tài khoản Google Sheets để lưu trữ thông tin việc làm.
- Instance n8n Cloud hoặc tự cài đặt trên VPS.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/9941](https://n8n.io/workflows/9941).
3. Hoặc tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When chat message received"**:
   - Cấu hình credentials cho WhatsApp API hoặc Twilio.
   - Có thể kích hoạt thủ công để bắt đầu workflow.

2. **Node "Run an Actor"**:
   - Kết nối với Apify API credentials.
   - Đảm bảo Actor ID trùng khớp với Actor trên Apify dashboard.

3. **Node "Get dataset items"**:
   - Kết nối với Apify API credentials.
   - Đảm bảo resource là "Datasets".

4. **Node "Code in JavaScript"**:
   - Chỉnh sửa mã JavaScript để lọc và định dạng dữ liệu theo nhu cầu.
   - Ví dụ: Chỉ bao gồm việc làm chứa từ khóa như "automation", "Python", hoặc "n8n".
   - Giới hạn số lượng thông báo để tránh spam.

5. **Node "Edit Fields1"**:
   - Ánh xạ dữ liệu đã được làm sạch (tiêu đề, ngân sách, URL) vào các trường phù hợp.
   - Đảm bảo định dạng tin nhắn nhất quán cho cả Google Sheets và WhatsApp.

6. **Node "Append or update row in sheet1"**:
   - Kết nối với Google Sheets OAuth2 API credentials.
   - Đảm bảo tên sheet và phạm vi dữ liệu phù hợp.

7. **Node "Edit Fields To send Specific Data"**:
   - Chuẩn bị nội dung tin nhắn cho WhatsApp.
   - Ví dụ:
     ```
     🔔 New Job Alert!
     💼 {{job_title}}
     💰 Budget: {{price}}
     🔗 Link: {{url}}
     ```

8. **Node "Send message"**:
   - Kết nối với WhatsApp API credentials.
   - Đảm bảo số điện thoại nhận tin nhắn đã được cấu hình đúng.

#### 3. Kích hoạt ⚡️
- Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu theo dõi việc làm mới.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Cron để chạy workflow định kỳ (ví dụ: mỗi 2 giờ) để tự động kiểm tra việc làm mới.
- Kết hợp với Slack hoặc Telegram để nhận thông báo bổ sung.
- Lưu log hoạt động của workflow để theo dõi hiệu suất và sửa lỗi.
- Gửi báo cáo định kỳ qua email với tổng hợp các việc làm mới trong tuần.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và không bỏ lỡ cơ hội làm việc mới. Với việc tự động hóa hoàn toàn, các sếp có thể tập trung vào công việc chính và nhận thông báo tức thì khi có cơ hội mới. Hãy áp dụng ngay để tối ưu hóa quá trình tìm kiếm việc làm freelance!