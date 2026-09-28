---
title: "🚀 Tự động hóa tạo ảnh AI với FLUX Kontext, Google Sheets và Drive - Giải pháp 100% không code"
description: "Hướng dẫn chi tiết cách tự động hóa tạo ảnh AI với FLUX Kontext, lưu kết quả vào Google Drive và cập nhật URL vào Google Sheets - giải pháp tiết kiệm thời gian 90% cho các sếp thiết kế và marketing"
slug: "tu-dong-hoa-tao-anh-ai-flux-kontext-google-sheets-drive"
tags: [n8n, automation, no-code, ai, google-drive, google-sheets]
keywords: [n8n workflow, tự động hóa tạo ảnh, flux kontext, google sheets, google drive]
---

# 🚀 Tự động hóa tạo ảnh AI với FLUX Kontext, Google Sheets và Drive - Giải pháp 100% không code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp thiết kế và marketing khi phải tạo hàng loạt ảnh AI thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **90% thời gian** tạo ảnh AI thủ công
- Tự động hóa hoàn toàn quy trình từ tạo ảnh đến lưu trữ
- Dữ liệu được đồng bộ tự động giữa Google Sheets và Google Drive
- Tạo hàng loạt ảnh với cùng một prompt hoặc nhiều prompt khác nhau
- Tích hợp dễ dàng với các công cụ thiết kế khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets và Google Drive
- API Key từ [fal.ai](https://fal.ai/)
- Google Sheet mẫu đã được chuẩn bị theo [hướng dẫn này](https://docs.google.com/spreadsheets/d/1N1Yg7FA4tQ8mDll5HLKqwPBuHj31AGDKwzAOg8mLQKs/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/4916)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Create Image"**:
   - Cấu hình credentials "Header Auth":
     - Name: "Authorization"
     - Value: "Key YOURAPIKEY" (thay YOURAPIKEY bằng API Key thực tế từ fal.ai)

2. **Node "Get new image" và "Update result"**:
   - Cấu hình credentials "Google Sheets OAuth2 API"
   - Điền thông tin Sheet ID và tên sheet từ Google Sheet mẫu

3. **Node "Upload Image"**:
   - Cấu hình credentials "Google Drive OAuth2 API"
   - Chọn thư mục lưu trữ trong Google Drive

4. **Node "Schedule Trigger" (tùy chọn)**:
   - Thiết lập thời gian chạy tự động (mặc định 5 phút/lần)

#### 3. Kích hoạt ⚡️
1. Test workflow bằng cách click "Test workflow" (node "When clicking ‘Test workflow’")
2. Kiểm tra kết quả trong Google Sheet và Google Drive
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Slack" hoặc "Email" để nhận thông báo khi workflow hoàn thành
- Tích hợp với các công cụ thiết kế như Canva để tự động tạo template từ ảnh đã tạo
- Thiết lập nhiều workflow khác nhau với các prompt khác nhau cho các mục đích khác nhau
- Sử dụng node "Wait" để tránh bị giới hạn API của FLUX Kontext

### 📌 Kết luận
Workflow này giúp các sếp thiết kế và marketing tiết kiệm thời gian đáng kể trong việc tạo ảnh AI hàng loạt. Bằng cách tự động hóa quy trình từ tạo ảnh đến lưu trữ, các sếp có thể tập trung vào công việc sáng tạo hơn. Hãy thử ngay và trải nghiệm sự khác biệt!