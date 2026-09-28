---
title: "📄 Chuyển đổi PDF thành Google Doc sạch với Mistral OCR - Tự động hóa hoàn toàn"
description: "Hướng dẫn chi tiết cách tự động chuyển đổi PDF thành Google Doc sạch với Mistral OCR và n8n, tiết kiệm thời gian và đảm bảo chất lượng nội dung"
slug: "chuyen-doi-pdf-thanh-google-doc-sach-voi-mistral-ocr"
tags: [n8n, automation, no-code, document-extraction, multimodal-ai]
keywords: [n8n workflow, tự động hóa, OCR, Mistral, Google Docs]
---

# 📄 Chuyển đổi PDF thành Google Doc sạch với Mistral OCR - Tự động hóa hoàn toàn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý PDF lên đến 90%
- Đảm bảo chất lượng nội dung sau khi chuyển đổi
- Tự động hóa hoàn toàn quy trình chuyển đổi PDF
- Tích hợp liền mạch với Google Docs
- Xử lý cả văn bản và hình ảnh trong PDF
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mistral Cloud API
- Tài khoản Google Docs API
- Tài khoản OpenRouter API (cho LLM)
- Google Drive Folder ID để lưu kết quả
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/6937)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **On form submission** node:
   - Cấu hình form với 2 trường: PDF file upload và tên tài liệu

2. **Upload • PDF to Mistral** node:
   - Kết nối với credentials Mistral Cloud API
   - Đảm bảo API key có quyền upload file

3. **Create • Google Doc** node:
   - Kết nối với credentials Google Docs OAuth2 API
   - Thêm Google Drive Folder ID vào tham số "parent"

4. **LLM Model • GPT-4.1-mini** node:
   - Kết nối với credentials OpenRouter API
   - Đảm bảo tài khoản có đủ credit để sử dụng mô hình này

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu với một file PDF nhỏ
2. Kiểm tra kết quả trong Google Drive folder đã chỉ định
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. Tùy chỉnh prompt trong node "Clean • Markdown Text" để điều chỉnh mức độ làm sạch nội dung
2. Kết nối thêm node gửi email thông báo khi quy trình hoàn thành
3. Thêm node lưu log hoạt động vào Google Sheets để theo dõi lịch sử chuyển đổi
4. Tích hợp với Slack để nhận thông báo tức thời khi có file mới được xử lý

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc chuyển đổi PDF thành Google Doc sạch, tự động hóa hoàn toàn quy trình và đảm bảo chất lượng nội dung. Với các sếp có nhu cầu xử lý hàng loạt file PDF, đây là công cụ không thể thiếu để tiết kiệm thời gian và nâng cao hiệu suất làm việc.