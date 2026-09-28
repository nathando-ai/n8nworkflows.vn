---
title: "🚀 Tự động hóa Email Hỗ trợ: Tóm tắt Gmail với Gemini và Gửi lên Slack"
description: "Giải pháp tự động hóa 100% không cần code giúp tóm tắt email hỗ trợ từ Gmail bằng AI Gemini và gửi thông báo lên Slack, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-email-ho-tro-gmail-gemini-slack"
tags: [n8n, automation, no-code, ai, slack, gmail]
keywords: [n8n workflow, tự động hóa email, tóm tắt email, gemini ai, slack notification]
---

# 🚀 Tự động hóa Email Hỗ trợ: Tóm tắt Gmail với Gemini và Gửi lên Slack

[Các sếp đang làm việc với lượng lớn email hỗ trợ hàng ngày? Bạn mệt mỏi với việc phải đọc từng email dài dòng và tóm tắt thủ công? Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể bằng cách tự động hóa toàn bộ quy trình từ nhận email đến gửi thông báo tóm tắt lên Slack.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tóm tắt email dài thành bản tóm tắt ngắn gọn (5-10 dòng).
- **Nâng cao hiệu suất**: Nhận thông báo tóm tắt ngay trên Slack mà không cần mở email.
- **Tăng cường phản hồi**: Đảm bảo không bỏ sót bất kỳ email hỗ trợ quan trọng nào.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập email hỗ trợ.
- API Key từ Google Cloud cho dịch vụ Gemini.
- Token truy cập Slack với quyền gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/7594](https://n8n.io/workflows/7594)
3. Hoặc tải file JSON về máy và import từ local file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Check Support Emails"**:
  - Cấu hình credentials cho Gmail OAuth2.
  - Điền email và label/folder cần theo dõi (ví dụ: "support@company.com", "INBOX").

- **Node "Google Gemini To Summarize Email"**:
  - Cấu hình credentials cho Google Palm API.
  - Đảm bảo API Key có quyền truy cập vào dịch vụ Gemini.
  - Tùy chỉnh prompt nếu cần (mặc định đã được tối ưu cho tóm tắt email).

- **Node "Post Summary to Slack User"**:
  - Cấu hình credentials cho Slack API.
  - Chọn channel hoặc người dùng cụ thể để gửi thông báo.
  - Tùy chỉnh thông điệp nếu cần (ví dụ: thêm thông tin về người gửi).

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ (Gmail, Gemini, Slack).
2. Chạy test với một email mẫu để đảm bảo workflow hoạt động đúng.
3. Bật Active workflow và kiểm tra lại lần cuối.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thêm node gửi thông báo đến Telegram để nhận bản tóm tắt trên điện thoại.
- **Lưu log**: Thêm node lưu bản tóm tắt vào Google Sheets để theo dõi lịch sử.
- **Phân loại email**: Sử dụng node điều kiện để chỉ tóm tắt email từ các nguồn quan trọng nhất.
- **Gửi báo cáo định kỳ**: Lập lịch gửi báo cáo tổng hợp các email đã xử lý trong ngày.

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao hiệu suất làm việc bằng cách tự động hóa quy trình tóm tắt email. Hãy áp dụng ngay để trải nghiệm sự khác biệt!