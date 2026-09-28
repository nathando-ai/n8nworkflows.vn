---
title: "🚀 Tự động tạo ảnh quảng cáo sáng tạo từ ảnh gốc với Seedream v4 và đăng trực tiếp lên Facebook, Instagram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo ảnh AI từ prompt và ảnh tham chiếu bằng Seedream v4, sau đó tự động đăng bài lên Facebook và Instagram."
slug: "tao-anh-quang-cao-tu-dong-seedream-v4-facebook-instagram"
tags: [n8n, automation, ai-images, seedream-v4, facebook, instagram, marketing]
keywords: [n8n workflow, seedream v4, tao anh ai tu dong, dang bai facebook instagram tu dong, fal.ai, upload-post]
---

# 🚀 Tự động tạo ảnh quảng cáo sáng tạo từ ảnh gốc với Seedream v4 và đăng trực tiếp lên Facebook, Instagram

Việc thiết kế hình ảnh quảng cáo (ADV) thủ công kết hợp nhiều hình ảnh tham chiếu (reference images) thường tốn rất nhiều thời gian và công sức của đội ngũ Marketing. Chưa kể khâu xuất file và đăng tải lần lượt lên các nền tảng mạng xã hội như Facebook hay Instagram lại càng thêm phần lặp đi lặp lại. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp kết hợp sức mạnh của Multimodal AI (Seedream v4 qua Fal.ai), OpenAI để viết tiêu đề, lưu trữ Google Drive và tự động hóa xuất bản lên mạng xã hội qua Upload-Post.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Từ việc nhận yêu cầu qua Web Form, xử lý ảnh tham chiếu, gọi AI tạo ảnh, đến đăng bài Facebook & Instagram.
- **Tối ưu hóa sáng tạo**: Tạo ảnh quảng cáo độc đáo dựa trên văn bản (Prompt) kết hợp tối đa tới 6 ảnh tham chiếu.
- **Tiết kiệm 90% thời gian**: Không còn thao tác thủ công từ khâu thiết kế ý tưởng đến lên lịch đăng bài.
- **Hoạt động liền mạch 24/7**: Hệ thống tự động kiểm tra trạng thái render ảnh (Wait node, Loop/If check) và xử lý mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Fal.ai Account**: Để lấy API Key sử dụng mô hình Seedream v4.
- **OpenAI API Key**: Dùng cho node tạo tiêu đề (Generate title).
- **Upload-Post Account**: Đăng ký tại [Upload-Post](https://www.upload-post.com/?linkId=lp_144414&sourceId=n3witalia&tenantId=upload-post-app) để lấy API Key xuất bản bài viết lên Instagram và Facebook (Có gói miễn phí 10 bài/tháng).
- **Google Drive Account**: Tài khoản OAuth2 để lưu trữ hình ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ nguồn cung cấp, sau đó copy toàn bộ nội dung và dán trực tiếp vào n8n Editor của các sếp (hoặc chọn Import từ file).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và Credentials sau cho các node quan trọng:

- **On form submission**: Node nhận yêu cầu từ người dùng (Web Form). Các sếp có thể tuỳ chỉnh trường nhập liệu Prompt và các ảnh tham chiếu.
- **Generate title (OpenAi)**: Kết nối credentials `openAiApi` để AI tự động tạo tiêu đề hấp dẫn cho bài viết.
- **Create Video / Create Image (HTTP Request)**: 
  - Cần tạo tài khoản tại [Fal.ai](https://fal.ai/) để lấy API Key.
  - Trong node gọi API tạo ảnh, cấu hình `Header Auth` với:
    - **Name**: `Authorization`
    - **Value**: `Key YOURAPIKEY` (Thay thế bằng API Key của các sếp).
- **Get status, Wait 60 sec., Completed?**: Các node này đóng vai trò vòng lặp chờ kết quả render ảnh từ AI hoàn thành trước khi chuyển sang bước tiếp theo.
- **Upload Image (Google Drive)**: Cấu hình kết nối tài khoản Google Drive qua OAuth2 để lưu trữ bản sao hình ảnh.
- **Post to Instagram & Post to Facebook (HTTP Request)**:
  - Lấy API Key từ [Upload-Post Manage Api Keys](https://www.upload-post.com/?linkId=lp_144414&sourceId=n3witalia&tenantId=upload-post-app).
  - Cấu hình `Auth Header`:
    - **Name**: `Authorization`
    - **Value**: `Apikey YOUR_API_KEY_HERE`
  - Đặt tên Profile đã tạo trên Upload-Post vào biến `YOUR_USERNAME` (ví dụ: `test1` hoặc `test2`) để hệ thống biết đăng bài lên tài khoản xã hội nào.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một biểu mẫu (Form) mẫu để kiểm tra toàn bộ luồng dữ liệu từ tạo ảnh đến đăng bài.
- Sau khi test thành công, bật công tắc **Active** để workflow hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh đăng tải**: Ngoài Facebook và Instagram, các sếp có thể nâng cấp gói Upload-Post để đẩy nội dung sang LinkedIn, Twitter hoặc Pinterest.
- **Lưu log & Báo cáo**: Thêm node Google Sheets hoặc Telegram để gửi thông báo về máy khi workflow tạo ảnh và đăng bài thành công hoặc gặp lỗi.
- **Tối ưu Prompt**: Tích hợp thêm một node AI phụ trợ để tinh chỉnh (enhance) câu lệnh prompt của người dùng trước khi gửi cho Seedream v4 nhằm thu được bức ảnh chất lượng cao nhất.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một "phòng Marketing AI" tự động hoàn toàn: nhận yêu cầu, sáng tạo hình ảnh đẳng cấp từ ảnh gốc và tự động phủ sóng mạng xã hội trong tích tắc. Bắt tay vào cài đặt ngay thôi nào!