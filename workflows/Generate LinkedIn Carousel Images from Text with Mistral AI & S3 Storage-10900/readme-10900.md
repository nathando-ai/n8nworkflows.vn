---
title: "🚀 Tự động tạo ảnh Carousel LinkedIn từ văn bản với Mistral AI và S3"
description: "Biến mọi đoạn văn bản hoặc bài đăng thành bộ ảnh Carousel LinkedIn chuyên nghiệp, tự động chèn chữ lên template và lưu trữ trên AWS S3 bằng n8n, Mistral AI và Google Drive."
slug: "tao-anh-linkedin-carousel-tu-van-ban-mistral-ai-s3"
tags: [n8n, automation, no-code, ai-agent, mistral-ai, aws-s3, linkedin-automation]
keywords: [n8n workflow, tạo ảnh carousel linkedin, mistral ai, s3 storage, ai content creation, tự động hóa marketing]
keywords: [n8n workflow, tạo ảnh carousel linkedin, mistral ai, s3 storage, ai content creation, tự động hóa marketing]
---

# 🚀 Tự động tạo ảnh Carousel LinkedIn từ văn bản với Mistral AI & S3 Storage

Chào các sếp! Việc tạo nội dung trực quan như ảnh Carousel trên LinkedIn để thu hút tương tác thường ngốn rất nhiều thời gian của Designer. Phải nghĩ ý tưởng, viết nội dung ngắn gọn cho từng slide, rồi lại mở Canva chỉnh sửa từng chiếc ảnh một thủ công cực kỳ nản.

Hiểu được nỗi đau đó, workflow n8n cực đỉnh từ **DIGITAL BIZ TECH** này sẽ giúp các sếp tự động hóa 100% quy trình trên: **Chỉ cần nhập một đoạn văn bản bất kỳ, AI sẽ tự tóm tắt, chia thành các slide, ghép vào template ảnh sẵn có, lưu lên S3 và trả về kết quả ngay lập tức qua giao diện Chat!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý hình ảnh và gọi AI chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần dùng Canva thủ công cho từng bài đăng LinkedIn nữa.
- **Tự động hóa thông minh:** Mistral AI tự động cắt nghĩa văn bản dài thành 3-4 slide ngắn gọn, chuẩn cấu trúc thu hút (tiêu đề dưới 5 từ).
- **Đồng bộ nhận diện:** Tự động chèn text vào các template ảnh mẫu có sẵn độ phân giải cao thông qua Google Drive.
- **Lưu trữ chuyên nghiệp:** Toàn bộ ảnh sau khi render xong sẽ được đẩy thẳng lên AWS S3 và trả link tải trực tiếp liền mạch cho người dùng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Mistral AI API Key** (cho node *Mistral Cloud Chat Model*).
- **Google Drive Account & Credentials (OAuth2)** (để lưu trữ và tải các template ảnh gốc).
- **AWS S3 Bucket** (để lưu trữ các hình ảnh Carousel hoàn thiện).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình kỹ các node sau:
- **Mistral Cloud Chat Model**: Chọn đúng credential Mistral API và thiết lập model là `mistral-small-latest`.
- **AI Agent & Structured Output Parser**: Đảm bảo cấu hình prompt cho AI Agent hiểu rằng nó phải trả về JSON gồm 3 cặp `title/subtext` (tiêu đề ngắn gọn dưới 5 từ) để Structured Output Parser không bị lỗi xác thực.
- **Google Drive (get image template)**: Các node `Google Drive get image 1`, `Google Drive (get image template)...` dùng để lấy background template. Các sếp nhớ **thay thế các fileId cũ** bằng fileId các bức ảnh template PNG trên Google Drive của chính mình (nên chuẩn bị 4 template cho 4 slide với kích thước đồng nhất).
- **Edit Image nodes (`Edit Image 1`, `Edit Image2`, `Edit Image3`...)**: Node này dùng để vẽ tiêu đề và nội dung phụ lên template. Hãy test thử với tiêu đề dài/ngắn để đảm bảo chữ ngắt dòng đẹp mắt và nằm đúng vị trí quy định.
- **S3 / S32 / S34 / S35**: Kết nối AWS S3 Credentials, trỏ đúng vào `bucketname` của các sếp và cấu hình quyền truy cập (Public access hoặc Signed URLs) để file ảnh xuất ra có thể hiển thị được.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử qua giao diện **When chat message received** (Chat Trigger).
- Kiểm tra kết quả trả về gồm các markdown image links và link tải S3.
- Nếu mọi thứ mượt mà, bật **Active** cho workflow chạy chính thức!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì trả kết quả qua chat trigger nội bộ, các sếp có thể nối thêm node gửi thẳng bộ ảnh Carousel này vào nhóm Telegram hoặc Slack của team content để kiểm duyệt trước khi đăng bài.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở cuối workflow để lưu lại nội dung text gốc và link S3 của các bộ ảnh đã tạo, giúp dễ dàng quản lý kho content theo thời gian.
- **Đa dạng hóa Template:** Tạo nhiều bộ template Google Drive khác nhau và cho AI hoặc người dùng chọn phong cách thiết kế ngay từ giao diện chat.

### 📌 Kết luận
Workflow tích hợp AI và xử lý hình ảnh này là một "vũ khí bí mật" giúp các content creator và marketer tối ưu hóa năng suất làm việc trên mạng xã hội. Hãy triển khai ngay lên hệ thống n8n của các sếp để cảm nhận sức mạnh của tự động hóa không-chạm!