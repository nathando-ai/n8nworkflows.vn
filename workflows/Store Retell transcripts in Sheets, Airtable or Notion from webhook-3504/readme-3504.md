---
title: "📞 Lưu Transcript Retell vào Google Sheets/Airtable/Notion từ Webhook"
description: "Hướng dẫn tự động lưu transcript cuộc gọi từ Retell vào Google Sheets, Airtable hoặc Notion thông qua webhook - giải pháp hoàn hảo cho các nhà phát triển Retell"
slug: "luu-transcript-retell-vao-google-sheets-airtable-notion-tu-webhook"
tags: [n8n, automation, no-code, retell, ai]
keywords: [n8n workflow, tự động hóa, retell, transcript, google sheets, airtable, notion]
---

# 📞 Lưu Transcript Retell vào Google Sheets/Airtable/Notion từ Webhook

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà phát triển Retell khi phải theo dõi thủ công các cuộc gọi và dữ liệu phân tích. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu transcript và dữ liệu phân tích cuộc gọi Retell vào các công cụ quản lý dữ liệu quen thuộc
- Tiết kiệm thời gian và công sức trong việc theo dõi thủ công
- Dữ liệu được lưu trữ cấu trúc và dễ truy xuất
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Retell AI đã được cấu hình
- Agent Retell với số điện thoại đã liên kết
- Một trong các công cụ lưu trữ dữ liệu sau:
  - Airtable base và table (ví dụ: "Transcripts")
  - Google Sheet với tab "Transcripts"
  - Notion database với các cột phù hợp với dữ liệu transcript
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/3504)
2. Nhấn nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook Node**:
   - Đảm bảo đường dẫn webhook là `poc-retell-analysis`
   - Phương thức HTTP là POST

2. **Set fields to export Node**:
   - Cấu hình các trường dữ liệu cần lưu trữ (call ID, transcript, summary, sentiment...)
   - Có thể thêm các trường phân tích sau cuộc gọi nếu sử dụng

3. **Save to Airtable Node**:
   - Cấu hình credentials "airtableTokenApi"
   - Chọn base và table phù hợp
   - Đảm bảo các trường trong Airtable khớp với dữ liệu từ Retell

4. **Save to Excel Node**:
   - Cấu hình credentials "googleSheetsOAuth2Api"
   - Chọn Google Sheet và tab "Transcripts"
   - Đảm bảo các cột trong Sheet khớp với dữ liệu từ Retell

5. **Save to Notion Node**:
   - Cấu hình credentials "notionApi"
   - Chọn database phù hợp
   - Đảm bảo các thuộc tính trong Notion database khớp với dữ liệu từ Retell

6. **Filter - only call ended Node**:
   - Đảm bảo chỉ lọc các sự kiện `call_analyzed` từ Retell

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node, thực hiện test run với dữ liệu mẫu
2. Kiểm tra dữ liệu được lưu trữ đúng trong các công cụ đã chọn
3. Bật Active workflow để bắt đầu lưu trữ tự động

### ✍️ Mẹo & gợi ý nâng cao
- Nếu sử dụng các trường phân tích sau cuộc gọi, hãy thêm các cột tương ứng trong các công cụ lưu trữ
- Có thể kết hợp với Slack/Telegram để nhận thông báo khi có cuộc gọi mới
- Đặt lịch gửi báo cáo định kỳ về các cuộc gọi và dữ liệu phân tích
- Tích hợp với các công cụ phân tích dữ liệu khác để có cái nhìn tổng quan hơn

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh để tự động lưu trữ và quản lý dữ liệu cuộc gọi từ Retell. Với việc tích hợp dễ dàng và tính linh hoạt, các nhà phát triển có thể nhanh chóng triển khai hệ thống theo dõi cuộc gọi một cách hiệu quả mà không cần phải viết code. Hãy thử ngay và tiết kiệm thời gian cho các công việc quan trọng hơn!