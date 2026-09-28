---
title: "🚀 Tự động biến đánh giá khách hàng từ Feedspace thành Case Study chuẩn SEO và đăng lên WordPress bằng Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa 100%: Nhận đánh giá từ Feedspace, dùng AI Gemini viết case study chuẩn SEO và tự động xuất bản lên website WordPress."
slug: "tu-dong-tao-case-study-tu-feedspace-wordpress-gemini"
tags: [n8n, automation, wordpress, google-gemini, ai-agent, content-creation]
keywords: [n8n workflow, feedspace to wordpress, ai agent case study, google gemini n8n, tự động hóa nội dung]
---

# 🚀 Tự động biến đánh giá khách hàng từ Feedspace thành Case Study chuẩn SEO và đăng lên WordPress

Các sếp có công nhận rằng những đánh giá (testimonial) 5 sao từ khách hàng là "vũ khí" bán hàng cực kỳ lợi hại không? Nhưng ngặt nỗi, việc ngồi cop từng feedback, hì hục viết lại thành một bài case study hoàn chỉnh, rồi tối ưu SEO, đăng lên WordPress tốn biết bao nhiêu là thời gian và chất xám. 

Đừng lo, bài toán này nay đã có lời giải tự động hóa 100%! Workflow n8n siêu việt này sẽ tự động bắt lấy feedback từ **Feedspace**, giao cho **AI Agent (Google Gemini)** phân tích và viết thành một bài case study hấp dẫn, chuẩn SEO, rồi tự động "xuất xưởng" lên website **WordPress** của các sếp ngay lập tức. Không cần một dòng code nào thủ công cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ viết bài, hệ thống xử lý chỉ trong vài giây ngay khi có khách đánh giá.
- **Nội dung chất lượng cao, chuẩn SEO:** Google Gemini tự động chọn góc nhìn hấp dẫn, tạo tiêu đề thu hút và cấu trúc HTML chuẩn chỉnh.
- **Tự động hóa xuất bản:** Bài viết tự động lên sóng WordPress ở trạng thái Draft hoặc Publish tùy ý các sếp.
- **Hoạt động 24/7:** Không bỏ lỡ bất kỳ lời khen hay góp ý giá trị nào từ khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Feedspace** (để quản lý và gửi webhook đánh giá).
- API Key của **Google Gemini** (cho AI Model node).
- Trang web **WordPress** (cần bật tính năng REST API hoặc Application Passwords).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Feedspace Webhook**: Node này sẽ sinh ra một URL webhook. Các sếp cần kích hoạt workflow, copy Production Webhook URL, sau đó vào `Feedspace → Automations → Webhooks`, dán URL này vào để nhận dữ liệu thời gian thực.
- **Extract Testimonial Data & If**: Kiểm tra cấu trúc dữ liệu đầu vào từ Feedspace (Tên reviewer, Rating, Text feedback, Event type) và lọc chỉ lấy các feedback dạng văn bản.
- **Google Gemini Chat Model & AI Agent**: Điền Google Gemini API Key. Node AI Agent được cấu hình sẵn để đọc feedback, chọn góc tiếp cận, viết nội dung case study dạng HTML và tạo tiêu đề chuẩn SEO.
- **Parse AI Agent Output & Memory Context Logger**: Các node Code giúp bóc tách và định dạng dữ liệu đầu ra từ AI thành các trường chuẩn để đẩy sang WordPress.
- **Create WordPress Post**: Kết nối tài khoản WordPress của các sếp (sử dụng thông tin đăng nhập Admin hoặc Application Passwords) để hệ thống có quyền tạo bài viết mới tự động.

#### 3. Kích hoạt ⚡️
- Gửi thử một dữ liệu test qua webhook bằng Postman hoặc trực tiếp từ Feedspace để kiểm tra xem bài viết đã được tạo trên WordPress chưa.
- Nếu mọi thứ xanh mượt, bật công tắc **Active workflow** lên và đi uống cà phê thôi các sếp!

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo:** Nối thêm node **Telegram** hoặc **Slack** sau node tạo bài viết thành công để nhận thông báo ngay trên điện thoại mỗi khi có case study mới xuất xưởng.
- **Lưu lịch sử:** Lưu toàn bộ thông tin feedback và link bài viết case study vào **Google Sheets** để dễ dàng tổng hợp và làm báo cáo marketing hàng tháng.
- **Tạo ảnh Thumbnail tự động:** Tích hợp thêm AI tạo ảnh (như DALL-E hoặc Stable Diffusion) để tự động sinh hình đại diện cho bài viết WordPress thêm phần bắt mắt.

### 📌 Kết luận
Việc xây dựng phễu nội dung tự động từ chính feedback của khách hàng chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay workflow này để tối ưu hóa quy trình Marketing và nâng tầm uy tín thương hiệu trên website của các sếp nhé!