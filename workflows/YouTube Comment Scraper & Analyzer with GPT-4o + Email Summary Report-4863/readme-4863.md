---
title: "🚀 Tự động thu thập và phân tích bình luận YouTube với GPT-4o + báo cáo email tổng hợp"
description: "Hướng dẫn tự động hóa thu thập bình luận YouTube, phân tích cảm xúc với AI và gửi báo cáo email tự động - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-thu-thap-phan-tich-binh-luan-youtube-voi-gpt-4o"
tags: [n8n, automation, no-code, AI, marketing, YouTube, Google Sheets, OpenAI]
keywords: [n8n workflow, tự động hóa, YouTube, phân tích cảm xúc, báo cáo email, OpenAI, Google Sheets]
---

# 🚀 Tự động thu thập và phân tích bình luận YouTube với GPT-4o + báo cáo email tổng hợp

[Các sếp đang gặp khó khăn khi phải theo dõi hàng nghìn bình luận trên YouTube thủ công. Phân tích cảm xúc và trích xuất thông tin hữu ích từ hàng trăm bình luận mỗi ngày là một công việc cực kỳ tốn thời gian và dễ gây lỗi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập bình luận đến phân tích cảm xúc và gửi báo cáo email chi tiết - hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân tích hàng nghìn bình luận mỗi ngày
- **Phân tích sâu sắc**: Sử dụng GPT-4o để phân tích cảm xúc và trích xuất thông tin hữu ích
- **Báo cáo tự động**: Nhận báo cáo email chi tiết về tình hình bình luận hàng ngày
- **Dễ dàng theo dõi**: Theo dõi xu hướng bình luận và phản hồi của khán giả một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã tạo và cấu hình
- Tài khoản YouTube với quyền truy cập API
- API Key từ OpenAI (đã đăng ký tài khoản và có credit)
- Tài khoản Gmail để gửi báo cáo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4863](https://n8n.io/workflows/4863)
2. Click vào nút "Import" để tải file JSON workflow
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Trigger**:
   - Tạo một Google Sheet với cấu trúc sau:
     ```
     | ID | Video Title | YouTube Video ID | Status |
     ```
   - Điền "Pending" vào cột Status để kích hoạt phân tích
   - Cấu hình Google Sheets Trigger node với ID của Google Sheet này

2. **YouTube API**:
   - Tạo dự án trong Google Cloud Console và bật YouTube Data API v3
   - Tạo OAuth 2.0 Client ID và cấu hình trong n8n
   - Đảm bảo tài khoản YouTube có quyền truy cập vào các video cần phân tích

3. **OpenAI Chat Model**:
   - Điền API Key từ OpenAI vào credentials
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4o

4. **Gmail Account Configuration**:
   - Cấu hình tài khoản Gmail để gửi báo cáo
   - Đảm bảo tài khoản có quyền truy cập đầy đủ

5. **Google Sheets Update**:
   - Cấu hình node "Update Status on Google Sheet" với ID của Google Sheet đã tạo

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ (Google Sheets, YouTube, OpenAI, Gmail)
2. Chạy test với một video mẫu để đảm bảo workflow hoạt động đúng
3. Bật Active workflow để bắt đầu quá trình tự động hóa

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh phân tích**: Chỉnh sửa prompt trong node AI Agent để phù hợp với nhu cầu phân tích cụ thể
2. **Lọc bình luận**: Thêm node để lọc bình luận theo từ khóa hoặc độ dài trước khi phân tích
3. **Báo cáo định kỳ**: Thiết lập lịch gửi báo cáo hàng ngày/tháng để theo dõi xu hướng
4. **Kết hợp với Slack**: Thêm node để gửi báo cáo đến kênh Slack của nhóm

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ thu thập bình luận YouTube đến phân tích cảm xúc và gửi báo cáo email - tiết kiệm thời gian đáng kể và cung cấp thông tin hữu ích để cải thiện nội dung và tương tác với khán giả. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của nhóm!