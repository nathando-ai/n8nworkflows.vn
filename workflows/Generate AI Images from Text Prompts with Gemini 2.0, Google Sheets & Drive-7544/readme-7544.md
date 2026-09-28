---
title: "🚀 Tự động tạo ảnh AI từ văn bản với Gemini 2.0, Google Sheets & Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình đọc prompt từ Google Sheets, tạo hình ảnh chất lượng cao bằng Gemini AI, lưu trữ vào Google Drive và cập nhật ngược lại link ảnh."
slug: "tu-dong-tao-anh-ai-gemini-google-sheets-drive"
tags: [n8n, automation, ai-agent, google-gemini, google-sheets, google-drive, content-creation]
keywords: [n8n workflow, tạo ảnh ai, gemini 2.0, google sheets automation, google drive, tự động hóa nội dung]
---

# 🚀 Tự động tạo ảnh AI từ văn bản với Gemini 2.0, Google Sheets & Drive

Các sếp có đang gặp khó khăn khi phải quản lý hàng trăm bài viết mạng xã hội nhưng lại thiếu hình ảnh minh họa đi kèm? Việc thuê designer hoặc tự tay tạo từng bức ảnh bằng các công cụ AI thủ công ngốn rất nhiều thời gian và gây nghẽn cổ chai cho đội ngũ Marketing.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ, giúp tự động hóa toàn bộ quy trình: Đọc ý tưởng từ Google Sheets 👉 Dùng AI Agent viết nội dung 👉 Tạo ảnh nghệ thuật bằng Gemini 2.0 👉 Lưu vào Google Drive 👉 Trả link ảnh hoàn chỉnh về lại Google Sheets mà không cần đụng tay vào bất kỳ thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chạy định kỳ theo lịch trình, tự động quét các dòng dữ liệu mới trong Google Sheets để xử lý.
- **Sức mạnh đa phương thức (Multimodal):** Kết hợp linh hoạt giữa Google Gemini Chat Model (để tối ưu nội dung) và Gemini Image Generation (để tạo ảnh trực quan).
- **Đồng bộ mượt mà:** Hình ảnh được tự động upload lên Google Drive cá nhân/doanh nghiệp, chia sẻ quyền truy cập công khai và tự động điền link vào bảng tính.
- **Tiết kiệm thời gian khổng lồ:** Giải phóng hoàn toàn thời gian cho designer và content creator để tập trung vào chiến lược cốt lõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Google Gemini (Google Palm API / Google AI Studio)** để lấy API Key sử dụng cho các model AI.
- Tài khoản **Google Drive & Google Sheets** để lưu trữ dữ liệu và file hình ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình. Workflow này bao gồm 12 nodes phối hợp nhịp nhàng với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các nodes quan trọng sau:

- **Schedule Trigger:** Thiết lập mốc thời gian muốn workflow tự động quét dữ liệu (ví dụ: chạy mỗi giờ, mỗi ngày một lần...).
- **Get row(s) in sheet (Google Sheets):** Kết nối tài khoản Google Sheets của sếp, trỏ tới file Google Sheet chứa danh sách các prompt/chủ đề bài viết.
- **AI Agent & Google Gemini Chat Model:** Cấu hình credentials sử dụng `googlePalmApi`. Node này sẽ đóng vai trò xử lý ngôn ngữ, viết lại hoặc mở rộng ý tưởng từ bảng tính.
- **Structured Output Parser:** Giúp định dạng đầu ra từ AI Agent theo đúng cấu trúc JSON mong muốn để truyền dữ liệu mượt mà sang bước tạo ảnh.
- **Generate Image with Gemini (googleGemini):** Node cốt lõi sử dụng prompt động được trích xuất từ văn bản:
  ```text
  Create a high-quality, visually engaging image for a social media post based on the following text:
  "{{ $json.output.post }}"
  ```
- **Upload file & Share file (Google Drive):** Kết nối tài khoản Google Drive (sử dụng `googleDriveOAuth2Api`). Node *Upload file* sẽ lưu ảnh vừa tạo lên Drive, còn node *Share file* sẽ cấu hình quyền chia sẻ công khai (Anyone with the link) để lấy URL truy cập.
- **update imageUrl (Google Sheets):** Cập nhật lại đường dẫn hình ảnh (`imageUrl`) vừa nhận từ Google Drive vào đúng dòng tương ứng trong bảng tính Google Sheets ban đầu.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** chạy thử với một vài dòng dữ liệu mẫu để kiểm tra xem ảnh đã được tạo và đẩy về Google Sheets thành công chưa.
- Sau khi kiểm tra mọi thứ hoạt động hoàn hảo, hãy gạt công tắc sang **Active** để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo:** Tích hợp thêm node **Telegram** hoặc **Slack** để gửi thông báo về chuông chat của các sếp ngay khi một loạt ảnh mới được tạo thành công.
- **Xử lý hàng loạt (Batching):** Sử dụng node **Limit** một cách thông minh để kiểm soát số lượng ảnh tạo ra mỗi lần chạy, tránh vượt quá giới hạn API (Rate limit) của Google Gemini.
- **Quản lý file khoa học:** Tạo một thư mục riêng biệt trên Google Drive thông qua ID thư mục để gom tất cả ảnh AI vào một nơi gọn gàng.

### 📌 Kết luận
Việc tích hợp AI vào quy trình sản xuất nội dung chưa bao giờ dễ dàng đến thế với n8n và Gemini 2.0. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp ngay hôm nay!