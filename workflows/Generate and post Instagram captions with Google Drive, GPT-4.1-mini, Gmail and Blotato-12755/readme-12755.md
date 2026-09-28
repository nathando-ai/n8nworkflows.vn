---
title: "🚀 Tự động hóa đăng bài Instagram với Google Drive, GPT-4o-mini, Gmail và Blotato"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy ảnh/video từ Google Drive, dùng AI viết caption, gửi email duyệt bài và tự động đăng lên Instagram qua Blotato."
slug: "tu-dong-hoa-dang-bai-instagram-google-drive-gpt-blotato"
tags: [n8n, automation, instagram, gpt-4, google-drive, blotato, ai-marketing]
keywords: [n8n workflow, tự động hóa Instagram, AI caption generator, Google Drive to Instagram, Blotato n8n, duyệt bài qua Gmail]
---

# 🚀 Tự động hóa đăng bài Instagram với Google Drive, GPT-4o-mini, Gmail và Blotato

Các sếp có đang mệt mỏi vì mỗi ngày phải lục tìm hình ảnh trong máy, vắt óc nghĩ caption, rồi ngồi bấm đăng bài Instagram thủ công? Việc này vừa tốn thời gian, vừa dễ bị ngắt quãng lịch đăng bài khiến kênh mất tương tác.

Giải pháp ở đây chính là workflow n8n tự động hóa 100% từ A-Z do **Automate With Marc** phát triển. Workflow này sẽ biến kho dữ liệu thô trên Google Drive của các sếp thành một cỗ máy sản xuất nội dung tự động, có tích hợp AI sáng tạo caption và chốt chặn phê duyệt qua email trước khi xuất bản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần phải lên lịch thủ công hay nghĩ caption mỗi ngày.
- **Kiểm soát chất lượng (Human-in-the-loop):** Gửi email yêu cầu duyệt kèm nút Phê duyệt/Từ chối trước khi đăng, tránh việc AI "nói hớ".
- **Đa dạng hóa nội dung thông minh:** Node Randomizer tự động bốc thăm ngẫu nhiên file trong thư mục Google Drive để tránh đăng lặp lại một nội dung.
- **Vận hành 24/7:** Chạy tự động theo lịch hẹn (Ví dụ: 10:00 sáng mỗi ngày).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive Account** (OAuth2 để tìm và tải file).
- **OpenAI API Key** (Sử dụng GPT-4o-mini để viết caption).
- **Gmail Account** (OAuth2 để gửi email chờ duyệt).
- **Blotato Account** (Nền tảng quản lý và đăng bài mạng xã hội).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n.io (Link gốc: [Workflow #12755](https://n8n.io/workflows/12755)) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Thiết lập mốc thời gian chạy tự động hàng ngày (Mặc định là 10:00 AM).
- **Search files and folders (Google Drive):** Kết nối tài khoản Google Drive OAuth và điền **Folder ID** của thư mục chứa hình ảnh/video của các sếp.
- **Randomizer (Code Node):** Node này dùng đoạn mã JS để chọn ngẫu nhiên 1 file từ kết quả tìm kiếm của Google Drive.
- **Caption Generator AI (OpenAI):** Kết nối OpenAI Credentials và tinh chỉnh system prompt để AI viết caption Instagram chuẩn phong cách thương hiệu của các sếp dựa trên tên file hoặc nội dung.
- **Send For Approval and Wait (Gmail):** Kết nối Gmail OAuth, cấu hình email nhận thông báo duyệt bài. Node này cực kỳ thông minh vì nó sẽ tạm dừng workflow (`Wait`) cho đến khi các sếp bấm nút Phê duyệt hoặc Từ chối trong email.
- **If (Node):** Kiểm tra kết quả phản hồi từ email:
  - *Nếu đồng ý (Yes):* Chạy tiếp nhánh tải file, upload lên Blotato và tạo bài viết.
  - *Nếu từ chối (No):* Workflow có thể vòng lại chọn file khác (tùy cấu hình mở rộng).
- **Download Content File & Upload media / Create post (Blotato):** Tải file từ Drive, đẩy lên Blotato và tự động publish lên Instagram.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Execute Workflow`) với dữ liệu mẫu để kiểm tra luồng gửi email chờ duyệt.
- Bật công tắc **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì dùng Gmail để duyệt bài, các sếp có thể đổi thành node Telegram hoặc Slack Bot để bấm duyệt trực tiếp trên điện thoại cho nhanh.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets vào cuối luồng để lưu lại lịch sử các bài đã đăng thành công kèm link bài viết.
- **Tinh chỉnh AI Prompt:** Cung cấp thêm bối cảnh về sản phẩm/dịch vụ vào node OpenAI để caption cuốn hút, chèn sẵn hashtag tự động.

### 📌 Kết luận
Workflow này là trợ lý đắc lực cho các nhà sáng tạo nội dung và doanh nghiệp vừa và nhỏ muốn tối ưu hóa quy trình Social Media. Hãy thiết lập ngay hôm nay để giải phóng thời gian và để AI làm thay những việc lặp đi lặp lại!