---
title: "🚀 Tự động tạo video VSL ngắn siêu tốc bằng GPT-4o, Google Veo và Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình tạo video VSL (Video Sales Letter) từ hình ảnh sản phẩm sử dụng AI đa phương thức và gửi trực tiếp về Telegram."
slug: "tu-dong-tao-video-vsl-ngan-gpt-4o-google-veo-telegram"
tags: [n8n, automation, no-code, ai, content-creation, telegram]
keywords: [n8n workflow, tao video vsl, gpt-4o, google veo, creatomate, telegram automation, ai video generation]
---

# 🚀 Tự động tạo video VSL ngắn siêu tốc bằng GPT-4o, Google Veo và Telegram

Việc sản xuất video VSL (Video Sales Letter) thủ công cho các chiến dịch marketing thường ngốn rất nhiều thời gian, từ khâu lên kịch bản, tạo hình ảnh, dựng phim đến chèn phụ đề. Các sếp có đang cảm thấy mệt mỏi khi phải tẻ nhạt lặp đi lặp lại những công đoạn này? 

Workflow n8n tuyệt vời này do chuyên gia **Koulikas Giannis** phát triển sẽ giải quyết triệt để bài toán trên. Hệ thống sẽ tự động hóa 100% quy trình: phân tích ảnh sản phẩm bằng AI, viết kịch bản, tạo video động với công nghệ AI tiên tiến, xử lý phụ đề và trả kết quả thẳng về Telegram cho các sếp chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến hình ảnh sản phẩm thành video VSL hoàn chỉnh chỉ với vài thao tác kích hoạt đơn giản.
- **Ứng dụng AI đa phương thức đỉnh cao:** Kết hợp sức mạnh của GPT-4o (phân tích & viết kịch bản) và Google Veo (tạo chuyển động video).
- **Tiết kiệm 90% thời gian:** Không còn cảnh tự tay dựng video hay chèn phụ đề thủ công từng khung hình.
- **Nhận kết quả tức thì:** Video sau khi render xong và gắn phụ đề sẽ tự động gửi thẳng về tài khoản Telegram của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted VPS).
- **OpenAI API Key:** Cho các node `AI Describe Product Image`, `AI Generate VeoPrompt` và `AI Messaging Model`.
- **Google Cloud Storage (GCS) Credentials:** Để lưu trữ và truyền tải tệp tin trung gian.
- **Google Cloud/Veo API & JWT:** Xác thực và gọi API tạo video.
- **Creatomate API (hoặc dịch vụ tương đương qua HTTP Request):** Dùng cho các node thêm phụ đề và render video.
- **Telegram Bot Token & Chat ID:** Để nhận thông báo và video hoàn thiện.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy trực tiếp đoạn JSON, sau đó paste vào giao diện n8n Editor của các sếp thông qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà vận hành, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Manual Workflow Trigger & Set Form Data:** Nơi khởi tạo quy trình bằng cách nhập dữ liệu đầu vào hoặc tải lên hình ảnh sản phẩm mẫu.
- **AI Describe Product Image, AI Generate VeoPrompt & AI Messaging Model (OpenAI):** Kết nối tài khoản OpenAI Credentials, tinh chỉnh System Prompt nếu muốn văn phong kịch bản hoặc câu lệnh tạo video (Veo Prompt) phù hợp hơn với ngách sản phẩm của mình.
- **Generate JWT Token & Fetch OAuth Token:** Điền đúng thông tin xác thực để gọi các API của Google Cloud/Veo một cách an toàn.
- **Upload File to Google Cloud Storage:** Chọn đúng Bucket Name và cấp quyền truy cập để đẩy tệp tin lên mây.
- **Post to Start Video Generation & Post to Add Captions API (HTTP Request):** Cấu hình Endpoint URL và API Key của dịch vụ render video (như Creatomate) để xử lý việc dựng phim và đóng phụ đề.
- **Send Video via Telegram:** Nhập chính xác Bot Token và Chat ID của sếp để bot có chỗ "giao hàng" tận nơi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với dữ liệu mẫu (Test run) để đảm bảo các bước gọi API, xử lý file và sinh AI không gặp lỗi gián đoạn.
- Sau khi test thành công, gạt công tắc sang trạng thái **Active** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Typeform:** Thay vì dùng Manual Trigger, các sếp có thể kết nối form đăng ký sản phẩm của khách hàng để hệ thống tự động sinh VSL ngay khi có đơn mới.
- **Lưu trữ Google Drive/Airtable:** Bổ sung thêm node lưu trữ thông tin kịch bản và đường dẫn video vào Google Sheets hoặc Airtable để tiện quản lý kho tư liệu.
- **Mở rộng kênh trả kết quả:** Ngoài Telegram, có thể cấu hình thêm node gửi video lên Slack, Discord hoặc tự động đăng nháp lên TikTok/Reels.

### 📌 Kết luận
Workflow tạo VSL tự động kết hợp GPT-4o, Google Veo và Telegram là "vũ khí bí mật" giúp các nhà sáng tạo nội dung và chủ doanh nghiệp tối ưu hóa tốc độ sản xuất video marketing. Hãy cài đặt ngay hôm nay để nâng tầm hệ thống tự động hóa của các sếp!