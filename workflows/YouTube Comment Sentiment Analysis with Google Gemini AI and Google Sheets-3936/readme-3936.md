---
title: "🚀 Phân tích cảm xúc bình luận YouTube với Google Gemini AI và Google Sheets"
description: "Tự động hóa phân tích cảm xúc bình luận YouTube bằng công nghệ AI tiên tiến, lưu kết quả vào Google Sheets và tạo biểu đồ trực quan"
slug: "phan-tich-cam-xuc-binh-luan-youtube-voi-gemini-ai-va-google-sheets"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, youtube comment, google sheets]
---

# 🚀 Phân tích cảm xúc bình luận YouTube với Google Gemini AI và Google Sheets

[Các sếp] có biết rằng mỗi bình luận trên YouTube đều chứa một thế giới cảm xúc? Với workflow này, các sếp có thể tự động hóa việc phân tích cảm xúc của hàng nghìn bình luận chỉ trong vài bước đơn giản, giúp đưa ra quyết định marketing thông minh hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích tự động**: Xử lý hàng nghìn bình luận trong vài phút
- **Dữ liệu chính xác**: Sử dụng công nghệ AI tiên tiến của Google Gemini
- **Báo cáo trực quan**: Tạo biểu đồ cảm xúc từ dữ liệu phân tích
- **Tích hợp hoàn hảo**: Lưu kết quả vào Google Sheets để dễ dàng chia sẻ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud Platform với API Google Sheets và Google Gemini được kích hoạt
- Google Sheets API Key và Credentials
- ID Video YouTube cần phân tích
- Tài khoản n8n đã cài đặt các node cần thiết (LangChain, Google Sheets, HTTP Request)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/3936)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get API Comments"**:
   - Cấu hình Google Sheets API credentials
   - Điền ID Video YouTube cần phân tích vào trường "videoId"

2. **Node "Google Gemini"**:
   - Cấu hình Google Cloud Platform credentials
   - Đảm bảo API Google Gemini đã được kích hoạt

3. **Node "Save comments" và "Update sentiment"**:
   - Chỉnh sửa ID Google Sheet và tên sheet phù hợp với tài khoản của các sếp
   - Đảm bảo tài khoản có quyền truy cập vào Google Sheet

4. **Node "QuickChart"**:
   - Có thể tùy chỉnh màu sắc và kiểu biểu đồ theo ý thích

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để chạy thử với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa định kỳ**: Thêm node Schedule Trigger để chạy phân tích tự động hàng ngày
2. **Thông báo kết quả**: Kết nối với Slack/Telegram để nhận báo cáo cảm xúc qua tin nhắn
3. **Phân tích sâu hơn**: Sử dụng node Code để thêm các chỉ số phân tích nâng cao
4. **Xử lý dữ liệu lớn**: Tăng số lượng batch trong node "Loop Over Comments" nếu xử lý nhiều bình luận

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian đáng kể mà còn mang lại cái nhìn sâu sắc về cảm xúc của khán giả. Với kết hợp của công nghệ AI tiên tiến và công cụ quản lý dữ liệu quen thuộc như Google Sheets, các sếp có thể đưa ra quyết định marketing thông minh hơn, nâng cao trải nghiệm người xem và tăng tương tác với nội dung.

Hãy thử ngay và biến dữ liệu bình luận thành nguồn thông tin vàng cho chiến lược marketing của các sếp!