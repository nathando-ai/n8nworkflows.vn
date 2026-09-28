---
title: "🔄 Đồng bộ danh bạ Google Sheets sang SeaTable với logic cập nhật/chèn tự động"
description: "Hướng dẫn tự động hóa đồng bộ danh bạ từ Google Sheets sang SeaTable với logic cập nhật/chèn thông minh, tiết kiệm thời gian và đảm bảo dữ liệu luôn đồng bộ"
slug: "dong-bo-danh-ba-google-sheets-sang-seatable"
tags: [n8n, automation, no-code, crm, seatable, google-sheets]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, google sheets, seatable]
---

# 🔄 Đồng bộ danh bạ Google Sheets sang SeaTable với logic cập nhật/chèn tự động

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc đồng bộ dữ liệu thủ công
- Đảm bảo dữ liệu luôn đồng bộ giữa Google Sheets và SeaTable
- Tự động cập nhật thông tin liên hệ mới và thay đổi
- Giảm thiểu lỗi nhập liệu do thủ công
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản SeaTable Cloud đang hoạt động
- API Token từ SeaTable
- Google Sheets ID của danh bạ cần đồng bộ
- n8n phiên bản 1.105.2 trở lên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7691)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "settings"**:
   - Thay thế giá trị `googleSheetId` bằng ID của Google Sheet chứa danh bạ của bạn
   - Để tìm ID: Mở Google Sheet → URL sẽ có dạng `https://docs.google.com/spreadsheets/d/GOOGLE_SHEET_ID/edit`

2. **Node "seatablelookup"**:
   - Cấu hình credentials "seaTableApi"
   - Đảm bảo bảng SeaTable có các trường: email, firstname, lastname, company

3. **Node "Create a row" và "Update a row"**:
   - Cấu hình credentials "seaTableApi"
   - Đảm bảo các trường dữ liệu được ánh xạ đúng với cấu trúc bảng SeaTable

4. **Node "contacts"**:
   - Cấu hình credentials "googleSheetsOAuth2Api"
   - Đảm bảo Google Sheet có các trường: email, firstname, lastname, company

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả đồng bộ trên SeaTable
3. Sau khi xác nhận hoạt động đúng, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa định kỳ**: Thêm node "Schedule Trigger" để chạy workflow theo lịch định kỳ (ví dụ: hàng ngày lúc 9h sáng)
2. **Thông báo kết quả**: Kết nối với Slack/Telegram để nhận thông báo khi workflow hoàn thành
3. **Lưu log hoạt động**: Thêm node "File" để lưu log các lần chạy workflow
4. **Xử lý lỗi**: Thêm node "Error Trigger" để xử lý các trường hợp lỗi trong quá trình đồng bộ

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc đồng bộ danh bạ giữa Google Sheets và SeaTable. Với logic cập nhật/chèn thông minh, dữ liệu luôn được đồng bộ chính xác và liên tục. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!