---
title: "🚀 Tự động hóa ưu tiên giao hàng thông minh với Google Gemini và Google Sheets"
description: "Hướng dẫn tự động hóa quy trình ưu tiên giao hàng bằng AI Gemini và Google Sheets, tiết kiệm thời gian và tối ưu hóa quy trình vận hành"
slug: "tu-dong-hoa-uu-tien-giao-hang-google-gemini-sheets"
tags: [n8n, automation, no-code, google-sheets, ai]
keywords: [n8n workflow, tự động hóa giao hàng, google sheets, ai gemini, quản lý vận chuyển]
---

# 🚀 Tự động hóa ưu tiên giao hàng thông minh với Google Gemini và Google Sheets

[Các sếp đang gặp khó khăn khi phải phân loại hàng trăm đơn hàng hàng ngày một cách thủ công. Workflow này sẽ giúp các sếp tự động hóa quy trình này bằng công nghệ AI Gemini và Google Sheets, tiết kiệm thời gian và tối ưu hóa quy trình vận hành.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại hàng nghìn đơn hàng mỗi ngày với độ chính xác cao
- Tiết kiệm thời gian đáng kể cho đội ngũ vận hành
- Tối ưu hóa quy trình giao hàng dựa trên dữ liệu thực tế
- Hiển thị thông tin giao hàng trực quan trên màn hình
- Tích hợp hoàn hảo với hệ thống Google Sheets hiện tại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini Flash 2.5 được kích hoạt
- Google Sheets chứa dữ liệu đơn hàng với các cột: idEnvio, fechaOrden, nombre, direccion, detalle và enviado
- API Key cho Google Sheets
- Quyền truy cập vào Google Sheets để chỉnh sửa
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" trong thanh công cụ
3. Dán link sau vào ô nhập liệu: https://n8n.io/workflows/7296
4. Nhấn "Import" để tải workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Button" (webhook)**:
   - Thay đổi tham số "path" thành đường dẫn mong muốn cho webhook của bạn
   - Ví dụ: `/shipping-priority`

2. **Node "Gemini Flash 2.5" (lmChatGoogleGemini)**:
   - Thêm credentials cho Google Cloud với API Gemini Flash 2.5
   - Đảm bảo tài khoản có đủ quyền truy cập và quota

3. **Node "Shipping" (googleSheetsTool)**:
   - Thêm credentials cho Google Sheets
   - Cấu hình tham số:
     - Spreadsheet ID: ID của Google Sheets chứa dữ liệu đơn hàng
     - Sheet Name: Tên sheet chứa dữ liệu đơn hàng
     - Range: Phạm vi dữ liệu cần đọc (ví dụ: "A1:F1000")

4. **Node "Update" (googleSheets)**:
   - Đảm bảo credentials giống với node "Shipping"
   - Cấu hình tham số:
     - Spreadsheet ID: ID của Google Sheets
     - Sheet Name: Tên sheet cần cập nhật
     - Range: Phạm vi dữ liệu cần cập nhật

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra với dữ liệu mẫu
2. Kiểm tra kết quả trên màn hình hiển thị (node "Screen")
3. Sau khi xác nhận hoạt động đúng, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node để gửi thông báo khi có đơn hàng ưu tiên
2. **Báo cáo định kỳ**: Thêm node để xuất báo cáo hàng ngày về đơn hàng đã xử lý
3. **Xử lý ngoại lệ**: Thêm logic để xử lý các trường hợp ngoại lệ trong dữ liệu đơn hàng
4. **Tối ưu hóa**: Thử nghiệm với các mô hình Gemini khác để tìm ra mô hình phù hợp nhất

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình phân loại đơn hàng, tiết kiệm thời gian và giảm thiểu lỗi con người. Bằng cách tích hợp AI Gemini và Google Sheets, các sếp có thể tối ưu hóa quy trình vận hành và nâng cao hiệu suất giao hàng. Hãy áp dụng ngay để thấy kết quả ngay lập tức!