---
title: "🎥 Tự động hóa nội dung từ transcript cuộc họp với Fathom, GPT-4 & DALL-E"
description: "Hướng dẫn tự động hóa 100% không cần code để chuyển đổi transcript cuộc họp thành nội dung đa dạng: video, hình ảnh và bài viết - tiết kiệm thời gian và nâng cao hiệu quả nội dung"
slug: "tu-dong-hoa-noi-dung-tu-transcript-cuoc-hop"
tags: [n8n, automation, no-code, content-creation, ai-content]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo nội dung, transcript cuộc họp, video từ văn bản, hình ảnh từ văn bản]
---

# 🎥 Tự động hóa nội dung từ transcript cuộc họp với Fathom, GPT-4 & DALL-E

[Các sếp] có bao giờ phải tốn hàng giờ để chuyển đổi transcript cuộc họp thành nội dung đa dạng (video, hình ảnh, bài viết) không? Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này với công nghệ AI tiên tiến - tiết kiệm thời gian và nâng cao chất lượng nội dung.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quy trình chuyển đổi transcript (từ 2-5 tiếng thành 5 phút)
- **Nội dung chuyên nghiệp**: Tạo ra video chất lượng, hình ảnh đẹp mắt và bài viết hấp dẫn
- **Tối ưu chi phí**: Chỉ tốn 50-200k cho mỗi video (tùy nhà cung cấp)
- **Tăng hiệu quả**: Tự động hóa quy trình sáng tạo nội dung phức tạp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Fathom (đã ghi âm các cuộc họp)
- API Key OpenAI (khuyến nghị dùng GPT-4)
- Tài khoản Google Docs (để lưu trữ nội dung)
- API Video (Luma AI hoặc Runway ML)
- 3 subworkflows riêng biệt (chi tiết xem phần dưới)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12009](https://n8n.io/workflows/12009)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
:::note[CẤU HÌNH CHÍNH]
1. **Subworkflows bắt buộc**:
   - Tạo 3 subworkflows riêng biệt trước:
     - Text to Video (kết nối Luma AI/Runway ML)
     - Text to Image (kết nối DALL-E)
     - Transcript to Content (xử lý transcript thành nội dung)

2. **Node quan trọng**:
   - **Main GPT-4 Model** và **Video Generator GPT Model**: Cấu hình OpenAI API credentials
   - **Get Fathom Transcript**: Cập nhật endpoint API Fathom của các sếp
   - **Create Google Doc**: Điền ID tài liệu Google Docs
   - **Call DALL-E API**: Cập nhật API Key DALL-E
   - **Call Video API**: Cập nhật API Key Luma/Runway
   - **Video Ready**: Cấu hình Slack credentials để nhận thông báo
:::

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu
2. Bật Active workflow
3. Gửi tin nhắn qua chat interface: "Create content from my latest session - video and image"

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack**: Thêm node Slack để nhận thông báo khi nội dung hoàn thành
2. **Lưu log**: Thêm node Google Sheets để theo dõi lịch sử tạo nội dung
3. **Tự động hóa báo cáo**: Kết hợp với workflow gửi email báo cáo hàng tuần
4. **Tối ưu chi phí**: Sử dụng GPT-4.1-mini thay vì GPT-4 để giảm chi phí

### 📌 Kết luận
Workflow này là giải pháp toàn diện cho các sếp cần tự động hóa quy trình chuyển đổi transcript cuộc họp thành nội dung đa dạng. Với việc kết hợp công nghệ AI tiên tiến và tự động hóa hoàn toàn, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao chất lượng nội dung một cách đáng kể. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn! 🚀