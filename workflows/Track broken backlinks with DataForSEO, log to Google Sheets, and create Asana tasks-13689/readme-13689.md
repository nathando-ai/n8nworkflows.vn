---
title: "🔗 Theo dõi và xử lý liên kết hỏng với DataForSEO, Google Sheets và Asana"
description: "Tự động hóa việc theo dõi liên kết hỏng, ghi log vào Google Sheets và tạo task trên Asana để tối ưu hóa SEO hiệu quả"
slug: "theo-doi-lien-ket-hong-dataforseo-google-sheets-asana"
tags: [n8n, automation, no-code, seo, dataforseo, google-sheets, asana]
keywords: [n8n workflow, tự động hóa seo, theo dõi liên kết hỏng, dataforseo, google sheets, asana]
---

# 🔗 Theo dõi và xử lý liên kết hỏng với DataForSEO, Google Sheets và Asana

[Các sếp SEO] thường phải tốn nhiều thời gian để theo dõi và xử lý liên kết hỏng trên trang web. Việc này thường phải làm thủ công, dễ gây lỗi và mất thời gian. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình theo dõi liên kết hỏng.
- Chính xác: Dữ liệu được cập nhật liên tục và chính xác từ DataForSEO.
- Cá nhân hóa: Tùy chỉnh được các tham số theo nhu cầu của từng trang web.
- Hoạt động liên tục: Workflow chạy định kỳ theo lịch trình đã đặt.
- Tích hợp hoàn hảo: Kết nối liền mạch giữa DataForSEO, Google Sheets và Asana.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản DataForSEO với API key (đăng ký tại [DataForSEO](https://app.dataforseo.com/api-access)).
- Tài khoản Google với quyền truy cập Google Sheets.
- Tài khoản Asana với Workspace ID, Project ID và Assignee ID.
- Trang web cần theo dõi liên kết hỏng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13689](https://n8n.io/workflows/13689).
2. Click vào nút "Import" để tải file JSON về máy.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get lost backlinks"**:
   - Chọn credentials là "dataForSeoApi".
   - Điền tham số "Target Domain" với tên miền cần theo dõi.
   - Có thể điều chỉnh các tham số khác như "Limit", "Offset", "Filter" theo nhu cầu.

2. **Node "Create spreadsheet"**:
   - Chọn credentials là "googleSheetsOAuth2Api".
   - Điền tham số "Spreadsheet Name" với tên bảng tính mong muốn.
   - Có thể điều chỉnh các tham số khác như "Locale", "Time Zone" theo nhu cầu.

3. **Node "Append row in sheet"**:
   - Chọn credentials là "googleSheetsOAuth2Api".
   - Điền tham số "Spreadsheet ID" với ID của bảng tính đã tạo.
   - Điền tham số "Sheet Name" với tên sheet mong muốn.
   - Có thể điều chỉnh các tham số khác như "Headers", "Data" theo nhu cầu.

4. **Node "Create a task"**:
   - Chọn credentials là "asanaApi".
   - Điền tham số "Workspace ID" với ID của Workspace Asana.
   - Điền tham số "Project ID" với ID của Project Asana.
   - Điền tham số "Assignee ID" với ID của người thực hiện task.
   - Có thể điều chỉnh các tham số khác như "Name", "Notes", "Due Date" theo nhu cầu.

5. **Node "Schedule Trigger"**:
   - Điền tham số "Timezone" với múi giờ mong muốn.
   - Điền tham số "Schedule" với lịch trình chạy workflow (ví dụ: "0 0 * * *" để chạy hàng ngày lúc 00:00).

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test run dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Sheets và Asana.
3. Nếu kết quả đúng, click vào nút "Activate" để bật workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có liên kết hỏng mới.
- Lưu log chi tiết hơn vào Google Sheets, bao gồm thời gian phát hiện, người xử lý, trạng thái xử lý.
- Gửi báo cáo định kỳ về tình trạng liên kết hỏng qua email.

### 📌 Kết luận
Workflow này giúp các sếp SEO tiết kiệm thời gian và công sức trong việc theo dõi và xử lý liên kết hỏng. Với việc tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào các công việc quan trọng hơn. Hãy áp dụng ngay để tối ưu hóa SEO hiệu quả!