---
title: "🚀 Theo dõi tiến độ công trình bằng AI Gemini + Google Drive & Sheets"
description: "Tự động hóa theo dõi tiến độ xây dựng bằng AI Gemini, lưu kết quả vào Google Sheets và gửi báo cáo qua email - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "theo-doi-tien-do-xay-dung-ai-gemini"
tags: [n8n, automation, no-code, google-drive, google-sheets, ai]
keywords: [n8n workflow, tự động hóa, AI Gemini, quản lý dự án, theo dõi tiến độ]
---

# 🚀 Theo dõi tiến độ công trình bằng AI Gemini + Google Drive & Sheets

[Các sếp xây dựng đang gặp khó khăn khi phải kiểm tra thủ công hàng chục ảnh công trình hàng ngày, ghi chép kết quả vào bảng tính và gửi báo cáo cho các bên liên quan. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, giảm thiểu sai sót và tiết kiệm thời gian đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công mỗi ngày
- **Chính xác cao**: AI Gemini phân tích hình ảnh với độ chính xác 90%+
- **Theo dõi dễ dàng**: Kết quả được lưu tự động vào Google Sheets
- **Báo cáo chuyên nghiệp**: Email báo cáo tự động với hình ảnh và phân tích
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive chứa ảnh công trình
- Tài khoản Google Sheets để lưu kết quả
- API Key từ Google Cloud (cho Google Drive và Google Gemini)
- Tài khoản email SMTP để gửi báo cáo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6742](https://n8n.io/workflows/6742)
2. Click "Import" và chọn "Import from URL"
3. Hoặc copy toàn bộ JSON workflow và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "List a file" (Google Drive)**:
   - Chọn credentials Google API
   - Điền ID thư mục chứa ảnh công trình
   - Thiết lập bộ lọc để chỉ lấy ảnh mới (ví dụ: chỉ lấy ảnh trong 24h qua)

2. **Node "Google Gemini"**:
   - Chọn credentials Google Palm API
   - Đặt prompt phân tích hình ảnh (ví dụ: "Phân tích tiến độ xây dựng từ hình ảnh này, bao gồm các phần đã hoàn thành, đang thi công và chưa bắt đầu")

3. **Node "Append data to a sheet" (Google Sheets)**:
   - Chọn credentials Google API
   - Điền ID bảng tính và tên sheet
   - Thiết lập cột dữ liệu (ví dụ: ngày, tên ảnh, phân tích AI, đường dẫn ảnh)

4. **Node "Send email"**:
   - Chọn credentials SMTP
   - Điền địa chỉ email người nhận
   - Thiết lập template email với biến {{ $node["AI Analysis"].json.summary }}

#### 3. Kích hoạt ⚡️
1. Test run với 1-2 ảnh mẫu
2. Kiểm tra kết quả trong Google Sheets
3. Bật Active workflow và thiết lập lịch chạy hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo tức thời
- Thêm node lưu log để theo dõi lịch sử phân tích
- Tạo báo cáo định kỳ (tuần/tháng) với tổng hợp dữ liệu
- Kết nối với hệ thống quản lý dự án để cập nhật tiến độ

### 📌 Kết luận
Workflow này giúp các sếp xây dựng tiết kiệm thời gian đáng kể trong việc theo dõi tiến độ công trình. Với sự kết hợp của AI Gemini và Google Workspace, các sếp có thể nhận được báo cáo chuyên nghiệp hàng ngày mà không cần can thiệp thủ công. Hãy áp dụng ngay để nâng cao hiệu quả quản lý dự án!