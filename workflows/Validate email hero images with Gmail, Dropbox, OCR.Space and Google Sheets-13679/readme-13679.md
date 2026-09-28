---
title: "🚀 Tự động hóa kiểm tra nội dung hình ảnh trong email với n8n"
description: "Hướng dẫn tự động so sánh nội dung hình ảnh trong email với thiết kế mong đợi, tiết kiệm thời gian và đảm bảo chất lượng nội dung"
slug: "tu-dong-hoa-kiem-tra-noi-dung-hinh-anh-email"
tags: [n8n, automation, no-code, email-marketing, document-extraction]
keywords: [n8n workflow, tự động hóa email, kiểm tra hình ảnh, OCR, Google Sheets]
---

# 🚀 Tự động hóa kiểm tra nội dung hình ảnh trong email với n8n

[Các sếp] có bao giờ phải tốn thời gian tải hình ảnh từ email, chạy công cụ OCR và so sánh thủ công với thiết kế mong đợi không? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình kiểm tra hình ảnh
- Đảm bảo chất lượng: So sánh chính xác nội dung hình ảnh với thiết kế mong đợi
- Tăng hiệu suất: Giảm thiểu lỗi do kiểm tra thủ công
- Theo dõi dễ dàng: Kết quả được lưu trữ trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail (để truy cập email)
- Tài khoản Google Sheets (để lưu kết quả)
- API Key từ OCR.Space (để trích xuất văn bản từ hình ảnh)
- Tài khoản Dropbox (để lưu trữ hình ảnh mong đợi)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13679](https://n8n.io/workflows/13679)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get many messages"**:
   - Chọn credentials "gmailOAuth2"
   - Đảm bảo tài khoản Gmail có quyền truy cập vào email cần kiểm tra

2. **Node "Extract Hero Image SRC From HTML"**:
   - Chỉnh sửa code để trích xuất đúng URL hình ảnh từ email HTML
   - Thường cần điều chỉnh selector CSS dựa trên cấu trúc email cụ thể

3. **Node "Convert Image File from HTML to Binary"**:
   - Đảm bảo URL hình ảnh từ email là URL trực tiếp (không yêu cầu đăng nhập)

4. **Node "Convert Image File from Dropbox to Binary"**:
   - Thay thế URL Dropbox trong node với URL hình ảnh mong đợi của các sếp
   - Đảm bảo URL Dropbox là URL truy cập trực tiếp (không yêu cầu đăng nhập)

5. **Node "Extracting Expected Image Content from OCR1" và "Extracting Actual Image Content from OCR"**:
   - Thêm API Key của OCR.Space vào phần headers của HTTP Request
   - Có thể điều chỉnh các tham số OCR như ngôn ngữ, độ chính xác...

6. **Node "Log Image Checks to Excel"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Tạo sheet mới với các cột: SectionId, ExpectedImageURL, ExpectedText, ActualText, Result
   - Cấu hình đúng Spreadsheet ID và Sheet Name

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute workflow" để chạy thử với email mẫu
2. Kiểm tra kết quả trong Google Sheets
3. Sau khi xác nhận hoạt động đúng, bật chế độ "Active" để workflow chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi có sự khác biệt lớn
- Tích hợp với Google Drive để lưu trữ hình ảnh đã kiểm tra
- Thiết lập lịch chạy định kỳ để kiểm tra email hàng ngày
- Kết hợp với workflow khác để tự động gửi báo cáo hàng tuần

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc kiểm tra nội dung hình ảnh email. Bằng cách tự động hóa toàn bộ quá trình, các sếp có thể tập trung vào những công việc quan trọng hơn và đảm bảo chất lượng nội dung email luôn được duy trì cao. Hãy thử ngay và trải nghiệm sự khác biệt!