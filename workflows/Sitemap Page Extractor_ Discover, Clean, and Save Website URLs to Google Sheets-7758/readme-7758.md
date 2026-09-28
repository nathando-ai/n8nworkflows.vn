---
title: "🚀 Tự động trích xuất URL từ Sitemap và lưu vào Google Sheets - Giải pháp SEO không cần code"
description: "Hướng dẫn tự động hóa trích xuất URL từ sitemap của website và lưu vào Google Sheets bằng n8n. Tiết kiệm thời gian SEO và tối ưu hóa công việc nghiên cứu thị trường."
slug: "tu-dong-trich-xuat-url-tu-sitemap-luu-google-sheets"
tags: [n8n, automation, no-code, seo, google-sheets]
keywords: [n8n workflow, tự động hóa, trích xuất sitemap, google sheets, seo]
---

# 🚀 Tự động trích xuất URL từ Sitemap và lưu vào Google Sheets - Giải pháp SEO không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải làm thủ công việc trích xuất hàng trăm URL từ sitemap của website. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động trích xuất hàng trăm URL trong vài phút thay vì làm thủ công.
- Chính xác: Lọc bỏ các URL không cần thiết (như sitemap.xml) để chỉ giữ lại URL nội dung thực sự.
- Cá nhân hóa: Lưu kết quả vào Google Sheets của riêng bạn để quản lý và phân tích.
- Hoạt động liên tục: Chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets.
- API Key hoặc OAuth2 Credentials cho Google Sheets (đã được cấu hình trong n8n).
- URL của website bạn muốn trích xuất sitemap.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7758](https://n8n.io/workflows/7758)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Input Website URL" (formTrigger)**:
   - Không cần cấu hình gì thêm, đây là node bắt đầu workflow.

2. **Node "Prepare website URL" (set)**:
   - Kiểm tra biểu thức trong node này đã chuẩn bị URL đúng định dạng chưa.
   - Ví dụ: `https://example.com` thay vì `example.com`.

3. **Node "Save Page URLs to Sheet" (googleSheets)**:
   - Chọn đúng Google Sheets OAuth2 Credentials đã được cấu hình trong n8n.
   - Điền thông tin:
     - **Spreadsheet ID**: ID của Google Sheet bạn muốn lưu kết quả.
     - **Sheet Name**: Tên sheet trong Google Sheet (ví dụ: "List_Of_All_URLs").
     - **Operation**: Chọn "Append or Update" để thêm mới hoặc cập nhật URL đã tồn tại.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu.
2. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động vào Google Sheets để theo dõi lịch sử trích xuất.
- Gửi báo cáo định kỳ (hàng tuần/hàng tháng) về số lượng URL mới được trích xuất.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc trích xuất và quản lý URL từ sitemap. Hãy áp dụng ngay để tối ưu hóa công việc SEO và nghiên cứu thị trường!