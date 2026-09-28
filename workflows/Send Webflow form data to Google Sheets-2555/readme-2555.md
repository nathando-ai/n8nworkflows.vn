---
title: "🚀 Tự động lưu dữ liệu form Webflow vào Google Sheets - Giải pháp không code hoàn hảo"
description: "Hướng dẫn tự động hóa lưu trữ dữ liệu form Webflow vào Google Sheets bằng n8n, tiết kiệm thời gian và đảm bảo dữ liệu luôn được cập nhật ngay lập tức"
slug: "tu-dong-luu-du-lieu-form-webflow-vao-google-sheets"
tags: [n8n, automation, no-code, webflow, google-sheets]
keywords: [n8n workflow, tự động hóa form, lưu dữ liệu webflow, google sheets api, không code]
---

# 🚀 Tự động lưu dữ liệu form Webflow vào Google Sheets - Giải pháp không code hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có sử dụng Webflow để thu thập dữ liệu từ khách hàng thông qua các form nhưng lại phải tốn thời gian nhập tay vào Google Sheets? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian nhập liệu thủ công
- Dữ liệu luôn được cập nhật ngay lập tức
- Tự động tạo cột mới khi có dữ liệu mới
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Webflow với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets API
- Biết cách lấy Client ID và Client Secret từ Webflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "On Form Submission" (webflowTrigger)**:
   - Chọn credentials "webflowOAuth2Api"
   - Đảm bảo đã disable legacy API trong Webflow
   - Cấu hình webhook để nhận dữ liệu form

2. **Node "Prepare Fields" (code)**:
   - Sử dụng đoạn code sau để chuẩn bị dữ liệu:
     ```javascript
     const data = {
       ...$input.all()[0].json,
       date: new Date().toISOString()
     };
     return data;
     ```

3. **Node "Append New Row" (googleSheets)**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Chọn operation "append"
   - Điền thông tin Spreadsheet ID và Sheet Name
   - Đảm bảo Google Sheets có quyền truy cập đầy đủ

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có dữ liệu mới
- Thêm node để gửi email báo cáo hàng ngày
- Tự động phân loại dữ liệu vào các sheet khác nhau dựa trên loại form

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình thu thập và lưu trữ dữ liệu từ Webflow vào Google Sheets mà không cần viết một dòng code. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả làm việc!