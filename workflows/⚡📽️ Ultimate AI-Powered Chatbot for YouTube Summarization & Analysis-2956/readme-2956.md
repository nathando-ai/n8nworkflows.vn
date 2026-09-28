---
title: "⚡📽️ Chatbot AI Tự Động Hóa Phân Tích & Tóm Tắt Video YouTube"
description: "Tự động hóa hoàn toàn quá trình lấy thông tin video YouTube và phân tích nội dung bằng AI, tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "chatbot-ai-tu-dong-hoa-phan-tich-video-youtube"
tags: [n8n, automation, no-code, AI, marketing, YouTube]
keywords: [n8n workflow, tự động hóa, AI chatbot, phân tích video, YouTube]
---

# ⚡📽️ Chatbot AI Tự Động Hóa Phân Tích & Tóm Tắt Video YouTube

[Các sếp đang gặp khó khăn khi phải xem và tóm tắt hàng loạt video YouTube hàng ngày. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quá trình này bằng công nghệ AI tiên tiến, tiết kiệm thời gian quý giá và nâng cao hiệu quả làm việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy thông tin và tóm tắt video YouTube trong vài giây.
- **Nâng cao hiệu quả**: Phân tích nội dung video một cách chi tiết và chính xác.
- **Tích hợp hoàn hảo**: Kết nối dễ dàng với các công cụ khác trong hệ thống của các sếp.
- **Hỗ trợ đa dạng**: Phù hợp với nhiều loại video từ giáo dục đến marketing.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud Console với YouTube Data API đã kích hoạt.
- API Key từ OpenAI và DeepSeek.
- n8n đã được cài đặt và cấu hình trên hệ thống.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/2956](https://n8n.io/workflows/2956)
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get YouTube Video Details"**:
   - Chọn credentials cho Google Cloud Console.
   - Đảm bảo API Key đã được kích hoạt YouTube Data API.

2. **Node "gpt-4o-mini1" và "DeepSeek-V3 Chat"**:
   - Thêm credentials cho OpenAI API.
   - Đảm bảo tài khoản có đủ credit để sử dụng mô hình AI.

3. **Node "When chat message received"**:
   - Cấu hình webhook để nhận tin nhắn từ các nền tảng chat (Slack, Telegram...).

4. **Node "Create YouTube API URL"**:
   - Chỉnh sửa URL để phù hợp với API của các sếp.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách nhập một ID video YouTube hợp lệ.
2. Kiểm tra kết quả từ các node "Respond with YouTube Details & Transcript".
3. Bật Active workflow sau khi đã kiểm tra kỹ.

### ✍️ Mẹo & gợi ý nâng cao
- Kết nối với Slack/Telegram để nhận thông báo khi có video mới.
- Lưu log các tương tác để theo dõi hiệu suất của chatbot.
- Tích hợp với Google Sheets để lưu trữ dữ liệu tóm tắt video.
- Sử dụng DeepSeek-V3 Chat để phân tích sâu hơn nội dung video.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình lấy thông tin và phân tích video YouTube, tiết kiệm thời gian và nâng cao hiệu quả làm việc. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!