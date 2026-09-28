---
title: "🚀 Tự động hóa phân tích nội dung website với GPT-4 và lưu vào Google Sheets"
description: "Workflow n8n tự động hóa 100% không cần code để phân tích nội dung website, tổng hợp thông tin quan trọng và lưu kết quả vào Google Sheets"
slug: "tu-dong-hoa-phan-tich-noi-dung-website-voi-gpt-4-va-luu-vao-google-sheets"
tags: [n8n, automation, no-code, AI, marketing]
keywords: [n8n workflow, tự động hóa, phân tích nội dung, GPT-4, Google Sheets]
---

# 🚀 Tự động hóa phân tích nội dung website với GPT-4 và lưu vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc phân tích nội dung website
- Tự động hóa quy trình tổng hợp thông tin quan trọng từ nội dung dài
- Lưu trữ kết quả phân tích một cách có cấu trúc trong Google Sheets
- Tích hợp AI thông minh để trích xuất thông tin chính xác
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key từ OpenAI để sử dụng GPT-4
- URL của website cần phân tích
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4355](https://n8n.io/workflows/4355)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Click to Start" (manualTrigger)**:
   - Không cần cấu hình gì, chỉ cần click để kích hoạt workflow

2. **Node "Input Your Website URL" (httpRequest)**:
   - Chỉnh sửa URL trong phần "Request URL" để trỏ đến website cần phân tích
   - Đảm bảo website cho phép truy cập từ n8n (không bị chặn bởi robots.txt)

3. **Node "Process the Markdown to readable Contents" (openAi)**:
   - Thêm credentials cho OpenAI bằng cách:
     - Click vào biểu tượng bánh răng ở góc trên bên phải của node
     - Chọn "Add Credential" và chọn "OpenAI API"
     - Nhập API Key của bạn
   - Tùy chỉnh prompt trong phần "Prompt" nếu cần thay đổi cách xử lý nội dung

4. **Node "Save the Website Scraping content to Google Sheet" (googleSheets)**:
   - Thêm credentials cho Google Sheets:
     - Click vào biểu tượng bánh răng ở góc trên bên phải của node
     - Chọn "Add Credential" và chọn "Google Sheets OAuth2 API"
     - Theo dõi hướng dẫn để xác thực tài khoản Google
   - Chọn spreadsheet và worksheet đích trong phần "Resource"
   - Map các cột trong Google Sheets với dữ liệu đầu ra từ node trước đó

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" ở góc trên bên phải của workflow
2. Để test workflow, click vào nút "Execute Workflow" ở góc trên bên phải
3. Kiểm tra kết quả trong Google Sheets của bạn

### ✍️ Mẹo & gợi ý nâng cao
1. **Lập lịch tự động chạy**: Sử dụng node "Schedule Trigger" để tự động chạy workflow theo lịch trình cụ thể
2. **Thêm thông báo**: Kết nối với Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành
3. **Xử lý nhiều URL**: Sử dụng node "Split In Batches" để xử lý nhiều URL cùng lúc
4. **Lưu log**: Thêm node "File" để lưu log của quá trình xử lý

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc phân tích nội dung website. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong công việc hàng ngày. Hãy thử áp dụng ngay để nâng cao hiệu suất làm việc của mình!