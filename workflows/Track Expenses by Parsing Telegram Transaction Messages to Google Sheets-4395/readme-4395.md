---
title: "💰 Tự động theo dõi chi tiêu từ Telegram sang Google Sheets - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động lưu trữ và phân tích chi tiêu từ tin nhắn Telegram vào Google Sheets bằng workflow n8n. Tiết kiệm thời gian và tránh lỗi thủ công."
slug: "tu-dong-theo-doi-chi-tieu-telegram-google-sheets"
tags: [n8n, automation, no-code, finance, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa chi tiêu, telegram automation, google sheets api, quản lý tài chính]
---

# 💰 Tự động theo dõi chi tiêu từ Telegram sang Google Sheets - Workflow n8n

[Các sếp đang mệt mỏi với việc ghi chép chi tiêu thủ công? Hãy để workflow n8n giúp bạn tự động hóa quy trình này trong vài phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chép thủ công mỗi giao dịch
- **Dữ liệu chính xác**: Tránh lỗi nhập liệu thủ công
- **Phân tích dễ dàng**: Dữ liệu tự động cập nhật vào Google Sheets
- **Tự động hóa hoàn toàn**: Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- Google Sheets API đã được kích hoạt
- Credentials cho Google Sheets và Telegram API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: [https://n8n.io/workflows/4395](https://n8n.io/workflows/4395)
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger Node**:
   - Chọn credentials cho Telegram API
   - Điền ID của bot Telegram
   - Cấu hình trigger để nhận tin nhắn từ bot

2. **Code Node (transactions)**:
   - Chỉnh sửa hàm xử lý tin nhắn để trích xuất thông tin chi tiêu
   - Đảm bảo hàm trả về đối tượng với các trường: amount, category, date, description

3. **If Node**:
   - Cấu hình điều kiện để lọc các tin nhắn liên quan đến chi tiêu
   - Ví dụ: `{{ $node["transactions"].json["isExpense"] }} === true`

4. **Google Sheets Node**:
   - Chọn credentials cho Google Sheets API
   - Điền Spreadsheet ID và tên Sheet cần ghi dữ liệu
   - Cấu hình các cột tương ứng với dữ liệu từ tin nhắn

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets
3. Bật "Active" để workflow chạy tự động khi có tin nhắn mới

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Email để nhận thông báo khi có giao dịch mới
- Tích hợp với các công cụ phân tích như Google Data Studio
- Tự động phân loại chi tiêu bằng AI (sử dụng node LLM)
- Thiết lập báo cáo định kỳ từ dữ liệu trong Google Sheets

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý chi tiêu hàng ngày. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào những việc quan trọng hơn trong công việc. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!