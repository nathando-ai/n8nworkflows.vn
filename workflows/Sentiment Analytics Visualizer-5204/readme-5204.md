---
title: "📊 Tự động phân tích cảm xúc và tạo biểu đồ từ đánh giá khách hàng với n8n"
description: "Hướng dẫn tự động hóa phân tích cảm xúc từ đánh giá khách hàng, tạo biểu đồ và gửi email báo cáo chỉ trong 10 nodes n8n"
slug: "tu-dong-phan-tich-cam-xuc-tao-bieu-do-tu-danh-gia-khach-hang"
tags: [n8n, automation, no-code, google-sheets, openai, ai]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, google sheets, openai]
---

# 📊 Tự động phân tích cảm xúc và tạo biểu đồ từ đánh giá khách hàng với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân tích cảm xúc từ hàng nghìn đánh giá khách hàng
- Tạo biểu đồ trực quan về phân phối cảm xúc (Positive/Negative/Neutral)
- Gửi báo cáo email tự động với biểu đồ đính kèm
- Tiết kiệm thời gian xử lý dữ liệu thủ công
- Lấy được insight về trải nghiệm khách hàng một cách nhanh chóng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Sheets và Gmail)
- API key OpenAI (để phân tích cảm xúc)
- Google Sheet đã chuẩn bị với dữ liệu đánh giá (cột A: Review title, cột B: Review text)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5204](https://n8n.io/workflows/5204)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Workflow" > "Import from URL"
4. Dán URL của workflow vào ô nhập liệu và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node "Select Google Sheet" và "Read Data from Google Sheet":**
1. Chọn credentials Google Sheets đã cấu hình
2. Thay thế `documentId` bằng ID của Google Sheet chứa dữ liệu đánh giá
3. Chọn sheet chứa dữ liệu đánh giá
4. Đảm bảo sheet có cột A: "Review title" và cột B: "Review text"

**Node "OpenAI Chat Model":**
1. Thêm credentials OpenAI API
2. Model đã được cấu hình là `gpt-4o-mini` (tiết kiệm chi phí)
3. Đảm bảo tài khoản OpenAI có đủ credits

**Node "Send Gmail with Sentiment Chart":**
1. Thay thế địa chỉ email nhận báo cáo
2. Cấu hình credentials Gmail OAuth2
3. Tùy chỉnh tiêu đề và nội dung email theo nhu cầu

**Node "Update Google Sheet":**
1. Đảm bảo sheet có cột C: "Sentiment" để lưu kết quả phân tích

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả ở các node trung gian (Sentiment Analysis, Extract Number of Answers per Sentiment)
3. Sau khi xác nhận hoạt động đúng, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để gửi báo cáo vào kênh Slack của nhóm
- Lưu log kết quả phân tích vào Google Sheets khác để theo dõi lịch sử
- Tự động hóa gửi báo cáo định kỳ hàng tuần/tháng
- Kết hợp với workflow khác để phân tích cảm xúc từ các nguồn khác (Facebook, Twitter, etc.)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc phân tích cảm xúc từ đánh giá khách hàng. Bằng cách tự động hóa quy trình này, các sếp có thể lấy được insight về trải nghiệm khách hàng một cách nhanh chóng và chính xác, từ đó cải thiện dịch vụ và tăng cường sự hài lòng của khách hàng. Hãy thử ngay và xem cách workflow này có thể giúp doanh nghiệp của bạn phát triển!