---
title: "🚀 Tự động tạo ảnh bằng AI và kiểm duyệt chất lượng với DALL-E 2 và GotoHuman trên n8n"
description: "Xây dựng quy trình tự động hóa kết hợp AI tạo ảnh DALL-E 2 và vòng lặp kiểm duyệt thủ công (Human-in-the-loop) chuyên nghiệp với GotoHuman trên n8n."
slug: "tu-dong-tao-anh-ai-dall-e-2-goto-human-review-n8n"
tags: [n8n, automation, ai, dall-e, gotohuman, content-creation]
keywords: [n8n workflow, tạo ảnh AI, DALL-E 2, kiểm duyệt thủ công, Human-in-the-loop, GotoHuman]
---

# 🚀 Tự động tạo ảnh bằng AI và kiểm duyệt chất lượng với DALL-E 2 và GotoHuman

Các sếp có bao giờ gặp tình trạng dùng AI tạo ảnh hàng loạt nhưng chất lượng không đồng đều, ảnh bị lỗi chi tiết hoặc không đúng ý muốn? Việc phải ngồi lọc thủ công từng bức ảnh tốn rất nhiều thời gian.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100% quy trình: **AI vẽ ảnh (DALL-E 2) ➔ Gửi cho con người kiểm duyệt (GotoHuman) ➔ Nếu chưa đạt thì yêu cầu AI vẽ lại theo ý kiến chỉnh sửa**. Không còn cảnh "quay tay" thủ công nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát chất lượng (Quality Control):** Đảm bảo 100% hình ảnh đầu ra đạt tiêu chuẩn trước khi đưa vào sử dụng thực tế.
- **Tự động hóa vòng lặp (Human-in-the-loop):** Kết hợp hoàn hảo giữa tốc độ của AI và sự tinh tế trong đánh giá của con người.
- **Tối ưu thời gian:** AI tự động tinh chỉnh lại prompt và vẽ lại ngay lập tức khi nhận được phản hồi từ chối từ người kiểm duyệt.
- **Linh hoạt mở rộng:** Dễ dàng tích hợp thêm các bước lưu trữ vào Google Drive hoặc đăng trực tiếp lên mạng xã hội sau khi được duyệt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance:** Bản Cloud hoặc Self-hosted.
- **OpenAI API Account:** Có quyền truy cập DALL-E 2.
- **GotoHuman Account:** Dùng làm giao diện giao việc kiểm duyệt cho team.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow và chọn **Import from Clipboard** trong giao diện n8n Editor của các sếp. Hệ thống sẽ tự động dựng sẵn 8 nodes với đầy đủ các liên kết.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **Set Image Prompt (Node Set):** 
  - Nơi khởi nguồn ý tưởng. Các sếp hãy sửa lại trường `Prompt` thành nội dung bức ảnh mình muốn tạo (ví dụ: *"Make an image of an attractive person standing in new york city"*).
- **Initial Image Generation & Second Image Generation (Nodes OpenAI):** 
  - Chọn Credentials là tài khoản OpenAI API của các sếp.
  - Model được cấu hình mặc định là `dall-e-2`, resource là `image`.
- **Initial Review & Second Review (Nodes GotoHuman):** 
  - Chọn Credentials là tài khoản GotoHuman API.
  - Đảm bảo Review Template ID trùng khớp với template đã tạo trên dashboard của GotoHuman (`3473LaRDbdf03sd6uzYG`).
- **If rejected (Node If):** 
  - Node điều kiện kiểm tra phản hồi từ người duyệt. Nếu kết quả là `rejected`, luồng sẽ tự động kích hoạt tiến trình tạo ảnh lần 2 dựa trên prompt cải tiến.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** trên nút **Start Workflow** (Manual Trigger) để test thử nghiệm với dữ liệu mẫu.
- Kiểm tra dashboard GotoHuman để xem form duyệt ảnh, bấm Approve/Reject để test tính năng rẽ nhánh.
- Khi mọi thứ đã chạy trơn tru, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Thêm node **Google Drive** hoặc **Supabase** ở cuối luồng để tự động tải và lưu trữ những bức ảnh đã được "Approved".
- **Thông báo qua Slack/Telegram:** Thêm node gửi tin nhắn thông báo cho team ngay khi có một bức ảnh mới cần được kiểm duyệt trên GotoHuman.
- **Tích hợp Webhook:** Thay thế node `Start Workflow` bằng `Webhook` để nhận yêu cầu tạo ảnh từ các hệ thống CRM hoặc Website của doanh nghiệp.

### 📌 Kết luận
Workflow kết hợp DALL-E 2 và GotoHuman này là chìa khóa giúp các doanh nghiệp sản xuất nội dung hình ảnh số lượng lớn mà vẫn giữ được chất lượng kiểm soát chặt chẽ. Hãy cài đặt ngay hôm nay để tối ưu hóa đội ngũ sáng tạo của các sếp!