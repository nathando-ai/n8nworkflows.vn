---
title: "🚀 Xây dựng nhà máy nội dung LinkedIn tự động với AI Agent và Replicate"
description: "Tự động hóa toàn bộ quy trình từ ý tưởng trên Google Sheets, nghiên cứu xu hướng với AI, viết bài LinkedIn chuyên nghiệp đến tạo ảnh nhận diện thương hiệu và xuất bản."
slug: "linkedin-content-factory-openai-replicate"
tags: [n8n, automation, no-code, AI Agent, LinkedIn, OpenAI, Replicate]
keywords: [n8n workflow, tự động hóa linkedin, ai agent content creator, replicate image generation, google sheets automation]
---

# 🚀 Tự động hóa nhà máy nội dung LinkedIn với AI Agent và Replicate

Chào các sếp! Việc duy trì đăng bài đều đặn trên LinkedIn để xây dựng thương hiệu cá nhân hoặc doanh nghiệp là vô cùng quan trọng, nhưng lại cực kỳ ngốn thời gian. Bạn phải nghĩ chủ đề, tra cứu thông tin, viết bài sao cho bắt mắt, rồi lại đi tìm hoặc thiết kế hình ảnh phù hợp. 

Nhưng đừng lo, với workflow n8n cực kỳ mạnh mẽ này (**LinkedIn Content Factory with OpenAI Research & Replicate Branded Images** do tác giả Onur phát triển), các sếp sẽ sở hữu một "nhà máy" sản xuất nội dung tự động 100%. Workflow sẽ lấy chủ đề thô từ Google Sheets, dùng AI Agent kết hợp SerpAPI để nghiên cứu xu hướng, viết bài chuẩn viral, tạo ảnh nhận diện thương hiệu qua Replicate và tự động đăng lên LinkedIn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh trăn trở mỗi sáng không biết đăng gì hay ngồi thiết kế ảnh Canva thủ công.
- **Nội dung chuẩn SEO & Viral:** AI tự động tìm kiếm thông tin mới nhất trên mạng thông qua SerpAPI để đưa ra góc nhìn sắc bén, thu hút tương tác.
- **Nhận diện thương hiệu độc quyền:** Hình ảnh minh họa được tạo tự động qua Replicate tuân thủ nghiêm ngặt bộ nhận diện màu sắc của thương hiệu.
- **Vận hành khép kín:** Từ khâu lấy ý tưởng -> Nghiên cứu -> Viết bài -> Tạo ảnh -> Đăng bài -> Cập nhật trạng thái Google Sheets đều diễn ra hoàn toàn tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để "lên đồ" cho workflow này, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Google Sheets:** Tài khoản Google chứa bảng dữ liệu chủ đề bài viết.
- **OpenAI API Key:** Cho các node AI Agent (sử dụng model `gpt-4.1-mini`).
- **SerpAPI Key:** Dùng để AI Agent truy vấn thông tin, tìm kiếm xu hướng trên web.
- **Replicate API Key:** Dùng để gọi mô hình tạo ảnh AI.
- **LinkedIn Account:** Tài khoản LinkedIn cá nhân hoặc trang doanh nghiệp (Page) để cấp quyền đăng bài qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow này từ n8n template hoặc copy đoạn JSON trực tiếp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp) và chọn file JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 20 nodes chính được chia thành các phase rõ rệt. Các sếp cần cấu hình kỹ các điểm sau:

- **Chuẩn bị Google Sheets:** 
  - Tại node `1. Get Pending Topic from Google Sheets` và `8. Update Google Sheets`: Kết nối tài khoản Google Sheets của các sếp.
  - Tạo sẵn một file Google Sheets có các cột: `Topic` (Chủ đề) và `Status` (Trạng thái - đặt là "Pending" cho các dòng chờ chạy).
- **Cấu hình AI & Tìm kiếm:**
  - Nodes `2. Research Topic & Find Viral Angle with AI` và `3. Generate LinkedIn Post Content with AI`: Liên kết với `OpenAI Chat Model` và `SerpAPI` bằng các credentials tương ứng.
- **Tùy chỉnh phong cách hình ảnh:**
  - Tại node `4. Generate Branded Image Prompt` (Code node): Các sếp có thể chỉnh sửa biến `fixedImageStyleDetails` để khớp với mã màu thương hiệu (ví dụ: mã màu RAL, phong cách ánh sáng, bố cục) để ảnh sinh ra mang đậm dấu ấn riêng.
- **Tạo và kiểm tra ảnh:**
  - Nodes `5a. Start Image Generation (Replicate)` và `5b. Check Image Status`: Điền Replicate API key vào HTTP Header Auth credentials để hệ thống gọi lệnh tạo ảnh và lặp kiểm tra trạng thái hoàn thành.
- **Xuất bản:**
  - Node `7. Publish Post to LinkedIn`: Kết nối tài khoản LinkedIn qua OAuth2 để cho phép n8n thay mặt đăng bài.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một dòng dữ liệu mẫu (trạng thái "Pending") để kiểm tra toàn bộ luồng từ A-Z.
- Sau khi test thành công, bấm nút **Active** góc trên cùng bên phải để bật chế độ tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node Telegram hoặc Slack ngay sau node `7. Publish Post to LinkedIn` để nhận thông báo tức thì kèm link bài viết khi AI đăng bài thành công.
- **Lưu trữ hình ảnh:** Thêm node Google Drive hoặc AWS S3 để lưu lại bản sao của hình ảnh đã tạo phục vụ cho các chiến dịch marketing khác.
- **Lên lịch định kỳ:** Thay vì chạy thủ công, hãy gắn thêm một node `Schedule Trigger` ở đầu workflow để hệ thống tự động quét Google Sheets và sản xuất bài viết mỗi ngày vào khung giờ vàng.

### 📌 Kết luận
Với workflow **LinkedIn Content Factory**, việc xây dựng kênh social media chuyên nghiệp chưa bao giờ dễ dàng đến thế. Hãy trang bị ngay cho mình một hệ thống tự động hóa thông minh để tối ưu hóa hiệu suất làm việc ngay hôm nay! Chúc các sếp thao tác thành công!