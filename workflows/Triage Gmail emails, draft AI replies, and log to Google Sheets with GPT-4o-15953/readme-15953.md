---
title: "🚀 Tự động phân loại email Gmail, soạn nháp trả lời AI và ghi log vào Google Sheets với GPT-4o"
description: "Workflow n8n tự động phân loại email Gmail, soạn nháp trả lời AI và ghi log vào Google Sheets với GPT-4o giúp tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-phan-loai-email-gmail-soan-nhap-tra-loi-ai-ghi-log-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, gmail, google-sheets, ai, openai]
keywords: [n8n workflow, tự động hóa email, phân loại email, soạn nháp AI, ghi log Google Sheets, GPT-4o]
---

# 🚀 Tự động phân loại email Gmail, soạn nháp trả lời AI và ghi log vào Google Sheets với GPT-4o

[Các sếp đang gặp khó khăn khi phải xử lý hàng loạt email hàng ngày, phân loại ưu tiên và soạn nháp trả lời một cách thủ công. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này với công nghệ AI tiên tiến từ OpenAI.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại email theo mức độ ưu tiên (khẩn cấp/không khẩn cấp)
- Tự động soạn nháp trả lời bằng AI cho email khẩn cấp
- Ghi log chi tiết vào Google Sheets cho cả email khẩn cấp và không khẩn cấp
- Tiết kiệm thời gian xử lý email hàng ngày lên đến 70%
- Tăng tính chuyên nghiệp trong giao tiếp với khách hàng
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ (đọc email và tạo nháp)
- Tài khoản OpenAI với API key và quyền truy cập GPT-4o
- Tài khoản Google với quyền truy cập Google Sheets
- Bảng tính Google Sheets đã được tạo sẵn để lưu log
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/15953)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When New Email Arrives" (gmailTrigger)**:
   - Cấu hình credentials cho tài khoản Gmail
   - Đảm bảo tài khoản có quyền đọc email mới

2. **Node "Extract Email Details" (set)**:
   - Kiểm tra các trường dữ liệu được trích xuất (sender, subject, body, message ID)
   - Có thể thêm/xóa các trường dữ liệu tùy theo nhu cầu

3. **Node "AI Determines Urgency" (openAi)**:
   - Cấu hình credentials cho OpenAI
   - Chọn model GPT-4o
   - Tùy chỉnh prompt để phân loại mức độ ưu tiên phù hợp với nhu cầu của các sếp

4. **Node "Assign Urgency Label" (set)**:
   - Kiểm tra giá trị nhãn ưu tiên được gán (ví dụ: "urgent", "non-urgent")
   - Có thể điều chỉnh nhãn này theo tiêu chuẩn của các sếp

5. **Node "Check Email Urgency" (if)**:
   - Kiểm tra điều kiện IF để đảm bảo nó khớp với đầu ra của node "AI Determines Urgency"
   - Điều chỉnh nếu cần thiết để đảm bảo logic phân nhánh đúng

6. **Node "Draft Urgent Reply with AI" (openAi)**:
   - Cấu hình credentials cho OpenAI
   - Chọn model GPT-4o
   - Tùy chỉnh prompt để tạo nháp trả lời phù hợp với phong cách giao tiếp của các sếp

7. **Node "Create Draft in Gmail" (gmail)**:
   - Cấu hình credentials cho tài khoản Gmail
   - Đảm bảo tài khoản có quyền tạo nháp email

8. **Node "Log Urgent Email to Sheets" (googleSheets)**:
   - Cấu hình credentials cho Google Sheets
   - Chọn spreadsheet và sheet đích
   - Kiểm tra các cột dữ liệu được ghi log (có thể thêm/xóa cột tùy theo nhu cầu)

9. **Node "Log Non-Urgent Email to Sheets" (googleSheets)**:
   - Cấu hình credentials cho Google Sheets
   - Chọn spreadsheet và sheet đích
   - Kiểm tra các cột dữ liệu được ghi log (có thể thêm/xóa cột tùy theo nhu cầu)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Gmail và Google Sheets để đảm bảo workflow hoạt động đúng
3. Nếu mọi thứ ổn, click vào nút "Activate" để bật workflow và cho nó chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node để thông báo email khẩn cấp qua Slack hoặc Microsoft Teams
2. **Lưu log chi tiết hơn**: Thêm các trường dữ liệu bổ sung vào Google Sheets như thời gian xử lý, người xử lý...
3. **Tự động gửi báo cáo**: Thiết lập gửi báo cáo hàng ngày/ hàng tuần về số lượng email đã xử lý
4. **Tùy chỉnh nhãn ưu tiên**: Điều chỉnh các nhãn ưu tiên và prompt AI để phù hợp với quy trình làm việc cụ thể của các sếp

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc xử lý email hàng ngày, đồng thời nâng cao hiệu suất làm việc và chuyên nghiệp trong giao tiếp. Hãy áp dụng ngay để trải nghiệm sự thay đổi tích cực trong quy trình làm việc của các sếp!