---
title: "🚀 Tự động gửi email cảnh báo nhiệm vụ khẩn cấp từ Google Sheets và Gmail"
description: "Hướng dẫn tự động hóa gửi email cảnh báo khi có nhiệm vụ khẩn cấp trong Google Sheets, tiết kiệm thời gian và tránh quên nhiệm vụ quan trọng."
slug: "tu-dong-gui-email-canh-bao-nhiem-vu-khan-cap"
tags: [n8n, automation, no-code, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa, google sheets, gmail, email cảnh báo]
---

# 🚀 Tự động gửi email cảnh báo nhiệm vụ khẩn cấp từ Google Sheets và Gmail

[Các sếp đang làm việc với nhiều nhiệm vụ hàng ngày trên Google Sheets? Bạn có bao giờ quên gửi email cảnh báo cho đồng nghiệp về nhiệm vụ khẩn cấp? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ theo dõi Google Sheets đến gửi email cảnh báo chỉ trong vài phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi Google Sheets liên tục.
- Chính xác: Email cảnh báo được gửi chỉ khi có nhiệm vụ khẩn cấp.
- Cá nhân hóa: Email chứa thông tin chi tiết về nhiệm vụ (tên, người phụ trách, hạn chót...).
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets và Gmail.
- Google Sheets đã được cấu hình với các cột: Priority, Notified, Task name, Owner, Deadline, Status, Action required.
- Tài khoản n8n đã được kết nối với Google Sheets và Gmail.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [https://n8n.io/workflows/9324](https://n8n.io/workflows/9324)
2. Chọn "Copy to clipboard" để sao chép JSON workflow.
3. Trong n8n Editor, chọn "Import from Clipboard" và dán JSON đã sao chép.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger when Urgent status** (googleSheetsTrigger):
   - Chọn credentials: `googleSheetsTriggerOAuth2Api`.
   - Cấu hình trigger theo dõi thay đổi trong cột "Priority".
   - Chọn Google Sheets và bảng dữ liệu chứa nhiệm vụ.

2. **Get the row number** (googleSheets):
   - Chọn credentials: `googleSheetsOAuth2Api`.
   - Cấu hình truy vấn để lấy số hàng của nhiệm vụ khẩn cấp.

3. **Condition to send the email** (if):
   - Thiết lập điều kiện:
     - Priority = "Urgent"
     - Notified is empty
     - row_number exists

4. **Email alert** (gmail):
   - Chọn credentials: `gmailOAuth2`.
   - Cấu hình email với các thông tin cá nhân hóa:
     - Task name: `{{ $json.task_name }}`
     - Owner: `{{ $json.owner }}`
     - Deadline: `{{ $json.deadline }}`
     - Status: `{{ $json.status }}`
     - Action required: `{{ $json.action_required }}`

5. **Update row avoiding spam** (googleSheets):
   - Chọn credentials: `googleSheetsOAuth2Api`.
   - Cấu hình cập nhật cột "Notified" thành "Yes" hoặc timestamp.
   - Sử dụng tham số `row_number = {{ $json.row_number }}`.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo ngay lập tức.
- Lưu log các email đã gửi để theo dõi lịch sử.
- Gửi báo cáo định kỳ về các nhiệm vụ đã hoàn thành.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc gửi email cảnh báo nhiệm vụ khẩn cấp từ Google Sheets, tiết kiệm thời gian và tránh quên nhiệm vụ quan trọng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!