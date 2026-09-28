---
title: "🚀 Tự Động Hóa Tạo Nội Dung Đa Sàn Từ YouTube Bằng AI & RSS trong n8n"
description: "Biến 1 video YouTube thành hàng loạt bài đăng tối ưu cho LinkedIn, X (Twitter), Threads và Instagram hoàn toàn tự động bằng n8n, OpenRouter AI và Google Sheets."
slug: "tu-dong-hoa-tao-noi-dung-da-san-tu-youtube-bang-ai-va-rss"
tags: [n8n, automation, ai, content-creation, openrouter, telegram, google-sheets]
keywords: [n8n workflow, tạo nội dung tự động, youtube to social media, openrouter ai, content marketing automation]
---

# 🚀 Tự Động Hóa Tạo Nội Dung Đa Sàn Từ YouTube Bằng AI & RSS

Các sếp làm sáng tạo nội dung, marketing hay quản lý mạng xã hội chắc chắn đều hiểu cảm giác "kiệt sức" khi cứ phải ngồi xem video dài, tóm tắt lại, rồi lại hì hục cắt gọt, viết lại cho từng nền tảng: LinkedIn thì cần chuyên nghiệp, X (Twitter) phải ngắn gọn sắc bén, Threads thì tâm tình, còn Instagram lại cần visual cuốn hút. Làm thủ công thì tốn hàng giờ liền!

Đừng lo, workflow **Multi Platform Content Generator from YouTube using AI & RSS** do tác giả *Budi SJ* thiết kế sẽ giải quyết trọn gói bài toán này. Chỉ với một lịch trình tự động, hệ thống sẽ quét video mới trên YouTube, bóc tách nội dung, nhờ AI "hô biến" thành bài đăng cho 4 mạng xã hội lớn, lưu trữ gọn gàng vào Google Sheets và gửi thông báo kiểm duyệt qua Telegram. 100% không cần code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến 1 video YouTube thành chuỗi bài đăng đa nền tảng chỉ trong vài phút.
- **Tối ưu hóa từng nền tảng:** Nội dung được AI tùy chỉnh văn phong, giới hạn ký tự chuẩn chỉnh cho LinkedIn, X, Threads và Instagram.
- **Quản lý tập trung:** Toàn bộ lịch sử video, bản tóm tắt và nội dung tạo ra được lưu tự động vào Google Sheets để dễ dàng kiểm tra, duyệt bài và cộng tác nhóm.
- **Kiểm soát chủ động:** Nhận bản xem trước (preview) ngay qua Telegram để duyệt hoặc chỉnh sửa trước khi đăng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Sheets Template & Credentials (OAuth2):** Dùng để lưu trữ URL kênh, metadata video và nội dung xuất ra. (Tham khảo [Google Sheets template tại đây](https://docs.google.com/spreadsheets/d/17OjwIwx7eAwbkT5wtwvpCQU4rjrLH0v7j3fmC2Sc1CY/edit?usp=sharing)).
- **Supadata API Key:** Dùng để tự động lấy transcript (phụ đề/lời thoại) từ video YouTube.
- **OpenRouter API Key:** Cung cấp mô hình ngôn ngữ lớn (LLM) để tóm tắt và viết content (Workflow sử dụng model `google/gemini-2.0-flash-exp:free`).
- **Telegram Bot Token & Chat ID:** Để nhận thông báo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Mở giao diện n8n của các sếp, chọn **Add workflow** -> **Import from File** (hoặc Paste trực tiếp JSON vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 29 nodes được chia thành các cụm chức năng chính. Các sếp cần chú ý cấu hình kỹ các node sau:
- **Schedule Trigger:** Thiết lập lịch chạy tự động (ví dụ: chạy hàng ngày hoặc vài lần một tuần).
- **Get row(s) in sheet (Google Sheets):** Kết nối tài khoản Google Sheets của các sếp và trỏ đến file quản lý danh sách kênh YouTube.
- **HTTP Request & HTML Nodes:** Làm nhiệm vụ phân tích trang YouTube để lấy channel ID và tự động tạo RSS feed tương ứng.
- **Supadata API (HTTP Request1):** Cấu hình API Key của Supadata để trích xuất transcript video YouTube.
- **OpenRouter Chat Model (1 đến 4):** Cấu hình credential OpenRouter và chọn model AI (mặc định dùng `google/gemini-2.0-flash-exp:free`). Các node **Basic LLM Chain** sẽ đóng vai trò nhận prompt để viết bài cho từng nền tảng cụ thể:
  - *LinkedIn:* Định dạng chia sẻ câu chuyện, kinh nghiệm (≤ 1300 ký tự).
  - *X/Twitter:* Ngắn gọn, sắc bén (≤ 280 ký tự).
  - *Threads:* Gần gũi, mang tính trò chuyện.
  - *Instagram:* Caption ngắn gọn kèm gợi ý hình ảnh/video.
- **Google Sheets (Write/Append nodes):** Đảm bảo map đúng các cột trong Google Sheets để lưu metadata video, bản tóm tắt và nội dung các bài đăng đã tạo.
- **Send a text message (Telegram):** Điền Bot Token và Chat ID của các sếp để nhận thông báo tóm tắt và bản xem trước nội dung.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) với 1 URL kênh mẫu để kiểm tra luồng dữ liệu qua các bước AI và Google Sheets.
- Sau khi chắc chắn mọi thứ chạy trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Webhook/Slack:** Ngoài Telegram, các sếp có thể nối thêm node Slack hoặc Discord để team content cùng theo dõi và duyệt bài.
- **Tự động đăng bài:** Thay vì chỉ lưu vào Google Sheets và gửi Telegram, các sếp có thể kết nối tiếp các node như Buffer, Hootsuite hoặc API trực tiếp của LinkedIn/X để tự động xuất bản bài viết theo lịch hẹn.
- **Tinh chỉnh System Prompt:** Trong các node *Basic LLM Chain*, hãy điều chỉnh lại prompt để AI hiểu sâu hơn về văn phong (tone of voice) riêng của thương hiệu các sếp.

### 📌 Kết luận
Tự động hóa sản xuất nội dung chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n, RSS và AI đa mô hình. Hãy áp dụng ngay workflow này để tiết kiệm hàng chục giờ làm việc mỗi tuần và bứt phá sự hiện diện trên mọi nền tảng mạng xã hội nhé các sếp!