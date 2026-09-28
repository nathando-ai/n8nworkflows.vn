---
title: "🏋️‍♂️ Tự động hóa kế hoạch tập luyện cá nhân với AI Gemini và Telegram"
description: "Hướng dẫn tạo bot Telegram thông minh giúp phân tích hình ảnh hoặc văn bản để tạo kế hoạch tập luyện cá nhân hóa bằng AI Gemini của Google"
slug: "tu-dong-hoa-ke-hoach-tap-luyen-ca-nhan-voi-ai-gemini-va-telegram"
tags: [n8n, automation, no-code, telegram, ai, google-gemini]
keywords: [n8n workflow, tự động hóa, bot telegram, kế hoạch tập luyện, ai gemini]
---

# 🏋️‍♂️ Tự động hóa kế hoạch tập luyện cá nhân với AI Gemini và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên đến 80% cho việc tạo kế hoạch tập luyện
- Nhận được kế hoạch tập luyện cá nhân hóa dựa trên hình ảnh hoặc mô tả văn bản
- Tự động hóa hoàn toàn quá trình tạo kế hoạch mà không cần can thiệp thủ công
- Hỗ trợ cả hình ảnh và văn bản để tạo kế hoạch tập luyện
- Kết quả được định dạng đẹp mắt và dễ đọc
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram để tạo bot và nhận tin nhắn
- API Key của Google Gemini (để sử dụng mô hình AI)
- Tài khoản n8n đã được cài đặt và cấu hình
- Các credentials cho các node: Telegram, Google Gemini
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Google Gemini Chat Model**: Cấu hình API Key của Google Gemini
- **Workout Guide**: Cấu hình prompt để tạo kế hoạch tập luyện từ văn bản
- **Workout Guide through Image**: Cấu hình prompt để tạo kế hoạch tập luyện từ hình ảnh
- **Analyze image**: Cấu hình để phân tích hình ảnh và trích xuất thông tin
- **Receive a Message**: Cấu hình bot Telegram để nhận tin nhắn
- **Text Vs Photo**: Cấu hình để phân biệt giữa tin nhắn văn bản và hình ảnh
- **Clean up Workout plane and Make User freindly And Visually appealing**: Cấu hình để định dạng kết quả đầu ra đẹp mắt
- **Send A Workout Planes**: Cấu hình để gửi kế hoạch tập luyện qua Telegram

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các dịch vụ khác như Slack hoặc Email để gửi báo cáo định kỳ
- Lưu log các tương tác để phân tích và cải thiện hiệu suất
- Tích hợp với các ứng dụng theo dõi sức khỏe để cập nhật tiến độ tập luyện

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình tạo kế hoạch tập luyện cá nhân hóa bằng AI Gemini và Telegram. Với việc tích hợp các tính năng phân tích hình ảnh và văn bản, workflow này mang lại trải nghiệm tập luyện cá nhân hóa và hiệu quả cao. Hãy áp dụng ngay để tối ưu hóa quá trình tập luyện của mình!