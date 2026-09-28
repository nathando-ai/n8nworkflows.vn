---
title: "🚀 Tự động hóa kiểm tra cấu hình GitHub với GPT-4o-mini và ghi log lỗi lên Sheets & Slack"
description: "Hướng dẫn tự động hóa kiểm tra đồng bộ cấu hình giữa các file config trong repo và tài liệu FAQ sử dụng AI, ghi log lỗi lên Google Sheets và gửi cảnh báo Slack"
slug: "tu-dong-hoa-kiem-tra-cau-hinh-github-voi-gpt-4o-mini"
tags: [n8n, automation, no-code, devops, ai]
keywords: [n8n workflow, tự động hóa, devops, ai, github]
---

# 🚀 Tự động hóa kiểm tra cấu hình GitHub với GPT-4o-mini và ghi log lỗi lên Sheets & Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải kiểm tra thủ công sự đồng bộ giữa các file cấu hình trong repo và tài liệu FAQ. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian kiểm tra thủ công: Tự động phát hiện các điểm không đồng bộ giữa cấu hình thực tế và tài liệu
- Tăng độ chính xác: Sử dụng AI để phân tích chi tiết các điểm khác biệt
- Hoạt động liên tục: Theo dõi thay đổi trong repo và kiểm tra ngay lập tức
- Tăng tính minh bạch: Ghi log tất cả các vấn đề phát hiện được
- Giảm rủi ro: Nhận cảnh báo ngay khi phát hiện các vấn đề nghiêm trọng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền truy cập repo cần kiểm tra
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- API key từ OpenAI (đã đăng ký gói sử dụng GPT-4o-mini)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n Editor](https://n8n.io/workflows/10329)
2. Click vào nút "Import from URL" và nhập link: https://n8n.io/workflows/10329
3. Hoặc copy nội dung JSON từ trang workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "GitHub Push or PR Event"**:
   - Thêm credentials GitHub OAuth2
   - Cấu hình các sự kiện cần theo dõi (push, pull_request)
   - Đặt webhook secret nếu cần bảo mật

2. **Node "Fetch Repository Config" và "Fetch FAQ Reference Config"**:
   - Cập nhật đường dẫn đến file config trong repo của các sếp
   - Đảm bảo các file này tồn tại và có định dạng JSON hợp lệ

3. **Node "OpenAI GPT-4o-mini"**:
   - Thêm credentials OpenAI API
   - Đảm bảo tài khoản có đủ credit để sử dụng GPT-4o-mini
   - Có thể điều chỉnh các tham số như max_tokens, temperature nếu cần

4. **Node "Log to Google Sheets"**:
   - Tạo Google Sheet mới với cấu trúc các cột như sau:
     - timestamp
     - configKey
     - faqReference
     - actualConfig
     - issueType
     - severity
     - suggestion
     - confidence
     - issueId
     - summary
   - Thêm credentials Google Sheets OAuth2
   - Cập nhật ID của Google Sheet và tên sheet trong node

5. **Node "Send Slack Alert"**:
   - Thêm credentials Slack API
   - Chọn channel cần gửi cảnh báo
   - Tùy chỉnh template tin nhắn nếu cần

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" để kích hoạt workflow
2. Test với một sự kiện push/PR mẫu để kiểm tra hoạt động
3. Kiểm tra Google Sheets và Slack để xác nhận các vấn đề được ghi log và gửi cảnh báo đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với các công cụ khác**: Có thể thêm node để gửi email cảnh báo hoặc cập nhật trạng thái trong Jira
2. **Tùy chỉnh mức độ nghiêm trọng**: Thêm điều kiện để chỉ gửi cảnh báo cho các vấn đề nghiêm trọng nhất
3. **Lịch sử kiểm tra**: Có thể thêm node để lưu trữ lịch sử kiểm tra và so sánh giữa các lần kiểm tra
4. **Báo cáo định kỳ**: Thiết lập workflow chạy định kỳ để kiểm tra toàn bộ repo và gửi báo cáo tổng hợp

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình kiểm tra đồng bộ cấu hình giữa repo và tài liệu FAQ, giảm thiểu rủi ro và tiết kiệm thời gian cho các công việc thủ công. Bằng cách tích hợp AI để phân tích và gửi cảnh báo, các sếp có thể tập trung vào các vấn đề quan trọng nhất và đảm bảo tính nhất quán của hệ thống.