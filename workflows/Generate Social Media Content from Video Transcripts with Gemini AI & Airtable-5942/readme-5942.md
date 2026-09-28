---
title: "🚀 Tự động hóa sản xuất nội dung đa nền tảng từ Video Transcript với Gemini AI và Airtable"
description: "Hướng dẫn xây dựng workflow n8n tự động biến video transcript thành bộ nội dung social media hoàn chỉnh (YouTube, TikTok, LinkedIn, Twitter, Instagram) bằng Google Gemini AI và lưu trữ tự động vào Airtable, Google Drive."
slug: "tu-dong-hoa-tao-noi-dung-social-media-gemini-airtable"
tags: [n8n, automation, ai, google-gemini, airtable, google-drive]
keywords: [n8n workflow, tạo content tự động, gemini ai, airtable automation, multimodal ai, content creator]
---

# 🚀 Biến Video Transcript thành Bộ Nội dung Social Media tự động 100% với Gemini AI & Airtable

Các sếp là Content Creator, Marketer hay Solopreneur chắc chắn đã quá ngán ngẩm cảnh mỗi lần có video mới là lại hì hục ngồi cắt gọt, viết lại caption cho từng nền tảng: YouTube, LinkedIn, Twitter/X, TikTok, Instagram... Việc này vừa tốn hàng giờ đồng hồ, vừa dễ bị cạn kiệt ý tưởng diễn đạt.

Hiểu được nỗi đau đó, workflow n8n được thiết kế bởi tác giả **Kurt Bijl** này sẽ giải quyết triệt để vấn đề trên. Chỉ với một đoạn video transcript ban đầu, hệ thống sẽ tự động hóa toàn bộ quy trình: gọi AI phân tích, tạo thư mục trên Google Drive, lưu trữ file transcript, và xuất ra một bộ content đa nền tảng chuẩn chỉnh được đồng bộ thẳng về Airtable. Các sếp chỉ việc "copy và paste" lên lịch đăng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa dạng hóa nội dung tự động:** AI phân tích transcript và trả về kết cấu chuẩn cho YouTube (Title, Description, Thumbnail text), Twitter Thread, LinkedIn post, Instagram/TikTok/Shorts caption và bộ Tags liên quan.
- **Tối ưu hóa thời gian:** Giảm từ 3-4 tiếng làm content thủ công xuống còn vài giây kích hoạt qua Webhook.
- **Quản lý tài nguyên khoa học:** Tự động tạo thư mục riêng trên Google Drive cho từng project và lưu file transcript gọn gàng.
- **Đồng bộ hóa tập trung:** Toàn bộ kết quả trả về được cập nhật tự động vào đúng dòng (record) trên Airtable, sẵn sàng để quản lý lịch đăng bài.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Airtable:** Base quản lý video/transcript với các trường (fields) chứa tiêu đề, nội dung transcript và các trường trống để nhận dữ liệu content trả về.
- **Tài khoản Google Drive:** Nơi lưu trữ thư mục và file transcript được tạo tự động.
- **Google Gemini API Key:** (Google Palm/Gemini API) để cấp quyền cho AI Agent phân tích ngữ cảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu 3 chấm góc trên bên phải -> **Import from Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:
- **🎯 Webhook Trigger:** Nhận tín hiệu kích hoạt từ Airtable Automation khi có bản ghi (record) mới cần xử lý. Cần cấu hình URL này vào Airtable Automations (phần "Send a webhook").
- **1. Get Record Data & 4. Save Social Media Content & 5. Link Folder to Record (Airtable):** Cần kết nối tài khoản thông qua `airtableTokenApi`, sau đó trỏ đúng vào **Base** và **Table** mà các sếp đang sử dụng trên Airtable.
- **🤖 AI Content Generator & 🧠 Gemini Pro Model / ⚡ Gemini Flash Model:** Kết nối bằng `googlePalmApi` (Gemini API Key). Trong node Agent và Structured Output Parser, kiểm tra kỹ schema JSON đầu ra để đảm bảo AI trả về đúng các định dạng (YouTube, Twitter, LinkedIn, TikTok...).
- **2. Create Project Folder & 6. Save Transcript File (Google Drive):** Kết nối qua `googleDriveOAuth2Api`, cấu hình thư mục gốc (parent folder) trên Google Drive để hệ thống tự động tạo thư mục con mang tên video và lưu trữ file văn bản (transcript).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng một bản ghi mẫu trên Airtable.
- Kiểm tra kết quả trên Google Drive và Airtable xem dữ liệu đã đổ về đầy đủ chưa.
- Nếu mọi thứ trơn tru, hãy gạt công tắc **Active** sang trạng thái `On` để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về điện thoại cho các sếp mỗi khi AI tạo xong bộ content mới.
- **Tự động lên lịch:** Kết hợp thêm node Google Calendar hoặc Buffer/Hootsuite để tự động đẩy bài viết lên các nền tảng social theo lịch định sẵn.
- **Mở rộng ngôn ngữ:** Tinh chỉnh prompt bên trong AI Agent để yêu cầu tạo nội dung bằng nhiều ngôn ngữ khác nhau (Tiếng Anh, Tiếng Việt...) tùy theo đối tượng khán giả.

### 📌 Kết luận
Tự động hóa sản xuất nội dung chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Gemini AI. Hãy thiết lập ngay workflow này để giải phóng sức lao động và tối ưu hóa hiệu suất kênh truyền thông của các sếp ngay hôm nay!