---
title: "📄 Tự động hóa trích xuất PDF và gửi tóm tắt qua email với CoreNexis OCR + GPT-4.1-mini + GPT-4o-mini"
description: "Giải pháp tự động hóa hoàn chỉnh giúp các sếp trích xuất văn bản từ PDF, tạo tóm tắt thông minh bằng AI và gửi email chuyên nghiệp chỉ trong vài bước đơn giản."
slug: "tu-dong-hoa-trich-xuat-pdf-va-gui-tom-tat-email"
tags: [n8n, automation, no-code, ai, document-processing]
keywords: [n8n workflow, tự động hóa tài liệu, xử lý PDF, tóm tắt AI, gửi email tự động]
---

# 📄 Tự động hóa trích xuất PDF và gửi tóm tắt qua email với CoreNexis OCR + GPT-4.1-mini + GPT-4o-mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý tài liệu từ 80% trở lên
- Tạo tóm tắt chuyên nghiệp với 5 phần cấu trúc rõ ràng
- Tự động hóa hoàn toàn quy trình từ trích xuất đến gửi email
- Hỗ trợ xử lý hàng loạt tài liệu PDF một cách hiệu quả
- Gửi email định dạng HTML chuyên nghiệp với thương hiệu của doanh nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản CoreNexis API (lấy tại [api.corenexis.com](https://api.corenexis.com))
- Tài khoản OpenAI với quyền truy cập GPT-4.1-mini và GPT-4o-mini
- Tài khoản Gmail với quyền truy cập OAuth2
- Tài liệu PDF mẫu để test workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15956](https://n8n.io/workflows/15956)
2. Chọn "Import" và dán JSON workflow vào n8n Editor
3. Hoặc tải file JSON về máy và import từ n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 3. HTTP — CoreNexis OCR Submit**:
   - Thay thế `YOUR_CORENEXIS_API_KEY` bằng API key của bạn
   - Đảm bảo endpoint URL chính xác: `https://api.corenexis.com/v1/ocr`

2. **Node 6. HTTP — Poll OCR Status**:
   - Thay thế `YOUR_CORENEXIS_API_KEY` bằng API key của bạn
   - Đảm bảo endpoint URL chính xác: `https://api.corenexis.com/v1/ocr/jobs/{{$node["3. HTTP — CoreNexis OCR Submit"].json["job_id"]}}`

3. **Node OpenAI — GPT-4.1-mini Model**:
   - Kết nối credential OpenAI API của bạn
   - Đảm bảo model được chọn là `gpt-4.1-mini`

4. **Node OpenAI — GPT-4o-mini Model**:
   - Kết nối credential OpenAI API của bạn
   - Đảm bảo model được chọn là `gpt-4o-mini`

5. **Node 17. Gmail — Send Summary Email**:
   - Kết nối credential Gmail OAuth2 của bạn
   - Cấu hình email gửi (From, Subject) theo yêu cầu của doanh nghiệp

#### 3. Kích hoạt ⚡️
1. Test run với tài liệu PDF mẫu
2. Kiểm tra email nhận được để xác nhận nội dung tóm tắt
3. Bật Active workflow sau khi test thành công

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý hàng loạt tài liệu**: Sử dụng node "Loop Over Items" để xử lý nhiều file PDF cùng lúc
2. **Lưu trữ tóm tắt**: Thêm node Google Drive để lưu bản tóm tắt dưới dạng PDF
3. **Thông báo Slack**: Kết nối thêm node Slack để nhận thông báo khi xử lý hoàn thành
4. **Lịch sử xử lý**: Thêm node Database để lưu lại lịch sử xử lý tài liệu

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa xử lý tài liệu PDF, từ trích xuất văn bản đến tạo tóm tắt thông minh và gửi email chuyên nghiệp. Với cấu hình đơn giản và hiệu suất cao, các sếp có thể tiết kiệm thời gian đáng kể trong công việc hàng ngày. Hãy thử nghiệm ngay và nâng cao năng suất làm việc của đội ngũ!